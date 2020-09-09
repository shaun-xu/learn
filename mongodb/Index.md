##  查询实例

<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1giefaqe0hyj30na0dq3z7.jpg" alt="image-20200904104546344" style="zoom:33%;" />

inputStage是给上层提供数据的层，在这个例子中，有一个inputStage，一个"IXSCAN"**索引扫描**，然后将扫描出来的document提供给父层。

<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1gieffq809kj30gi0a0glx.jpg" alt="image-20200904105036678" style="zoom:33%;" />

被拒绝的查询是一个SORT，按照student_id来排序，当我们看到SORT的时候，说明**mongodb无法利用索引去排序**，因此它必须把数据加载到内存中，进行排序。

> 如果你查询的数据的字段只包含了index,那么查询的时候就不会把文档数据从磁盘上读出来。



* or 语句分析

```
db.foo.find({"$or" : [{"x" : 123}, {"y" : 456}]}).explain()
```

根据输出结果可以看出来，他把or分成了两个语句，一个按照x，一个按照y索引去查询，然后合并结果，这样的效率比较低，一般用$in来替换$or

*  嵌入式索引

```
{
"username" : "sid", 
"loc" : 
{
"ip" : "1.2.3.4", 
"city" : "Springfield", 
"state" : "NY"
}
}
```

我们可以通过以下命令来创建索引：

```
 > db.users.ensureIndex({"loc.city" : 1})
```

