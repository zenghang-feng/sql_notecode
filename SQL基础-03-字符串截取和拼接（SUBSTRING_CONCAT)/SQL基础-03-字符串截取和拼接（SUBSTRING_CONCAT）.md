环境：MySQL 5.7.29
下文示例中用到的表如下：
![0-原始数据.png](https://i-blog.csdnimg.cn/blog_migrate/8baf8916356fd37122312fdc3a4791ee.png)

# 1、字符串截取：SUBSTRING()
### 语法：SUBSTRING(col, pos, len)
**col：待截取的字段，字符类型；**
**pos：截取的起点，INT类型；**
**len：截取的长度，INT类型**

### 示例：
截取 birthday 字段中的年份，生成字段 sub_year，代码如下：
```
SELECT name,
	   country,
	   SUBSTRING(birthday, 1, 4) AS sub_year

  FROM tom_jerry
```
查询结果如下：
![1-SUBSTRING.png](https://i-blog.csdnimg.cn/blog_migrate/c8b8cfe1484a4720dcbf62a3100b5a9d.png)

# 2、字符串截取：SUBSTRING_INDEX()
### 语法：SUBSTRING_INDEX(col, sep, opt)
**col：待截取的字段，字符类型；**
**sep：分隔符，字符类型；**
**opt：截取得到第几个sep前的字符，INT类型**

### 示例：
截取 birthday 字段中的年份，生成字段 sub_year；截取 birthday 字段中的年份和月份，生成字段 sub_year_month，代码如下：
```
SELECT name,
	   country,
	   SUBSTRING_INDEX(birthday, '-', 1) AS sub_year,
	   SUBSTRING_INDEX(birthday, '-', 2) AS sub_year_month

  FROM tom_jerry
```
查询结果如下：
![2-SUBSTRING_INDEX.png](https://i-blog.csdnimg.cn/blog_migrate/63f2b3fcfa74fc8e3b8cb8eeb73cd69f.png)

# 3、字符串拼接：CONCAT()
### 语法：CONCAT(str1, str2, str3,...)
**str1，str2，str3：需要拼接的字符串，字符类型**

### 示例：
将表中的name、country和birthday 3个字段用 '+' 拼接起来，生成字段 col_concat，代码如下：
```
SELECT name,
	   country,
	   CONCAT(name, '+', country, '+', birthday) AS col_concat

  FROM tom_jerry
```
查询结果如下：
![3-CONCAT.png](https://i-blog.csdnimg.cn/blog_migrate/a9dfc69e09a3e5111a0b78f79a7974f7.png)

# 4、字符串拼接：CONCAT_WS()
### 语法：CONCAT_WS(sep, str1, str2, str3,...)
**sep：拼接用的分隔符，字符类型；**
**str1，str2，str3：需要拼接的字符串，字符类型**

### 示例：
将表中的name、country和birthday 3个字段用 '+' 拼接起来，生成字段 col_concat，代码如下：
```
SELECT name,
	   country,
	   CONCAT_WS('+', name, country, birthday) AS col_concat

  FROM tom_jerry
```
查询结果如下：
![4-CONCAT_WS.png](https://i-blog.csdnimg.cn/blog_migrate/54191d4dccf029040064f2e394d2d55a.png)

