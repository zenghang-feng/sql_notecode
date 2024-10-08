环境：MySQL 5.7.29 
下文示例中用到的表如下：
![1_原始表.png](https://i-blog.csdnimg.cn/blog_migrate/1eb2b855a397e6cc3db3a99529d7b660.png)

# 1、IF语句
### 简介：
当判断条件只分为两种情况时，可以使用IF语句进行条件判断
### 语法：
**IF(exp, operation1, operation2)**
当条件满足 exp 时，会执行 operation1；不满足exp 时，会执行 operation2
### 示例：
现在通过判断人员所在国家，添加名称是 location 的一列，location 的取值为国内或国外，代码如下:
```
SELECT name,
	   country,
	   IF(country='中国', '国内', '国外') AS location

  FROM tom_jerry
```
查询结果如下：
![2_添加location标签.png](https://i-blog.csdnimg.cn/blog_migrate/f0534fd950ec7b46bc01d2256f25e966.png)

# 2、CASE语句
### 简介：
当判断条件分为多种情况时，可以使用CASE语句进行条件判断
### 语法：
**CASE WHEN exp1 THEN operation1**
　　　**WHEN exp2 THEN operation2**
	  　　　 ......
	  　　　 **END**

当条件满足 exp1 时，会执行 operation1；满足exp2 时，会执行 operation2，依次进行判断
### 示例：
现在需要通过判断人员所在国家，添加名称是 continent 的一列，continent 的取值为亚洲、欧洲、北美洲等7大洲，代码如下：
```
SELECT name,
	   country,
	   CASE WHEN country='中国' THEN '亚洲'
	   		WHEN country='美国' THEN '北美洲'
	   		WHEN country='英国' THEN '欧洲'
	   		END AS continent

  FROM tom_jerry
```
查询结果如下：
![3_添加continent标签.png](https://i-blog.csdnimg.cn/blog_migrate/bbe977d918febffc7c71abf269c665c4.png)

