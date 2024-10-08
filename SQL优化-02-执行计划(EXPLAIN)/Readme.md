# 1、基本介绍
&emsp;&emsp;EXPLAIN语句可以获得关于MySQL如何执行SELECT语句的信息，借助于EXPLAIN，可以知道什么时候必须为表加入索引以得到一个使用索引来寻找记录的更快的SELECT。
# 2、语法
```
EXPLAIN [EXTENDED] SELECT select_options
```
# 3、示例
&emsp;&emsp;示例用到的原始表如下：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4d9f5eeb10fd8254c4688d33b55da054.png#pic_center)
&emsp;&emsp;表中的索引如下图所示：

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/1e8b86cbc601f6bf5a8c17f8cd47a3a2.png#pic_center)

&emsp;&emsp;执行如下的查询，使用 EXPLAIN 获取语句的执行计划：

```sql
EXPLAIN EXTENDED 
SELECT * FROM test_table WHERE id = 1
 UNION
SELECT * FROM test_table WHERE id = 2
```
&emsp;&emsp;得到的执行计划如下图所示：

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d27b6a627c7ea2101f7d71bb6bb21cbc.png#pic_center)
# 4、执行计划解释
## 4.1 id
&emsp;&emsp; **id** 是 SELECT 的查询序列号。**id** 相同时执行顺序由上到下，**id** 不同时，先执行 **id** 大的查询，**id** 为 **null** 表示查询结果集。
## 4.2 select_type
&emsp;&emsp; **select_type** 是查询类型，有如下取值：

&emsp;&emsp; 1. **SIMPLE** ：简单查询(不使用UNION或子查询)。
&emsp;&emsp; 2. **PRIMARY**  ：包含子查询时，最外层的查询。
&emsp;&emsp; 3. **UNION**  ：UNION中的第二个或后面的SELECT语句。
&emsp;&emsp; 4. **UNION RESULT**：UNION的结果集。
&emsp;&emsp; 5. **SUBQUERY**：子查询中的第一个查询。
&emsp;&emsp; 6. **DEPENDENT SUBQUERY**：子查询中的第一个查询，取决于外面的查询。
&emsp;&emsp; 7. **DERIVED**：导出表的SELECT(FROM子句的子查询)。

 ## 4.3 table
 &emsp;&emsp; **table** 是查询输出的行所引用的表，如果表存在别名，那么这里显示的是表的别名。
 ## 4.4 partitions
&emsp;&emsp; **partitions** 是表的分区信息。
## 4.5 type
&emsp;&emsp; **type** 是联接类型。下面给出各种联接类型，按照性能从高到低进行排序：

&emsp;&emsp; 1. **system** ：表仅有一行(=系统表)。这是const联接类型的一个特例。
&emsp;&emsp; 2. **const**  ：表最多有一个匹配行，它将在查询开始时被读取。因为仅有一行，在这行的列值可被优化器剩余部分认为是常数。const 表很快，因为它们只读取一次。const 用于用常数值比较PRIMARY KEY或UNIQUE索引的所有部分时。
&emsp;&emsp; 3. **eq_ref**  ：索引的所有部分被联接使用，并且索引是UNIQUE或PRIMARY KEY。eq_ref 可以用于使用 = 操作符比较的带索引的列，比较值可以为常量或一个使用在该表前面所读取的表的列的表达式。
&emsp;&emsp; 4. **ref**：使用的索引不是UNIQUE或PRIMARY KEY。ref可以用于使用=或<=>操作符的带索引的列。
&emsp;&emsp; 5. **ref_or_null**： 该联接类型如同ref，但是添加了MySQL可以专门搜索包含NULL值的行。
&emsp;&emsp; 6. **index_merge**： 该联接类型表示使用了索引合并优化方法。
&emsp;&emsp; 7. **unique_subquery**： 在 IN 子查询中使用 eq_ref 。
&emsp;&emsp; 8. **index_subquery**： 在 IN 子查询中使用 ref 。
&emsp;&emsp; 9. **range**： 使用一个索引来选择行，只检索给定范围的行。
&emsp;&emsp; 10. **index**： 遍历索引全部取值。
&emsp;&emsp; 11. **ALL**： 进行全表扫描。
## 4.6  possible_key
&emsp;&emsp; **possible_keys** 表示查询过程中可能使用的索引。
## 4.7  key
&emsp;&emsp; **key** 表示查询过程实际使用的索引。
## 4.8  key_len
&emsp;&emsp; **key_len** 表示查询所使用的索引的长度。
## 4.9  ref
&emsp;&emsp; **ref** 显示使用哪个列或常数与索引一起从表中进行查询。
## 4.10  rows
&emsp;&emsp;  **rows** 显示执行查询时必须扫描的行数，不一定是实际值。
# 5、总结
&emsp;&emsp; 通过 EXPLAIN 语句，可以查看查询的详细信息，分析在什么时候可以添加索引，以提高查询效率。


参考链接：https://www.mysqlzh.com/doc/66/292.html
