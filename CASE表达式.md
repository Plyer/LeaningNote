## CASE表达式

1. 语法：

   + ![搜索CASE表达式](http://ww3.sinaimg.cn/large/006tNc79ly1g5s88msdpyj31660dkgnv.jpg)
   + ![简单CASE表达式](http://ww2.sinaimg.cn/large/006tNc79ly1g5s8ahlrmmj310q0dmq56.jpg)
   + > WHEN 子句中的“< 求值表达式 >”就是类似“列 = 值”这样，返回值为真值(TRUE/FALSE/UNKNOWN)的表达式。ELSE子句也可以省略不写，这时会被默认为ELSE NULL。

2. 使用场景：在对 SELECT 语句的结果进行编辑时，CASE 表达式能够发挥较大
   作用。

3. 举例：

   ![CASE表达式使用](http://ww1.sinaimg.cn/large/006tNc79ly1g5s8atia33j30zx0u046y.jpg)

   ![执行结果](http://ww1.sinaimg.cn/large/006tNc79ly1g5s8b7av7aj313e0fogom.jpg)

