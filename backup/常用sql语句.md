## 库操作
### 增
```sql
create database `名称`;
create database if not exists `名称`;
create database if not exists `名称` character set 字符集 collate 排序规则;
```
### 删
```sql
drop database `名称`;
drop database if exists `名称`;
```
### 改
```sql
alter database `名称` character set 字符集 collate 排序规则;
```
### 查
```sql
show databases;
show tables from `库名`;
use `库名`;
select database();
show create database `库名`\G;
```

## 表操作
### 增
```sql
create table if not exists `表名` (
  列名 列类型 [列可选约束] [comment `列可选注释`],
  列名 列类型 [列可选约束] [comment `列可选注释`]
) [表可选约束] [comment `表可选注释`];
```
### 删
```sql
drop table if exists `表名`;
```
### 改
```sql
# 修改表名
alter table `表名` rename `新表名`;
# 新增列
alter table `表名` add `列名` 列类型 [列可选约束] [first | after 列名] [comment 列可选注释];
# 删除列
alter table `表名` drop `列名`;
# 改列名
alter table `表名` change `列名` `新列名` [first | after 列名];
# 改列类型
alter table `表名` modify 列类型 [列可选约束] [first | after 列名];
```
### 查
```sql
desc `表名`;
show create table `表名`\G;
```

## 表数据操作
### 增
```sql
insert into `表名` (列名1, 列名2, 列名3) values
  (列1值, 列2值, 列3值),
  (列1值, 列2值, 列3值),
  (列1值, 列2值, 列3值);
```
### 删
```sql
delete from `表名` where 条件; # 省略 where 条件 将会删除表中所有数据
```
### 改
```sql
update `表名` set 列名1 = 列值1, 列名2 = 列值2 where 条件; # 省略 where 条件 将会更新表中所有数据
```
### 查
```sql
# 简单查询
select * from `表名`;
select 列名1, 列名2 from `表名` [可选条件];
```