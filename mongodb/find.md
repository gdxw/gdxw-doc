## mongodb查找

mongodb常用查询
``` js
db.workmate.find({
        "skill.skillOne":"HTML+CSS"     //查询条件
    },{
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })
```

**不等修饰符**
* 小于($lt):英文全称less-than
* 小于等于($lte)：英文全称less-than-equal
* 大于($gt):英文全称greater-than
* 大于等于($gte):英文全称greater-than-equal
* 不等于($ne):英文全称not-equal

``` js
db.workmate.find({
        "age":{$lte: 40, $gte: 20}     //查询条件
    },{
        age: true,
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })

```

**$in修饰符**

查询指定的条件包含于

``` js
db.workmate.find({
        "age":{$in:[40,25]}     //查询条件
    },{
        age: true,
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })
```
**$nin修饰符**

查询指定的条件不包含于

``` js
db.workmate.find({
        "age":{$nin:[40,25]}     //查询条件
    },{
        age: true,
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })
```

**$or修饰符**

查询多个条件,满足一个条件即可

``` js
db.workmate.find({
        $or:[
            {"age":{$nin:[40,25]},
            {"skill.skillThree":'PHP'}
        ]//查询条件
    },{
        age: true,
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })
```

**$and修饰符**

查询多个条件,同时满足条件

``` js
db.workmate.find({
        $and:[
            {"age":{$lte:30},
            {"skill.skillThree":'PHP'}
        ]//查询条件
    },{
        age: true,
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })
```

**$not修饰符**

查询除条件之外的值,跟$and相反

``` js
db.workmate.find({
        age:{
            $lte:30,
            $gte:20
        }//查询条件
    },{
        age: true,
        name:true,                      // 输出内容
        "skill.skillOne":true,
        _id:false
    })
```

**$all-数组多项查询**

要查询出喜欢看电影和看书的人员信息，也就是对数组中的对象进行查询

``` js
db.workmate.find({
    interest:{$all:["看电影","看书"]},
    {name:1,interest:1,age:1,_id:0}
})
```

**$in-数组的或者查询**

用$all修饰符，是需要满足所有条件的，$in主要满足数组中的一项就可以被查出来（有时候会跟$or弄混）

``` js
db.workmate.find({
    interest:{$in:["看电影","看书"]},
    {name:1,interest:1,age:1,_id:0}
})
```

**$size-数组个数查询**

$size修饰符可以根据数组的数量查询出结果。比如现在我们要查找兴趣的数量是5个人员信息

``` js
db.workmate.find(
    {interest:{$size:5}},
    {name:1,interest:1,age:1,_id:0} 
)
```

**$slice-显示选项**

有时候我并不需要显示出数组中的所有值，而是只显示前两项，比如我们现在想显示每个人兴趣的前两项，而不是把每个人所有的兴趣都显示出来。

``` js
db.workmate.find(
    {},
    {name:1,interest:{$slice:2},age:1,_id:0}
)
```

**find参数：**
* query：这个就是查询条件，MongoDB默认的第一个参数。
* fields：（返回内容）查询出来后显示的结果样式，可以用true和false控制是否显示。
* limit：返回的数量，后边跟数字，控制每次查询返回的结果数量。
* skip:跳过多少个显示，和limit结合可以实现分页。
* sort：排序方式，从小到大排序使用1，从大到小排序使用-1。

分页Demo：

``` js
db.workmate.find({},{name:true,age:true,_id:false}).limit(0).skip(2).sort({age:1});
```

**$where修饰符**

它是一个非常强大的修饰符，但强大的背后也意味着有风险存在。它可以让我们在条件里使用javascript的方法来进行复杂查询。

``` js
db.workmate.find(
    {$where:"this.age>30"},
    {name:true,age:true,_id:false}
)
```

**hasNext循环结果**

想在文本中执行我们的find语句要用到游标和循环的操作

``` js
var db = connect("company")  //进行链接对应的集合collections
var result = db.workmate.find() //声明变量result，并把查询结果赋值给result
//利用游标的hasNext()进行循环输出结果。
while(result.hasNext()){
    printjson(result.next())  //用json格式打印结果
}
```

**forEach循环**

利用hasNext循环结果，需要借助while的帮助，MongoDB也为我们提供了forEach循环，现在修改上边的代码，使用forEach循环来输出结果。

``` js
var db = connect("company")  //进行链接对应的集合collections
var result = db.workmate.find() //声明变量result，并把查询结果赋值给result
//利用游标的hasNext()进行循环输出结果。
result.forEach(function(result){
    printjson(result)
})
```
