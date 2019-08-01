>在mybatis的mapper配置文件中，可以利用<foreach>标签实现sql条件的循环，可完成类似批量的sql
>mybatis接受的参数分为：（1）基本类型（2）对象（3）List（4）数组（5）Map

> 无论传哪种参数给mybatis，他都会将参数放在一个Map中：
> 如果传入基本类型：变量名作为key，变量值作为value    此时生成的map只有一个元素。
> 如果传入对象：        对象的属性名作为key，属性值作为value，
> 如果传入List：         "list"作为key，这个List是value  （这类参数可以迭代，利用<foreach>标签实现循环）
> 如果传入数组：       "array"作为key，数组作为value（同上）
> 如果传入Map：        键值不变。

> <foreach>标签的用法：
> 六个参数：
> collection：要循环的集合
> index：循环索引（不知道啥用。。）
> item：集合中的一个元素（item和collection，按foreach循环理解）
> open：以什么开始
> close：以什么结束                                                                                           separator：循环内容之间以什么分隔 