
MySQL 数据库的使用
=================

## 1. 创建数据库

```mysql
CREATE DATABASE `mydb` CHARACTER SET utf8;
```

* 语法：

```mysql
CREATE DATABASE [IF NOT EXISTS] db_name
    [create_specification [, create_specification] ...]

create_specification:
    [DEFAULT] CHARACTER SET charset_name
  | [DEFAULT] COLLATE collation_name
```

## 2. 使用数据库

```mysql
USE `mydb`;
```

* 语法：

```mysql
USE db_name
```

## 3. 表

#### 3.1. 创建表

```mysql
CREATE TABLE `mydb`.`mytab1` (
  `id` varchar(36) NOT NULL COMMENT 'ID',
  `tab2_id` varchar(36) NOT NULL COMMENT '表2的ID',
  `name` varchar(40) UNIQUE NOT NULL COMMENT '名称',
  `time` datetime NULL DEFAULT NOW() COMMENT '时间',
  `timestamp` timestamp NULL DEFAULT NOW() COMMENT '时间戳',
  PRIMARY KEY (`id`),
  FOREIGN KEY (`tab2_id`) REFERENCES `mydb`.`mytab2`(`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='我的表1';
```

* 语法：

```mysql
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    [(create_definition,...)]
    [table_options] [select_statement]

Or: 

CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    [(] LIKE old_tbl_name [)];

create_definition:
    column_definition
  | [CONSTRAINT [symbol]] PRIMARY KEY [index_type] (index_col_name,...)
  | KEY [index_name] [index_type] (index_col_name,...)
  | INDEX [index_name] [index_type] (index_col_name,...)
  | [CONSTRAINT [symbol]] UNIQUE [INDEX]
        [index_name] [index_type] (index_col_name,...)
  | [FULLTEXT|SPATIAL] [INDEX] [index_name] (index_col_name,...)
  | [CONSTRAINT [symbol]] FOREIGN KEY
        [index_name] (index_col_name,...) [reference_definition]
  | CHECK (expr)

column_definition:
    col_name type [NOT NULL | NULL] [DEFAULT default_value]
        [AUTO_INCREMENT] [[PRIMARY] KEY] [COMMENT 'string']
        [reference_definition]

type:
    TINYINT[(length)] [UNSIGNED] [ZEROFILL]
  | SMALLINT[(length)] [UNSIGNED] [ZEROFILL]
  | MEDIUMINT[(length)] [UNSIGNED] [ZEROFILL]
  | INT[(length)] [UNSIGNED] [ZEROFILL]
  | INTEGER[(length)] [UNSIGNED] [ZEROFILL]
  | BIGINT[(length)] [UNSIGNED] [ZEROFILL]
  | REAL[(length,decimals)] [UNSIGNED] [ZEROFILL]
  | DOUBLE[(length,decimals)] [UNSIGNED] [ZEROFILL]
  | FLOAT[(length,decimals)] [UNSIGNED] [ZEROFILL]
  | DECIMAL(length,decimals) [UNSIGNED] [ZEROFILL]
  | NUMERIC(length,decimals) [UNSIGNED] [ZEROFILL]
  | DATE
  | TIME
  | TIMESTAMP
  | DATETIME
  | CHAR(length) [BINARY | ASCII | UNICODE]
  | VARCHAR(length) [BINARY]
  | TINYBLOB
  | BLOB
  | MEDIUMBLOB
  | LONGBLOB
  | TINYTEXT
  | TEXT
  | MEDIUMTEXT
  | LONGTEXT
  | ENUM(value1,value2,value3,...)
  | SET(value1,value2,value3,...)
  | spatial_type

index_col_name:
    col_name [(length)] [ASC | DESC]

reference_definition:
    REFERENCES tbl_name [(index_col_name,...)]
               [MATCH FULL | MATCH PARTIAL]
               [ON DELETE reference_option]
               [ON UPDATE reference_option]

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT

table_options: table_option [table_option] ...

