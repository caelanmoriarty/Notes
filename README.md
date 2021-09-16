# Notes
## Task01
* 数据库系统与数据库
 ![Alt pic](https://github.com/caelanmoriarty/Notes/blob/gh-pages/O1CN01kROUDI22ITX6Evayf_!!6000000007097-0-tps-567-333.jpg?raw=true)
* 表：一种结构化文件，可用来存储某种特定类型的数据。
* 列：储存表中某部分的信息。
* 行：数据是按行储存的
* 主键：表中的每一行应该都有一列或几列可以唯一标识自己
* 数据类型：\
1.integer \
2.char 存储定长字符串 \
3.varchar 存储可变长度字符串，不会浪费存储空间 \
4.date 存储日期型数据
### 基本操作
1.创建数据库 
```javascript
CREATE DATABASE < 数据库名称 > ; 
```
2.创建表 
```javascript
CREATE TABLE < 表名 > 
( < 列名 1> < 数据类型 > < 该列所需约束 > , 
  < 列名 2> < 数据类型 > < 该列所需约束 > , 
  < 列名 3> < 数据类型 > < 该列所需约束 > , 
  < 列名 4> < 数据类型 > < 该列所需约束 > ,
  .
  .
  .
  < 该表的约束 1> , < 该表的约束 2> ,……);
```
练习1.1 
```javascript
create database shop;
create table addressbook(
	regist_no integer not null,
    name varchar(128) not null,
    address varchar(256) not null,
    tel_no char(10),
    mail_address char(20),
    primary key(rigist_no)
    );
```
3.表的删除和更新 
* 删除
 ```javascript
 DROP TABLE < 表名 > ; //删除 
 ALTER TABLE < 表名 > ADD COLUMN < 列的定义 >;//添加列的alter table语句 
 ALTER TABLE < 表名 > DROP COLUMN < 列名 >; //删除列的alter table语句 
 TRUNCATE TABLE TABLE_NAME; //清空表的内容 
 ```
 * 更新
 ```javascript
 UPDATE <表名>
SET <列名> = <表达式> [, <列名2>=<表达式2>...];  
WHERE <条件>;  -- 可选，非常重要。
ORDER BY 子句;  --可选
LIMIT 子句; --可选
```
练习1.2
```javascript
ALTER TABLE addressbook ADD COLUMN postal_code CHAR(8) not null;
```
4.向表中插入数据 
```javascript
INSERT INTO <表名> (列1, 列2, 列3, ……) VALUES (值1, 值2, 值3, ……); 
```
很多 RDBMS 都支持一次插入多行数据。
```javascript
INSERT INTO productins VALUES ('0002', '打孔器', '办公用品', 500, 320, '2009-09-11'),
                              ('0003', '运动T恤', '衣服', 4000, 2800, NULL),```
                              ('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20');  
 ```
 练习1.3
 ```javascript
 DROP TABLE addressbook;
 ```
 练习1.4 \
 drop掉的表无法恢复只能重新插入 再create一个
 
 
 ## Task02
 动手操作1：
 ![Alt pic](https://github.com/caelanmoriarty/Notes/blob/gh-pages/....PNG）
 ### select 语句
 
