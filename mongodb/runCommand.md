
## 修改：状态返回与安全

检查据库链接成功
``` js
db.runCommand({ping:1})
```

进行数据库操作

``` js
var db = connect("company")
var myModify = {
    findAndModify: "workmate",
    query: {name: 'DaiXingWang'},
    update:{$set: {age: 25}},
    new: true   //更新完成，需要查看结果，如果为false不进行查看结果
}

var ResultMessage = db.runCommand(myModify);

printjson(ResultMessage);

```

> findAndModify的性能是没有直接使用db.collections.update的性能好，但是在实际工作中都是使用它，毕竟要商用的程序安全性还是比较重要的

**findAndModify属性值：**
* query：需要查询的条件/文档
* sort:    进行排序
* remove：[boolean]是否删除查找到的文档，值填写true，可以删除。
* new:[boolean]返回更新前的文档还是更新后的文档。
* fields：需要返回的字段
* upsert：没有这个值是否增加。
