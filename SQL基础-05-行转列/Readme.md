环境：MySQL 5.7.29
# 0、问题描述
现在有如下图所示的表 income_record ：

![00-原始数据.png](https://i-blog.csdnimg.cn/blog_migrate/49083729dba7e85139996acc85ef2e8f.png)

需要按照 name，month_id 对 amount 进行求和，计算出每个 name 每个 month_id 对应的收入之和，并且将每个月的收入之和作为一列，需要生成的目标表如下：

![00-目标表.PNG](https://i-blog.csdnimg.cn/blog_migrate/6e7cab74af39692271169bd50d7cab04.png)

有如下两种方式可以实现：

# 方法1
方法1首先分别对每月的数据进行求和，然后在用 JOIN 方法拼接各个月的数据，得到最终结果。当月份很多时，这种方法较为繁琐。具体代码如下：

```
SELECT t1.name,
	   t1.amount_m1,
	   t2.amount_m2
  FROM
  
(
SELECT name,
	   SUM(amount) AS amount_m1

  FROM income_record
 WHERE month_id = '2021-01'
 GROUP BY name
) t1

  LEFT JOIN

(
SELECT name,
	   SUM(amount) AS amount_m2

  FROM income_record
 WHERE month_id = '2021-02'
 GROUP BY name
) t2

    ON t1.name = t2.name

```
得到的效果如下图所示：

![01-JOIN-行转列.png](https://i-blog.csdnimg.cn/blog_migrate/3d17e214c249960d7a2dd31d20549fea.png)

# 方法2（推荐）
方法2直接进行求和，在求和时对 amount 进行判断，计算1月数据时其他月的数据设置为0，计算2月数据时其他月的数据设置为0。这种方法较为简便。代码如下：

```
SELECT name,
	   SUM(IF(month_id = '2021-01', amount, 0)) AS amount_m1,
	   SUM(IF(month_id = '2021-02', amount, 0)) AS amount_m2

  FROM income_record
 GROUP BY name
```

得到的效果与方法1一致，结果如下图：

![02-IF-行转列.png](https://i-blog.csdnimg.cn/blog_migrate/3042acb35495175e0a61b2d14f997f95.png)



