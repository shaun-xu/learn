##  概括

<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1gikmoyfaxjj31120fy787.jpg" alt="image-20200909193501163" style="zoom:33%;" />

聚合类似于linux管道，把一个操作分为几个步骤，一个stage的输出是下一个stage的输入。

```
db.companies.aggregate([
{$match: {founded_year: 2004}}, 
{$project: {_id: 0,name: 1, founded_year: 1}} 
])
输出：
{"name": "Digg", "founded_year": 2004 }
{"name": "Facebook", "founded_year": 2004 }
```

这个例子分为两个阶段，一个match阶段，一个project阶段。match阶段把匹配的文档列表发送给project，project输出两个字段。

```
db.companies.aggregate([
{ $match: { founded_year: 2004 } },
{ $sort: { name: 1} },
{ $limit: 5 { $project: _id: 0, name: 1}, 
{$project: {_id: 0,name: 1, founded_year: 1} 
]
```

排序后输出前五条。

* 复合操作

```
db.companies.aggregate([
{$match: {founded_year: 2004}}, {$sort: {name: 1}},
{$skip: 10},
{$limit: 5},
{$project: {
_id: 0,
name: 1}}])
```

##  表达式



| 表达式     | 描述                   |
| :--------- | :--------------------- |
| Boolean    | 与，或，非操作         |
| Set        | 集合操作（交急，并集） |
| Comparison | 一些列的区间表达式     |
| Arithmetic |                        |
|            |                        |
|            |                        |
|            |                        |