table_option:
    {ENGINE|TYPE} = {BDB|HEAP|ISAM|InnoDB|MERGE|MRG_MYISAM|MYISAM}
  | AUTO_INCREMENT = value
  | AVG_ROW_LENGTH = value
  | CHECKSUM = {0 | 1}
  | COMMENT = 'string'
  | MAX_ROWS = value
  | MIN_ROWS = value
  | PACK_KEYS = {0 | 1 | DEFAULT}
  | PASSWORD = 'string'
  | DELAY_KEY_WRITE = {0 | 1}
  | ROW_FORMAT = { DEFAULT | DYNAMIC | FIXED | COMPRESSED }
  | RAID_TYPE = { 1 | STRIPED | RAID0 }
        RAID_CHUNKS = value
        RAID_CHUNKSIZE = value
  | UNION = (tbl_name[,tbl_name]...)
  | INSERT_METHOD = { NO | FIRST | LAST }
  | DATA DIRECTORY = 'absolute path to directory'
  | INDEX DIRECTORY = 'absolute path to directory'
  | [DEFAULT] CHARACTER SET charset_name [COLLATE collation_name]

select_statement:
    [IGNORE | REPLACE] [AS] SELECT ...   (Some legal select statement)
```

#### 3.2. 修改表结构

```mysql
ALTER TABLE `mydb`.`mytab1` RENAME TO `mytab1_new`;
ALTER TABLE `mydb`.`mytab1` MODIFY COLUMN `name` varchar(40) UNIQUE NOT NULL COMMENT '名称';
```

* 语法：

```mysql
ALTER [IGNORE] TABLE tbl_name
    alter_specification [, alter_specification] ...

alter_specification:
    ADD [COLUMN] column_definition [FIRST | AFTER col_name ]
  | ADD [COLUMN] (column_definition,...)
  | ADD INDEX [index_name] [index_type] (index_col_name,...)
  | ADD [CONSTRAINT [symbol]]
        PRIMARY KEY [index_type] (index_col_name,...)
  | ADD [CONSTRAINT [symbol]]
        UNIQUE [index_name] [index_type] (index_col_name,...)
  | ADD [FULLTEXT|SPATIAL] [index_name] (index_col_name,...)
  | ADD [CONSTRAINT [symbol]]
        FOREIGN KEY [index_name] (index_col_name,...)
        [reference_definition]
  | ALTER [COLUMN] col_name {SET DEFAULT literal | DROP DEFAULT}
  | CHANGE [COLUMN] old_col_name column_definition
        [FIRST|AFTER col_name]
  | MODIFY [COLUMN] column_definition [FIRST | AFTER col_name]
  | DROP [COLUMN] col_name
  | DROP PRIMARY KEY
  | DROP INDEX index_name
  | DROP FOREIGN KEY fk_symbol
  | DISABLE KEYS
  | ENABLE KEYS
  | RENAME [TO] new_tbl_name
  | ORDER BY col_name
  | CONVERT TO CHARACTER SET charset_name [COLLATE collation_name]
  | [DEFAULT] CHARACTER SET charset_name [COLLATE collation_name]
  | DISCARD TABLESPACE
  | IMPORT TABLESPACE
  | table_options
```

#### 3.3. 删除表

```mysql
DROP TABLE IF EXISTS `mydb`.`mytab1`;
```

* 语法：

```mysql
DROP [TEMPORARY] TABLE [IF EXISTS]
    tbl_name [, tbl_name] ...
    [RESTRICT | CASCADE]
```

#### 3.4. 查询表结构

```mysql
DESCRIBE `mydb`.`mytab1`;
```

* 语法：

```mysql
{DESCRIBE | DESC} tbl_name [col_name | wild]
```

#### 3.5. 新增数据

```mysql
LOCK TABLES `mydb`.`mytab1` WRITE;

INSERT INTO `mydb`.`mytab1`
(`id`,`tab2_id`,`name`,`time`,`timestamp`)
VALUES
('d4978f8b-8915-4366-abcb-2fbbd625e388','15477a35-307e-431c-ac28-5f187d0145c3','data1',NOW(),NOW()),
('a432cb60-f7b9-4c1c-8131-e25e219d994b','15477a35-307e-431c-ac28-5f187d0145c3','data2',NOW(),NOW());

UNLOCK TABLES;
```

* 语法：

```mysql
INSERT [LOW_PRIORITY | DELAYED] [IGNORE]
    [INTO] tbl_name [(col_name,...)]
    VALUES ({expr | DEFAULT},...),(...),...
    [ ON DUPLICATE KEY UPDATE col_name=expr, ... ]

