# EXPLAIN命令

### 定义

`EXPLAIN`命令是查看查询优化器如何决定执行查询的主要方法

### 用法

`EXPLAIN` 后跟上`DML`语句

### EXPLAIN中的列

#### id 列

对应查询使用的表和查询顺序

#### select_type 列

这一列显示了对应的查询是简单查询还是复杂查询。

复杂查询包括以下4种：

- SUBQUERY：包含在SELECT列表中的子查询(不在FROM字句)
- DERIVED：表示包含在FROM字句种的子查询
- UNION：在UNION中的第二个和随后的SELECT
- UNION RESULT：用来从UNION的匿名临时表中查询结果的SELECT

#### table 列

这一列显示对应行正在访问哪个表(表名或别名)

#### type 列

访问类型——MySQL查找表中行的方式。效率从最差到最优：

- ALL：全表扫描(例外，使用了LIMIT，或者在Extra列中显示”Using distinct/not exists“)
- Index：按索引顺序全表扫描，避免了排序，回表开销大(随机访问)。如果Extra显示"Using index"表示使用覆盖索引(不回表，开销小)
- range：范围索引扫描，例如BETWEEN、WHERE中带有>的查询、IN()、OR
- ref：索引查找。只有当使用非唯一索引或者唯一索引的非唯一前缀时发生，索引与某个参考值比较，返回匹配的行。
- eq_ref：唯一索引查找，使用主键或者唯一索引，只会返回一条记录。
- const, system：当MySQL能对查询的某部分优化转换成常量时。例如`SELECT id FROM user WHERE id = 1`
- NULL：MySQL在优化阶段分解查询语句，在执行阶段不需要访问表或索引。例如，从一个索引列选取最小值可以通过单独查找索引来完成，不需要再执行时访问表。

#### possible_keys 列

这一列显示了查询可以使用哪些索引，基于查询访问的列和使用的比较操作符来判断

#### key 列

MySQL实际采用的索引

#### key_len 列

MySQL在索引里使用的字节数

#### ref 列

记录了在key列使用的索引查找值缩影的列或常量

#### rows 列

MySQL估计此次查询需要扫描的行数(并不准确，反映不了LIMIT字句)

#### filtered 列

显示WHERE字句或者联接条件的记录数的百分比

#### Extra 列

额外信息，常见值如下：

- Using index：覆盖索引，不需要回表
- Using where：在MySQL服务器层进行过滤
- Using temporary：对查询结果排序时会使用临时表
- Using filesort：对结果使用外部索引排序，而不是按索引次序从表里读取
- Range checked for each record (index map: N)：没有好用的索引，新的索引在联接的每一行重新估算