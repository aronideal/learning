
MySQL
=====

## 1. 脚本语法

#### 1.1. 创建数据库

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
    [create_specification [, create_specification] ...]

create_specification:
    [DEFAULT] CHARACTER SET charset_name
  | [DEFAULT] COLLATE collation_name
```

* 举例：

```mysql
CREATE DATABASE mydb CHARACTER SET utf8;
```

#### 1.2. 使用数据库

```sql
USE db_name
```

* 举例：

```sql
USE mydb;
```
