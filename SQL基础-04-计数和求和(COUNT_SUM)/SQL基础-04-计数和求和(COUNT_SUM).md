环境：MySQL 5.7.29
下文示例中用到的表 income_record 如下：
![0-原始数据.png](https://i-blog.csdnimg.cn/blog_migrate/9dbb4e33d503a2d42746a1c781a18c3a.png)
# 1、COUNT
COUNT函数用于统计记录的条数，主要需要区分 **COUNT(col)**， **COUNT(\*)**， **COUNT(1)** 三者的区别。其中 **COUNT(col)** 是统计列 col 的记录的条数，不会对该列的**空值(NULL)**进行计数；**COUNT(\*)** 和 **COUNT(1)** 都是对全部记录的条数进行统计。COUNT函数既可以单独使用，也可以与GROUP BY函数搭配使用。
### 1.1、单独使用
现在单独使用COUNT函数对 income_record 表中的记录进行统计，代码如下：
```
SELECT COUNT(age) AS c1,
	   COUNT(*) AS c2,
	   COUNT(1) AS c3

  FROM income_record
```
得到的结果如下：

![1-COUNT.png](https://i-blog.csdnimg.cn/blog_migrate/b1859fb4645fb22b5e5e919e9ec52975.png)
### 1.2、与GROUP BY 搭配使用
现在使用 COUNT和GROUP BY 分别对 income_record 表中 name 列不同的值的条数进行统计，代码如下：
```
SELECT name,
	   COUNT(age) AS c1,
	   COUNT(*) AS c2,
	   COUNT(1) AS c3

  FROM income_record
 GROUP BY name
```
得到的结果如下：
![1-COUNT-GROUP_BY.png](https://i-blog.csdnimg.cn/blog_migrate/87b87303849aea5d97ec38a689869d84.png)
# 2、SUM
SUM函数用于计数或求和，**SUM(1)**与**COUNT(\*)/COUNT(1)**效果一样，用于统计记录的条数；**SUM(col)**用于对col列进行求和。SUM也可以单独使用或与GROUP BY搭配使用。
### 2.1、单独使用
现在单独使用SUM函数对 income_record 表中记录的条数进行统计，代码如下：
```
SELECT SUM(1)

  FROM income_record
```
得到的结果如下：
![2-SUM1.png](https://i-blog.csdnimg.cn/blog_migrate/1004166d487b21c89c30246c493c9b53.png)
### 2.2、与GROUP BY 搭配使用
现在使用 SUM和GROUP BY 分别对 income_record 表中 name 列不同的值对应的 amount 进行求和，代码如下：
```
SELECT name,
	   SUM(amount) AS sum_a

  FROM income_record
 GROUP BY name

```
得到的结果如下：
![2-SUM1-GROUP_BY.png](https://i-blog.csdnimg.cn/blog_migrate/5e6e22a598f04e4507ec5b42b6a927a3.png)