Or: 

INSERT [LOW_PRIORITY | DELAYED] [IGNORE]
    [INTO] tbl_name
    SET col_name={expr | DEFAULT}, ...
    [ ON DUPLICATE KEY UPDATE col_name=expr, ... ]

Or: 

INSERT [LOW_PRIORITY | DELAYED] [IGNORE]
    [INTO] tbl_name [(col_name,...)]
    SELECT ...
```

#### 3.6. 修改数据

```mysql
LOCK TABLES `mydb`.`mytab1` WRITE;

UPDATE `mydb`.`mytab1` t SET t.`name`='data1_new' WHERE t.`id`='d4978f8b-8915-4366-abcb-2fbbd625e388';

UNLOCK TABLES;
```

* 语法：

```mysql
Single-table syntax: 

UPDATE [LOW_PRIORITY] [IGNORE] tbl_name
    SET col_name1=expr1 [, col_name2=expr2 ...]
    [WHERE where_definition]
    [ORDER BY ...]
    [LIMIT row_count]

Multiple-table syntax: 

UPDATE [LOW_PRIORITY] [IGNORE] tbl_name [, tbl_name ...]
    SET col_name1=expr1 [, col_name2=expr2 ...]
    [WHERE where_definition]
```

#### 3.7. 删除数据

```mysql
LOCK TABLES `mydb`.`mytab1` WRITE;

DELETE t FROM `mydb`.`mytab1` t WHERE t.`id`='d4978f8b-8915-4366-abcb-2fbbd625e388';

UNLOCK TABLES;
```

* 语法：

```mysql
Single-table syntax: 

DELETE [LOW_PRIORITY] [QUICK] [IGNORE] FROM tbl_name
       [WHERE where_definition]
       [ORDER BY ...]
       [LIMIT row_count]

Multiple-table syntax: 

DELETE [LOW_PRIORITY] [QUICK] [IGNORE]
       tbl_name[.*] [, tbl_name[.*] ...]
       FROM table_references
       [WHERE where_definition]

Or: 

DELETE [LOW_PRIORITY] [QUICK] [IGNORE]
       FROM tbl_name[.*] [, tbl_name[.*] ...]
       USING table_references
       [WHERE where_definition]
```

#### 3.8. 查询数据

```mysql
LOCK TABLES `mydb`.`mytab1` READ;

SELECT * FROM `mydb`.`mytab1`;

UNLOCK TABLES;
```

* 语法：

```mysql
SELECT
    [ALL | DISTINCT | DISTINCTROW ]
      [HIGH_PRIORITY]
      [STRAIGHT_JOIN]
      [SQL_SMALL_RESULT] [SQL_BIG_RESULT] [SQL_BUFFER_RESULT]
      [SQL_CACHE | SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS]
    select_expr, ...
    [INTO OUTFILE 'file_name' export_options
      | INTO DUMPFILE 'file_name']
    [FROM table_references
      [WHERE where_definition]
      [GROUP BY {col_name | expr | position}
        [ASC | DESC], ... [WITH ROLLUP]]
      [HAVING where_definition]
      [ORDER BY {col_name | expr | position}
        [ASC | DESC] , ...]
      [LIMIT {[offset,] row_count | row_count OFFSET offset}]
      [PROCEDURE procedure_name(argument_list)]
      [FOR UPDATE | LOCK IN SHARE MODE]]
```

##### JOIN 关联查询

> 外联

> > 左外联
    
> > 右外联
    
> 内联

```mysql
```

* 语法：

```mysql
table_reference, table_reference
table_reference [INNER | CROSS] JOIN table_reference [join_condition]
table_reference STRAIGHT_JOIN table_reference
table_reference LEFT [OUTER] JOIN table_reference [join_condition]
table_reference NATURAL [LEFT [OUTER]] JOIN table_reference
{ OJ table_reference LEFT OUTER JOIN table_reference
    ON conditional_expr }
table_reference RIGHT [OUTER] JOIN table_reference [join_condition]
table_reference NATURAL [RIGHT [OUTER]] JOIN table_reference

