#### 1.MySQL存储引擎概述
**插件式存储引擎**是MySQL数据库最重要的特性之一，用户可以根据应用的需要选择**如何存储和索引数据、是否使用事务**等。MySQL默认支持多种存储引擎，以适
用于不同领域的数据库应用需要，用户可以通过选择使用不同的存储引擎提供应用的效率，提供灵活的存储，用户甚至可以按照自己的需要定制和使用自己的存储引擎，
以实现最大程度的可定制性。

#### 2.MySQL支持的存储引擎
MySQL5.0支持的存储引擎包括**MyISAM、InnoDB、BDB、MEMORY、MERGE、EXAMPLE、NDB Cluster、ARCHIVE、CSV、BLACKHOLE、FEDERATED**等，其中InnoDB和
BDB提供**事务安全表**，其他存储引擎都是**非事务安全表**。

#### 3.MySQL的默认存储引擎
创建新表时如果不指定存储引擎，那么系统就会使用**默认存储引擎**，MySQL5.5之前的默认存储引擎是MyISAM，5.5之后改为了InnoDB。如果要修改默认的存储引擎，
可以在参数文件中设置default-table-type。

#### 4.查看当前的默认存储引擎：show variables like 'default_storage_engine';

#### 5.查看当前数据库支持的存储引擎：show engines;


