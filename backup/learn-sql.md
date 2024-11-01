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
alter database `名称` character set 字符集 collate 排序规则
```
### 查
```sql
show databases;
select database();
use `库名`;
show create database `库名`\G;
```