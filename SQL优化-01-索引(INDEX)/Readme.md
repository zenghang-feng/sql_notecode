# 1、索引的基本概念
&emsp;&emsp;索引是一种特殊的查询表，可以被数据库搜索引擎用来加速数据的检索，用于快速找出在某个列中有一特定值的行。
&emsp;&emsp;不使用索引，MySQL必须从第1条记录开始然后读完整个表直到找出相关的行。表越大，花费的时间越多。
&emsp;&emsp;如果表中查询的列有一个索引，MySQL能快速到达一个位置去搜寻到数据文件的中间，没有必要看所有数据。如果一个表有1000行，这比顺序读取至少快100倍。注意如果你需要访问大部分行，顺序读取要快得多，因为此时我们避免磁盘搜索。
&emsp;&emsp;索引能够提高 SELECT 查询和 WHERE 子句的速度，但是却降低了包含 UPDATE 语句或 INSERT 语句的数据输入过程的速度。索引的创建与删除不会对表中的数据产生影响。

# 2、索引的分类
&emsp;&emsp;从应用上来说，索引可以分为 **普通索引**，**唯一索引**，**复合索引**。
&emsp;&emsp;**普通索引**：即一个索引只包含单个列，一个表可以有多个单列索引。
&emsp;&emsp;**唯一索引**：索引列的值必须唯一，但允许有空值。
&emsp;&emsp;**复合索引**：多列值组成一个索引，专门用于组合搜索，其效率大于索引合并。

# 3、索引的创建
## 3.1普通索引
&emsp;&emsp;普通索引基于单一的字段创建，其基本语法如下所示：
```
CREATE INDEX index_name ON table_name (column_name);
```

&emsp;&emsp;现在有一个名为 test_table 的表，如下图所示：

![test_table.PNG](https://i-blog.csdnimg.cn/blog_migrate/f5da8f22fb26ff5d0c8053b37c83dc7a.png)

&emsp;&emsp;在 test_table 中创建基于 `name` 字段的普通索引，代码如下：
```
CREATE INDEX index_1 ON test_table (`name`)
```
&emsp;&emsp;创建完成后可以查看索引，如下图所示：

![普通索引.PNG](https://i-blog.csdnimg.cn/blog_migrate/3a1bcd569e302dbdf9e5a5b5102ed024.png)

## 3.2唯一索引
&emsp;&emsp;在 test_table 中创建基于 id 字段的唯一索引，代码如下：
```
CREATE UNIQUE INDEX index_unique ON test_table (id)
```
&emsp;&emsp;创建完成后可以查看索引，如下图所示：

![唯一索引.PNG](https://i-blog.csdnimg.cn/blog_migrate/16a81b4f6e71e2a0626b1041d0cad692.png)

## 3.3复合索引
&emsp;&emsp;在 test_table 中创建基于 id，`name` 字段的复合索引，代码如下：
```
CREATE INDEX index_2 ON test_table (id, `name`)
```
&emsp;&emsp;创建完成后可以查看索引，如下图所示：

![复合索引.PNG](https://i-blog.csdnimg.cn/blog_migrate/6da03dfeca0d932628901f4ed6cddf55.png)

# 4、删除索引
&emsp;&emsp;以删除索引 index_1 为例，代码如下：
```
DROP INDEX index_1 ON test_table
```
&emsp;&emsp;删除完成后可以查看索引，发现索引 index_1已被删除 ，如下图所示：

![删除索引.PNG](https://i-blog.csdnimg.cn/blog_migrate/9f351c4956e335e16c40b8c2d68235a7.png)

# 5、总结
1、创建索引时，需要参考 WHERE 语句中经常出现的字段或字段组合。
2、经常修改的字段不建议创建索引。
3、包含大量 NULL 值的字段，不要使用索引。

参考链接：
https://www.mysqlzh.com/doc/68/303.html
https://mp.weixin.qq.com/s/gNmWY8ob-QN6ZVF7e-71cA
