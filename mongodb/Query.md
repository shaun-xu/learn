##  基本操作

* 返回需要的key

```
> db.users.find({}, {"username" : 1, "email" : 1}) 

{
"_id" : ObjectId("4ba0f0dfd22aa494fd523620"), 
"username" : "joe",
"email" : "joe@example.com"
}
```

* 排除一些key

```
> db.users.find({}, {"username" : 1, "_id" : 0}) 

{
"username" : "joe",
}
```

>  请注意： 查询语句里面的值只能是固定的值，不能是文档中其他的字段，这点和mysql不同
>
> "$lt", "$lte", "$gt", and "$gte" are all comparison operators, corresponding to <, <=, >, and >=
>
>  例如： db.users.find({"age" : {"$gte" : 18, "$lte" : 30}})

* in  & nin 操作

```
db.raffle.find({"ticket_no" : {"$in" : [725, 542, 390]}})
db.raffle.find({"ticket_no" : {"$nin" : [725, 542, 390]}})
```

* or 操作

```
db.raffle.find({"$or" : [{"ticket_no" : 725}, {"winner" : true}]})

db.raffle.find({"$or" : [{"ticket_no" : {"$in" : [725, 542, 390]}}, {"winner" : true}]})
```

* $Mod   $not

```
db.users.find({"id_num" : {"$mod" : [5, 1]}})
db.users.find({"id_num" : {"$not" : {"$mod" : [5, 1]}}})
```

> 注意： 条件语句的$一般都在内部， 操作的$一般都在外侧
>
> db.users.find({"age" : {"$lt" : 30, "$gt" : 20}})
>
> db.user.updateOne({}, {"$inc" : {"age" : 1}, "$set" : {age : 40}})
>
> $inc和$set是在外面包围着的

## 根据类型查询

> null 是特殊字符
>
> db.c.find({"y" : null})

* null包含了没有这个key，或者key为null的情况

```
> db.c.find({"z" : null})

{ "_id" : ObjectId("4ba0f0dfd22aa494fd523621"), "y" : null } 
{ "_id" : ObjectId("4ba0f0dfd22aa494fd523622"), "y" : 1 }
{ "_id" : ObjectId("4ba0f148d22aa494fd523623"), "y" : 2 }
```

* 可以查包含key的情况

```
> db.c.find({"z" : {"$eq" : null, "$exists" : true}})
```

## 正则表达式

```
> db.users.find( {"name" : {"$regex" : /joe/i } })
或者
> db.users.find({"name" : /joey?/i})
```

> \> db.foo.insertOne({"bar" : /baz/}) 
>
> db.foo.find({"bar" : /baz/}) 
>
> 
>
>  {
>
> "_id" : ObjectId("4b23c3ca7525f35f94b60a2d"),
>
> "bar" : /baz/ 
>
> }
>
> 

## 查询array

* 单个匹配

```
> db.food.insertOne({"fruit" : ["apple", "banana", "peach"]})
 
> db.food.find({"fruit" : "banana"})
```

* 多个匹配(不关注顺序)

```
> db.food.insertOne({"_id" : 1, "fruit" : ["apple", "banana", "peach"]})
> db.food.insertOne({"_id" : 2, "fruit" : ["apple", "kumquat", "orange"]}) 
> db.food.insertOne({"_id" : 3, "fruit" : ["cherry", "banana", "apple"]})
> db.food.find({fruit : {$all : ["apple", "banana"]}})

{"_id" : 1, "fruit" : ["apple", "banana", "peach"]} 
{"_id" : 3, "fruit" : ["cherry", "banana", "apple"]}
```

* 整个匹配

```
> db.food.find({"fruit" : ["apple", "banana", "peach"]})

{"_id" : 1, "fruit" : ["apple", "banana", "peach"]} 
```

* 按照数组长度

```
> db.food.find({"fruit" : {"$size" : 3}})
```

* slice操作返回固定长度的array

```
db.food.find({},{"fruit" : {"$slice":10}})
db.food.find({},{"fruit" : {"$slice":[1,2]}})
```

* 返回第一个

```
> db.food.find({}, {"fruit.$" : 1}})

{"_id" : 1, "fruit" : ["apple"]} 
{"_id" : 2, "fruit" : ["cherry"]}
```

* array与范围查询

  > 猜想： {"x" : {"$gt" : 10, "$lt" : 20}}  
  >
  > X 有以下几种情况：
  >
  > {"x" : 5}
  >  {"x" : 15}
  >  {"x" : 25}
  >  {"x" : [5, 25]}

```
> db.test.find({"x" : {"$gt" : 10, "$lt" : 20}}) 

{"x" : 15}
{"x" : [5, 25]}
```



