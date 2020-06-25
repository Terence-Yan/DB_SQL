#### 1.MySQL中的 IN()
在很多数据库系统中，IN()完全等同于多个 OR 条件的句子，因为这两者是完全等价的。在MySQL中这点是不成立的，MySQL将 IN() 列表中的数据先进行排序，
然后通过**二分查找**的方式来确定列表中的值是否满足条件，这是一个 O(log n)复杂度的操作，等价地转换成 OR 查询的复杂度为 O(n)，对于 IN() 列表中
有大量取值的时候，MySQL的处理速度将会更快。

#### 2.MySQL中的 IN() 与关联子查询
MySQL的子查询实现得非常糟糕。最糟糕的一类查询是 WHERE 条件中包含 IN() 的子查询语句，如：
```
  select * from table_a where id in(select id from table_b where column_x = 1);
```
因为MySQL对 IN() 列表中的选项有专门的优化策略，一般会认为MySQL会先执行子查询返回所有包含 column_x 为1的 id。一般来说，IN() 列表查询速度很快，
所以，我们会认为上面的查询会这样执行：
```
  -- select GROUP_CONCAT(id) from table_b where column_x = 1;
  -- result: 2,4,7,13,16,23,67,78,102,220,230,500
     select * from table_a where id IN(2,4,7,13,16,23,67,78,102,220,230,500);
```
很不幸，MySQL不是这样做的。MySQL会将相关的外层表压到子查询中，它认为这样可以更高效地查找到数据行：
```
  select * from table_a where id EXISTS(select id from table_b where column_x = 1 AND table_a.id = table_b.id);
```
通常可以采用以下方法进行优化：
* (1).使用函数 GROUP_CONCAT() 在 IN() 中构造一个由逗号分隔的列表；
* (2).使用 EXISTS() 等效的改写查询来获取更好的效率；
* (3).使用 JOIN 改写查询：
```
  select * from table_a 
     inner join table_b  USING(id) 
  where column_x = 1;
```
* 注：该限制直到 MySQL 5.5 都一直存在.