table_reference is defined as: 


tbl_name [[AS] alias]
    [[USE INDEX (key_list)]
      | [IGNORE INDEX (key_list)]
      | [FORCE INDEX (key_list)]]

join_condition is defined as: 

ON conditional_expr | USING (column_list)
```

##### UNION 联合查询

```mysql
SELECT name FROM `mydb`.`mytab1`
UNION
SELECT name FROM `mydb`.`mytab2`
```

* 语法：

```mysql
SELECT ...
UNION [ALL | DISTINCT]
SELECT ...
  [UNION [ALL | DISTINCT]
   SELECT ...]
```

## 4. 索引

#### 4.1. 创建索引

```mysql
CREATE INDEX `mydb`.`ind_name`
    ON `mydb`.`mytab2` (`name` ASC);
```

* 语法：

```mysql
CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX index_name [index_type]
    ON tbl_name (index_col_name,...)

index_type:
    [BTREE | FULLTEXT | HASH | RTREE]

index_col_name:
    col_name [(length)] [ASC | DESC]
```

## 5. 用户

#### 5.1. 创建用户

```mysql
CREATE USER 'myuser'@'%' IDENTIFIED BY PASSWORD '123456';
```

* 语法：

```mysql
CREATE USER user IDENTIFIED BY [PASSWORD] 'password';
```

#### 5.2. 修改密码

```mysql
SET PASSWORD FOR 'myuser'@'%' = PASSWORD('123456');
```

* 语法：

```mysql
SET PASSWORD = PASSWORD('some password')
SET PASSWORD FOR user = PASSWORD('some password')
```

#### 5.3. 权限管理

##### 授权

```mysql
```

* 语法：

```mysql
GRANT priv_type [(column_list)] [, priv_type [(column_list)]] ...
    ON {tbl_name | * | *.* | db_name.*}
    TO user [IDENTIFIED BY [PASSWORD] 'password']
        [, user [IDENTIFIED BY [PASSWORD] 'password']] ...
    [REQUIRE
        NONE |
        [{SSL| X509}]
        [CIPHER 'cipher' [AND]]
        [ISSUER 'issuer' [AND]]
        [SUBJECT 'subject']]
    [WITH [GRANT OPTION | MAX_QUERIES_PER_HOUR count |
                          MAX_UPDATES_PER_HOUR count |
                          MAX_CONNECTIONS_PER_HOUR count]]
```

##### 撤销权限

```mysql
```

* 语法：

```mysql
REVOKE priv_type [(column_list)] [, priv_type [(column_list)]] ...
    ON {tbl_name | * | *.* | db_name.*}
    FROM user [, user] ...
```

##### 权限类别 priv_type

```
ALL [PRIVILEGES]  Sets all simple privileges except GRANT OPTION
ALTER  Allows use of ALTER TABLE
CREATE  Allows use of CREATE TABLE
CREATE TEMPORARY TABLES  Allows use of CREATE TEMPORARY TABLE
DELETE  Allows use of DELETE
DROP  Allows use of DROP TABLE
EXECUTE  Allows the user to run stored procedures (MySQL 5.0)
FILE  Allows use of SELECT ... INTO OUTFILE and LOAD DATA INFILE
INDEX  Allows use of CREATE INDEX and DROP INDEX
INSERT  Allows use of INSERT
LOCK TABLES  Allows use of LOCK TABLES on tables for which you have the SELECT privilege
PROCESS  Allows use of SHOW FULL PROCESSLIST
REFERENCES  Not yet implemented
RELOAD  Allows use of FLUSH
REPLICATION CLIENT  Allows the user to ask where the slave or master servers are
REPLICATION SLAVE  Needed for replication slaves (to read binary log events from the master)
SELECT  Allows use of SELECT
SHOW DATABASES  SHOW DATABASES shows all databases
SHUTDOWN  Allows use of mysqladmin shutdown
SUPER  Allows use of CHANGE MASTER, KILL, PURGE MASTER LOGS, and SET GLOBAL statements, the mysqladmin debug command; allows you to connect (once) even if max_connections is reached
UPDATE  Allows use of UPDATE
USAGE  Synonym for ``no privileges''
GRANT OPTION  Allows privileges to be granted
```
