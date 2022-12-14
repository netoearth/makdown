> 摘要: 无论在平时开发中还是面试中我们都会遇到一些MySQL的问题, 最近也在梳理一些MySQL的一些问题和整理了一些学习思维导图，希望对你有帮助, 也欢迎大家一起交流。 本文首发于公众号: `漫步coding`

### [#](https://manbucoding.com/travel-coding/mysql/MySQL%E6%9C%80%E6%96%B0%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%8A%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.html#mysql%E5%AD%A6%E4%B9%A0%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE) MySQL学习思维导图

> 该图以 Markdown 绘制思维导图的开源工具——markmap(https://markmap.js.org/repl)自动渲染出来的, 如果需要Markdown原稿(看的更加清晰), 关注公众号, 回复mysql 即可获得。

![](https://images.xiaozhuanlan.com/uploads/photo/2022/5c7947f4-8b66-4d2a-9a02-e630295dd425.png)

### [#](https://manbucoding.com/travel-coding/mysql/MySQL%E6%9C%80%E6%96%B0%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%8A%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.html#%E9%9D%A2%E8%AF%95%E4%B8%ADmysql%E4%B8%80%E4%BA%9B%E5%B8%B8%E8%A7%81%E7%9A%84%E9%97%AE%E9%A2%98) 面试中MySQL一些常见的问题

**1、CHAR、VARCHAR的区别是什么？**

VARCHAR类型用于存储可变长度字符串，是最常见的字符串数据类型。它比固定长度类型更节省空间，因为它仅使用必要的空间(根据实际字符串的长度改变存储空间)。

VARCHAR节省了存储空间，所以对性能也有帮助。但是，由于行是变长的，在UPDATE时可能使行变得比原来更长，这就导致需要做额外的工作。如果一个行占用的空间增长，并且在页内没有更多的空间可以存储，在这种情况下，不同的存储引擎的处理方式是不一样的。例如，MylSAM会将行拆成不同的片段存储，InnoDB则需要分裂页来使行可以放进页内。

CHAR类型用于存储固定长度字符串：MySQL总是根据定义的字符串长度分配足够的空间。当存储CHAR值时，MySQL会删除字符串中的末尾空格(在MySQL 4.1和更老版本中VARCHAR 也是这样实现的——也就是说这些版本中CHAR和VARCHAR在逻辑上是一样的，区别只是在存储格式上)。

同时，CHAR值会根据需要采用空格进行剩余空间填充，以方便比较和检索。但正因为其长度固定，所以会占据多余的空间，也是一种空间换时间的策略。

CHAR适合存储很短或长度近似的字符串。例如，CHAR非常适合存储密码的MD5值，因为这是一个定长的值。对于经常变更的数据，CHAR也比VARCHAR更好，因为定长的CHAR类型不容易产生碎片。对于非常短的列，CHAR比VARCHAR在存储空间上也更有效率。例如用CHAR(1)来存储只有Y和N的值，如果采用单字节字符集只需要一个字节，但是VARCHAR(1)却需要两个字节，因为还有一个记录长度的额外字节。

**2、TRUNCATE和DELETE的区别是什么？**

DELETE命令从一个表中删除某一行，或多行，TRUNCATE命令永久地从表中删除每一行。

**3、什么是触发器，MySQL中都有哪些触发器？**

触发器是指一段代码，当触发某个事件时，自动执行这些代码。在MySQL数据库中有如下六种触发器：1.Before Insert2.After Insert3.Before Update4.After Update5.Before Delete6.After Delete

**4、FLOAT和DOUBLE的区别是什么？**

-   FLOAT类型数据可以存储至多8位十进制数，并在内存中占4字节。
-   DOUBLE类型数据可以存储至多18位十进制数，并在内存中占8字节。

**5、如何在MySQL种获取当前日期？**

**6、如何查询第N高的分数？**

这里有几个注意点:

-   因为成绩可能有一样的值，所以使用DISTINCT进行去重
-   如果不存在第N高成绩的分数，那么查询应返回 null
-   把下方的N换成具体的数值查询

**7、请说明InnoDB和MyISAM的区别**

这个在面试过程中过的比较多。

-   InnoDB支持事务，MyISAM不支持；
-   InnoDB数据存储在共享表空间，MyISAM数据存储在文件中；
-   InnoDB支持行级锁，MyISAM只支持表锁；
-   InnoDB支持崩溃后的恢复，MyISAM不支持；
-   InnoDB支持外键，MyISAM不支持；
-   InnoDB不支持全文索引，MyISAM支持全文索引；

**8、innodb引擎的特性**

-   1、插入缓冲（insert buffer)
-   2、二次写(double write)
-   3、自适应哈希索引(ahi)4、预读(read ahead)

**9、请说明varchar和text的区别**

-   varchar可指定字符数，text不能指定，内部存储varchar是存入的实际字符数+1个字节（n<=255）或2个字节(n>255)，text是实际字符数+2个字节。
-   text类型不能有默认值。
-   varchar可直接创建索引，text创建索引要指定前多少个字符。
-   varchar查询速度快于text,在都创建索引的情况下，text的索引几乎不起作用。
-   查询text需要创建临时表。

**10、简单描述MySQL中，索引，主键，唯一索引，联合索引的区别，对数据库的性能有什么影响？**

这个在面试过程中过的比较多。

-   一个表只能有一个主键索引，但是可以有多个唯一索引。
-   主键索引一定是唯一索引，唯一索引不是主键索引。
-   主键可以与外键构成参照完整性约束，防止数据不一致。
-   联合索引：将多个列组合在一起创建索引，可以覆盖多个列。（也叫复合索引，组合索引）
-   外键索引：只有InnoDB类型的表才可以使用外键索引，保证数据的一致性、完整性、和实现级联操作（基本不用）。
-   全文索引：MySQL自带的全文索引只能用于MyISAM，并且只能对英文进行全文检索 （基本不用）

**11、创建MySQL联合索引应该注意什么？**

需遵循前缀原则

**12、列值为NULL时，查询是否会用到索引？**

在MySQL里NULL值的列也是走索引的。当然，如果计划对列进行索引，就要尽量避免把它设置为可空，MySQL难以优化引用了可空列的查询,它会使索引、索引统计和值更加复杂。

**13：以下语句是否会应用索引：SELECT FROM users WHERE YEAR(adddate) < 2019**

不会，因为只要列涉及到运算，MySQL就不会使用索引。

**14、MyISAM索引实现？**

MyISAM存储引擎使用B+Tree作为索引结构，叶节点的data域存放的是数据记录的地址。MyISAM的索引方式也叫做非聚簇索引的，之所以这么称呼是为了与InnoDB的聚簇索引区分。

**15、MyISAM索引与InnoDB索引的区别？**

-   InnoDB索引是聚簇索引，MyISAM索引是非聚簇索引。
-   InnoDB的主键索引的叶子节点存储着行数据，因此主键索引非常高效。
-   MyISAM索引的叶子节点存储的是行数据地址，需要再寻址一次才能得到数据。
-   InnoDB非主键索引的叶子节点存储的是主键和其他带索引的列数据，因此查询时做到覆盖索引会非常高效。

**16、MySQL的关联查询语句你会那些？**

几种关联查询

-   1.交叉连接（CROSS JOIN）
-   2.内连接（INNER JOIN）
-   3.外连接（LEFT JOIN/RIGHT JOIN）
-   4.联合查询（UNION与UNION ALL）
-   5.全连接（FULL JOIN）

平时用到比较多的是内连和外连， 以及联合查询

a)、内连接分为三类:

