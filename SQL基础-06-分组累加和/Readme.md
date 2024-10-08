# 环境
本文方法在 **impala 3.1.0** 的环境下实现（spark sql也是同样的写法），下文用到的原始表 **a_test** 如下图所示：

![0-原始数据.png](https://i-blog.csdnimg.cn/blog_migrate/919cc20a777b5016d18fa37ff78b7ce9.png)

# 实现方法
现在对 **a_test** 中的数据按照 **name** 分组，以 **month_id** 排序，对 **amount** 求累加和，代码如下：

```
SELECT name,
	   month_id,
	   SUM(amount) OVER(PARTTION BY name ORDER BY month_id) AS amount_acc

  FROM income_record
 GROUP BY name, month_id, amount
```

得到的结果如下图所示：

![1-分组累加和.png](https://i-blog.csdnimg.cn/blog_migrate/b8cb9a7556e0631cd840778e374ba96b.png)

