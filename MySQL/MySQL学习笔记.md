#### 1.left/right join 与 左右表
```
示例sql: select * from table1 left join table2 on table1.id=table2.id
1).如何区分join语句中的左右表？
左右表是以join为中心来分类的，若表位于join关键字的左边，就被称为左表，位于右边，就称为右表。如上例中，table1是左表，table2是右表。
2).left/right join语句的结果集如何判断？
出现哪一个位置关键字(left/right，如left)，则对应的表(即左表)就是“主表”，即结果集包含它的所有行，另外一个表则匹配包含，即满足条件的行会被包含
在结果集中，左表中的行在右表中匹配不上的，则右表中所有目标字段用NULL填充。
```

#### 2.什么是视图(View)
视图是一种虚拟存在的表。或者说是一个被延迟加载的通过select方式获取的封装好的且可以被引用的数据结果集。