等值连接：ON A.id=B.id  
不等值连接：ON A.id > B.id  
自连接：SELECT \* FROM A T1 INNER JOIN A T2 ON T1.id=T2.pid

b)、外连接 分为: 左外连接、右外连接

左外连接：LEFT OUTER JOIN, 以左表为主，先查询出左表，按照ON后的关联条件匹配右表，没有匹配到的用NULL填充，可以简写成LEFT JOIN

右外连接：RIGHT OUTER JOIN, 以右表为主，先查询出右表，按照ON后的关联条件匹配左表，没有匹配到的用NULL填充，可以简写成RIGHT JOIN

c)、联合查询（UNION与UNION ALL）

就是把多个结果集集中在一起，UNION前的结果为基准，需要注意的是联合查询的列数要相等，相同的记录行会合并

从效率上说，UNION ALL 要比UNION快很多，所以，如果可以确认合并的两个结果集中不包含重复数据且不需要排序时的话，那么就使用UNION ALL。

d)、全连接（FULL JOIN）

1.MySQL不支持全连接 2.可以使用LEFT JOIN 和UNION和RIGHT JOIN联合使用

**17、UNION与UNION ALL的区别？**

如果使用UNION ALL，不会合并重复的记录行 效率 UNION 高于 UNION ALL

