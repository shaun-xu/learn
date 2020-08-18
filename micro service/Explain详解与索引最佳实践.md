## Explain 

<img src="/Users/xxp/Library/Application Support/typora-user-images/image-20200815213006647.png" alt="image-20200815213006647" style="zoom:50%;" />

* simple : 简单查询，查询不包括子查询和union
* Primary:   复杂查询中最外层的select
* Subquery: 包含在select总的子查询（不在from子句中）
* Derived:  包含在from子句中的子查询，mysql会将结果存储在一个临时表中，也成为派生表。



### 1：type  列

>  这一列表示关联类型或访问类型，即mysql决定如何查找表中的行，查找数据行记录的大概范围

依次从最优到最差分别为：**system>const>eq_ref>ref>range>index>ALL** 一般要达到ref级别



### 示例

#### 1

<img src="/Users/xxp/Library/Application Support/typora-user-images/image-20200815215400752.png" alt="image-20200815215400752" style="zoom:50%;" />

> eq_ref 代表是按照主键关联，速度也是非常快的

#### 2

<img src="/Users/xxp/Library/Application Support/typora-user-images/image-20200815215731324.png" alt="image-20200815215731324" style="zoom:50%;" />

