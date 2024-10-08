
本文的SQL语句基于MySQL，实现对表的增删改查等基本操作。
## 1、 创建表
创建一个名称是 tom_jerry 的表，设置 id 字段为自增主键，代码如下：
```
CREATE TABLE tom_jerry
(
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(255),
height DECIMAL(38,2),
weight DECIMAL(38,2),
age INT,
sex VARCHAR(255),
PRIMARY KEY (id)
)
```
运行代码，生成的表如下图：
![图片0-创建表.png](https://i-blog.csdnimg.cn/blog_migrate/a5f9df6d2ab38e18f839a315874a0a25.png)

## 2、插入数据
向表中插入数据3条数据，代码如下：
```
INSERT INTO tom_jerry (name, height, weight, age, sex) VALUES ('tom', 30, 10, 5, 'meal');
INSERT INTO tom_jerry (name, height, weight, age, sex) VALUES ('jerry', 5, 2, 3, 'male');
INSERT INTO tom_jerry (name, height, weight, age, sex) VALUES ('lucy', 10, 5, 10, 'female');
```
运行代码，表中的数据如下：
![图片1-添加记录.png](https://i-blog.csdnimg.cn/blog_migrate/4f807fa00b95580ee6bd8f482a4e685c.png)
## 3、删除数据
删除 name 为 lucy 的那一行记录，代码如下：
```
DELETE FROM tom_jerry WHERE name = 'lucy'
```
删除后的表中只剩下两条记录，如下图所示：
![图片2-删除记录.png](https://i-blog.csdnimg.cn/blog_migrate/ab21b1b39a9afe6f4452d8dc3ccb4a13.png)
## 4、修改数据
修改 name 为 tom 的那一行记录里的 sex 列，代码如下：
```
UPDATE tom_jerry SET sex = 'male' WHERE name = 'tom'
```
修改后的数据如下图所示：
![图片3-修改记录.png](https://i-blog.csdnimg.cn/blog_migrate/96c977a159ff532c65885ad87bf0d509.png)
## 5、查询数据
查询 name 为 jerry 的记录，代码如下：
```
SELECT * FROM tom_jerry WHERE name = 'jerry'
```
查询结果如下图所示：
![图片4-查询记录.png](https://i-blog.csdnimg.cn/blog_migrate/1b7311e1126211f0677a7a39f7381713.png)
以上就是SQL增删改查的基本操作。