**18、如何优化慢SQL**

使用explain分析单条SQL语句

优化查询过程中的数据访问

-   访问数据太多导致查询性能下降
-   确定应用程序是否在检索大量超过需要的数据，可能是太多行或列
-   确认MySQL服务器是否在分析大量不必要的数据行
-   避免犯如下SQL语句错误
-   查询不需要的数据。解决办法：使用limit解决多表
-   关联返回全部列。解决办法：指定列名
-   总是返回全部列。解决办法：避免使用SELECT \*重复
-   查询相同的数据。解决办法：可以缓存数据，下次直接读取缓存

是否在扫描额外的记录。解决办法：使用explain进行分析，如果发现查询需要扫描大量的数据，但只返回少数的行，可以通过如下技巧去优化:

使用索引覆盖扫描，把所有的列都放到索引中，这样存储引擎不需要回表获取对应行就可以返回结果。  
改变数据库和表的结构，修改数据表范式  
重写SQL语句，让优化器可以以更优的方式执行查询。

**19、优化长难的查询语句**

一个复杂查询还是多个简单查询  
MySQL内部每秒能扫描内存中上百万行数据，相比之下，响应数据给客户端就要慢得多使用尽可能小的查询是好的，但是有时将一个大的查询分解为多个小的查询是很有必要的。  
切分查询: 将一个大的查询分为多个小的相同的查询  
一次性删除1000万的数据要比一次删除1万，暂停一会的方案更加损耗服务器开销。  
分解关联查询，让缓存的效率更高。  
执行单个查询可以减少锁的竞争。  
在应用层做关联更容易对数据库进行拆分。  
查询效率会有大幅提升。  
较少冗余记录的查询。

**20、优化特定类型的查询语句**

count(_)会忽略所有的列，直接统计所有列数，不要使用count(列名)  
MyISAM中，没有任何where条件的count(_)非常快。  
当有where条件时，MyISAM的count统计不一定比其它引擎快。  
可以使用explain查询近似值，用近似值替代count(\*)  
增加汇总表  
使用缓存

**21、优化关联查询**

确定ON或者USING子句中是否有索引。  
确保GROUP BY和ORDER BY只有一个表中的列，这样MySQL才有可能使用索引。

**22、优化子查询**

用关联查询替代  
优化GROUP BY和DISTINCT  
这两种查询据可以使用索引来优化，是最有效的优化方法  
关联查询中，使用标识列分组的效率更高  
如果不需要ORDER BY，进行GROUP BY时加ORDER BY NULL，MySQL不会再进行文件排序。  
WITH ROLLUP超级聚合，可以挪到应用程序处理

**23、优化LIMIT分页**

LIMIT偏移量大的时候，查询效率较低

可以记录上次查询的最大ID，下次查询时直接根据该ID来查询

**24、优化UNION查询**

UNION ALL的效率高于UNION

**25、优化WHERE子句**

解题方法对于此类考题，先说明如何定位低效SQL语句，然后根据SQL语句可能低效的原因做排查，先从索引着手，如果索引没有问题，考虑以上几个方面，数据访问的问题，长难查询句的问题还是一些特定类型优化的问题，逐一回答。

**26、乐观锁和悲观锁**

这个问题一般在面试中都会问到

悲观锁

总是假设最坏的情况，每次取数据时都认为其他线程会修改，所以都会加（悲观）锁。一旦加锁，不同线程同时执行时,只能有一个线程执行，其他的线程在入口处等待，直到锁被释放。

乐观锁

顾名思义就是在操作时很乐观，认为操作不会产生并发问题(不会有其他线程对数据进行修改)，因此不会上锁。但是在更新时会判断其他线程在这之前有没有对数据进行修改，一般会使用版本号机制或CAS(compare and swap)算法实现。

**小结**

后续， 还会继续更新MySQL相关的内容， 如果对您有帮助,可以收藏本文或者关注我的公众号: 漫步coding, 一起交流，一起学习。