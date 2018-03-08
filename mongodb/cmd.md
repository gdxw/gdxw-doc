## mongodb 常用命令

mongodb 常用库查询命令

``` shell
mongod      ## 启动mongodb服务
mongo       ## 进入mongo shell
show dbs    ## 查看库
use ${dbname}       ## 进入${name}库
show collections    ## 查看库中的集合
db                  ## 显示当前位置
db.dropDatabase     ## 删除整个数据库
```

mongodb 集合常用操作
``` shell
db.${集合}.insert(${data})    ## 新建数据集合，并插入数据
db.${集合}.find()             ## 查询数据集合数据
db.${集合}.findOne()          ## 查询第一个文件数据
db.${集合}.update(${查询},${修改})    ## 根据条件查询数据，并进行修改操作
db.${集合}.remove(${查询})     ## 根据条件删除数据
db.${集合}.drop()             ## 删除集合
```

mongodb 修改操作(update)

``` shell
db.${集合}.update(${查询},{$set:${data}})     ## 只更新需要更新的数据，不会重复覆盖
db.${集合}.update(${查询},{$unset:${data}})   ## 删除部分数据
db.${集合}.update(${查询},{$inc:${data}})     ## 对数字进行计算

db.${集合}.update({},{$set:${data}},{multi:true}) ## multi， true：全部修改，false只修改一部分

db.${集合}.update(${查询},{$set:{age:20}},{upsert:true})    ## upsert true代表没有就添加，false代表没有不添加(默认值)。

db.${集合}.update(${查询},{$push:${data}})      ## 追加

db.${集合}.update(${查询名称:{$ne:查询值}},{$push:${data}}) ## 查询该值是否存在，没有追加  （没有则修改，有则不修改）

db.${集合}.update(${查询},{$addToSet:${data}})  ## 升级版的$ne

var $newInterset=["Sing","Dance","Code"];
db.${集合}.update(${查询},{$addToSet:${name:{$each:$newInterset}}})  ## 升级版的$ne  批量追加

db.${集合}.update(${查询},{$pop:${name:1}})  ## $pop只删除一次，并不是删除所有数组中的值  1从数组末端进行删除,-1：从数组开端进行删除

db.${集合}.update(${查询},{$set:{"name.2":"data"}}) ##从数组的第几位开始修改


```



