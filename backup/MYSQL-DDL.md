## 库管理

### 创建
```sql
# 创建
CREATE DATABASE `数据库名`;
CREATE DATABASE IF NOT EXISTS `数据库名`;

# 指定字符集
CREATE DATABASE IF NOT EXISTS `数据库名` CHARACTER SET 字符集 COLLATE 排序规则;

## utf8mb4_0900_ai_ci 不区分大小写
## utf8mb4_0900_as_cs 区分大小写

# 查看数据库字符集和排序规则
SHOW VARIABLES LIKE 'character_set_database';
SHOW VARIABLES LIKE 'collation_database';
```

### 查询
```sql
# 查看当前所有数据库
SHOW DATABASES;

# 查看当前使用库
SELECT DATABASE();

# 查看指定库所有表
SHOW TABLES FROM `数据库名`;

# 切换/选中库
USE 数据库名;
```

### 修改
```sql
# 修改数据库字符集排序规则
ALTER DATABASE `数据库名` CHARACTER SET 字符集 COLLATE 排序规则;
```

### 删除（慎用）
```sql
DROP DATABASE `数据库名`;
DROP DATABASE IF EXISTS `数据库名`;
```

##  表管理

### 创建
```sql
CREATE TABLE IF NOT EXISTS `表名` (
  列名 类型 [列可选约束] [COMMENT `列可选注释`],
  列名 类型 [列可选约束] [COMMENT `列可选注释`]
) [表可选约束] [COMMENT `表可选注释`];
```

### 查询
```sql
# 查看表定义
DESC `表名`;
# 查看创建表语句
SHOW CREATE TABLE `表名` /G;
```

### 修改
```sql
# 添加列
ALTER TABLE `表名` ADD `列名` 类型 [列可选约束] [FIRST|AFTER <col_name>];
# 删除列
ALTER TABLE `表名` DROP `列名`;
# 修改列名
ALTER TABLE `表名` CHANGE `列名` `新列名` [FIRST|AFTER <col_name>];
# 修改列类型
ALTER TABLE `表名` MODIFY `列名` 类型 [列可选约束] [FIRST|AFTER <col_name>];
# 修改表名
ALTER TABLE `表名` RENAME `新表名`;
```

### 删除（慎用）
```sql
DROP TABLE IF EXISTS `表名`;
```