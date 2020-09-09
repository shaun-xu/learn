##  Array

* 单独push

```
db.blog.updateOne({"_id":"aaaa"}, {"$push":{"field",{"data1":2,"data2":3}}} )
```

* 同时push多条数据

```
db.blog.updateOne({"_id":"aaaa"},{"$push":{"field":{"$each":["a","b","c"]}})
```

* push后保持数据最后10条

```
db.blog.updateOne({"_id":"aaaa"},{"$push":{"$each":["a","b","c"],"$slice":-10}})
```

* 插入后排序

```
db.movies.updateOne({"genre" : "horror"},
{"$push" : {"top10" : {"$each" : [{"name" : "Nightmare on Elm Street", "rating" : 6.6},
{"name" : "Saw", "rating" : 4.3}],
"$slice" : -10,
"$sort" : {"rating" : -1}}}})
```

* 把Array当做sets使用

```
db.users.updateOne({"_id" : ObjectId("4b2d75476cc613d5ee930164")},
{"$addToSet" : {"emails" : "joe@gmail.com"}})

可以用$each来多个
db.users.updateOne({"_id" : ObjectId("4b2d75476cc613d5ee930164")},
{"$addToSet" : {"emails" : {"$each":["joe@gmail.com","joe@gmail.com"]}}})
```



* 从array中删除

```
db.lists.insertOne({"todo" : ["dishes", "laundry", "dry cleaning"]})
db.lists.updateOne({}, {"$pull" : {"todo" : "laundry"}})
```



* 

  ```
  
  ```

  

  

  

