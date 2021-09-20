# Notes
## Task01
* 数据库系统与数据库
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
 动手操作1：\
 ![Alt pic](https://github.com/caelanmoriarty/Notes/blob/7300a29b9710dfdcc53e9f6f63c87edbabf87ed9/....PNG?raw=ture)
 ### select 语句
  ```javascript
SELECT prod_name
FROM Products;
 ```
 ps.练习如图（好像上传不上来我好无语(ˉ▽ˉ；)...），表和里面insert进去的数据我都是用的第一节里面的product
 * 检索所有列
```javascript
SELECT *
FROM Products
```
  *为通配符
  * 检索出不同的值
 ```javascript
SELECT DISTINCT vend_id
FROM Products;
```
* filter condition/search criteria
```javascript
SELECT <列名>, ……
  FROM <表名>
 WHERE <条件表达式>;
 ```
![Aaron Swartz](https://github.com/caelanmoriarty/Notes/raw/gh-pages/O1CN01kROUDI22ITX6Evayf_!!6000000007097-0-tps-567-333.jpg)
ps.还有加限制条件的比如只检索前四行用top 4 但是我试了好像不行，没这个关键词...是因为不是server或access而是workbench的原因吗？好像不同的DBMS用的不同？哪为路过大佬给我讲讲
* 注释
分为1行注释"-- "和多行注释两种"/* */"。
```javascript
/* SELECT prod_name, vend_id
FROM Products; */
SELECT prod_name
FROM Products;
```
 or 
```javascript
SELECT prod_name--这是一条注释
FROM Products
```
* 一些运算符
1. NOT 
```javascript
SELECT product_name, product_type, sale_price
  FROM product
 WHERE NOT sale_price >= 1000;
```
2.AND  OR \
**AND 运算符优先于 OR 运算符**\
**需要加括号**
```javascript
SELECT product_name, product_type, regist_date
  FROM product
 WHERE product_type = '办公用品'
   AND ( regist_date = '2009-09-11'
        OR regist_date = '2009-09-20');
```
练习题
**2.1**
```
SELECT product_name, regist_date
  FROM product
 WHERE regist_date>'2009-04-28';
```
**2.2** 
![Aaron Swartz](https://github.com/caelanmoriarty/Notes/raw/gh-pages/pp.JPG)\
**2.3**
```
SELECT product_name,product_type,sale_price,purchase_price
  FROM product
 WHERE sale_price-500>=purchase_price
 ```
 **2.4**
 ```
 select product_name,product_type,sale_price*0.9-purchase_price as profit
from product
where sale_price*0.9 -purchase_price>100 and ( product_type='办公用品'or product_type='厨房用品');
 ```
 ### 对表进行聚合查询
 * 聚集函数 aggregate function
我们经常需要**汇总数据**而不用把它们实际检索出来，为此SQL提供了专门的函数。\
![Aaron Swartz](https://github.com/caelanmoriarty/Notes/raw/gh-pages/function.JPG)\
![Aaron Swartz](https://github.com/caelanmoriarty/Notes/raw/gh-pages/cout.JPG)\
* 数据分组
使用分组可以将数据分为多个逻辑组，对每个组进行聚集计算。其中前三项用于筛选数据，GROUP BY对筛选出的数据进行处理，书写顺序有严格要求
```
SELECT <列名1>,<列名2>, <列名3>, ……
  FROM <表名>
 GROUP BY <列名1>, <列名2>, <列名3>, ……;
```
* 排序数据/
有严格的顺序，同GROUP BY
```
SELECT prod_name
FROM Product
ORDER BY prod_name;
```
实操：
```
SELECT product_id,sale_price,product_name
FROM Product
ORDER BY sale_price,product_name;
```
第一遍的时候把sale_price写后面了看着价格怎么不是顺序的然后换过来就ok了。仅在多个行具有相同的price值时才对产品按prod_name进行排序。如果price列中所有的值都是唯一的，则不会按prod_name排序。
```
SELECT prod_id, sale_price, prod_name
FROM Product
ORDER BY 2, 3;
```
这样就是先按第二列排序再按第三列排序。可以混合使用实际列名和相对列位置。/
默认为升序排列，降序排列为DESC
```
SELECT product_id, sale_price, product_name
FROM Product
ORDER BY sale_price DESC;
```
如果想进行多个排序则
```
SELECT prod_id, sale_price, prod_name
FROM Product
ORDER BY sale_price DESC, prod_name;
```
price列降序，name列升序\
**PS：GROUP BY中列名不能使用别名，ODER BY 中列名可以使用别名**\
练习题2.5 \
sum只能用于数值型；书写顺序错误\
2.6
```
SELECT product_type,SUM(sale_price),SUM(purchase_price)
from product
group by product_type
having sum(sale_price)>sum(purchase_price)*1.5;
```
## Task03  
## SQL函数
**不可移植性**
* 数值处理函数 ABS MOD EXP ROUND
* 文本处理函数 lower length concat replace substring upper lower left rtrim
* 日期函数 current_date current_time current_timestamp extract
* 转换函数 CAST COALESCE

均已进行实操
## 谓词
下午补完这部分。。。TT







## 子查询
任何sql语句都是查询，但查询一般指select语句。\
子查询：嵌套在其他查询中的查询
```
SELECT product_type, cnt_product
 FROM (SELECT *
	 FROM (SELECT product_type,COUNT(*) AS cnt_product
 		GROUP BY product_type) AS productsum
			WHERE cnt_product = 4) AS productsum2;
```
看到有用IN子句进行嵌套的，运行了一下，觉得用IN子句的比较好理解\
PS 作为子查询的SELECT语句只能查询单个列
* 标量子查询
返回单一值的子查询。因此，标量子查询的返回值可以用在=或者<>这样需要单一值的比较运算符之中。\
PS where子句后不能使用聚合函数，但可以使用标量子查询。
```
SELECT product_id, product_name, sale_price
  FROM product
 WHERE sale_price > (SELECT AVG(sale_price) FROM product);
 ```
* 关联子查询
通过一些标志将内外两层的查询连接起来起到过滤数据的目的\
**关联子查询的执行逻辑和通常的SELECT语句的执行逻辑完成不一样**\
*SELECT*\
书写顺序：SELECT》FROM 》WHERE》GROUP BY》HAVE》ORDER BY \
执行顺序：FROM 》WHERE》GROUP BY》HAVE》SELECT》ORDER BY \
*关联子查询*\
1）先从主查询的Product表中product _type列取出第一个值，进入子查询中，得到子查询结果，然后返回父查询，判断父查询的where子句条件，则返回整个语句的第1条结果。\
2）重复上述操作，直到所有主查询中的Product表中product _type列记录取完为止。得出整个语句的结果集，就是最后的答案。\
。。。。。有待理解。。。。


### 视图
视图：一个虚拟的表，不同于直接操作数据表，视图是依据 SELECT 语句来创建的。视图中存放的是sql查询语句（select语句）。使用视图时，会运行视图里的sql查询语句创建出一张临时表。
```
create view 视图名称(<视图列名1>,<视图列名2>,...)
as 
<select 查询语句>;
```
* 基于单表的视图\
如下，基于product的视图
```
CREATE VIEW productsum (product_type, cnt_product)
AS
SELECT product_type, COUNT(*)
  FROM product
 GROUP BY product_type ;
```
* 基于多表的视图
```
CREATE VIEW view_shop_product(product_type, sale_price, shop_name)
AS
SELECT product_type, sale_price, shop_name
  FROM product,
       shop_product
 WHERE product.product_id = shop_product.product_id;
```
 * 在视图的基础上进行查询
```
SELECT sale_price, shop_name
  FROM view_shop_product
 WHERE product_type = '衣服';
```
 * 修改视图结构
```
ALTER VIEW <视图名> AS <SELECT语句>
```
 * 更新视图内容
```
UPDATE productsum
   SET sale_price = '5000'
 WHERE product_type = '办公用品';
 ```
**限制条件**
即在限制条件下不能更新视图\
1.聚合函数\
2.DISTINCT\
3.HAVING\
4.UNION\
5.FROM子句中包含多个表\
PS 尽量不要通过视图来修改表 ！！！
* 删除视图
```
DROP VIEW <视图名1> [ , <视图名2> …]
 ```
 练习4.1
 ```
 Create view viewpractice5_1 
	AS
    select product_name,sale_price,regist_date
    from product
    where sale_price>=1000
    AND regist_date='2009-09-20'
 ```  
 4.2\
 盲猜会报错\
 4.3
 ```  
 select product_id,product_name,product_type,sale_price,
(select avg(sale_price)from product)as sale_price_all
from product
```  
4.4\
其实我不懂，但这个题下面提示说关联子查询...（关联子查询就没学明白呢还
```  
create view avgpricebytype as
select product_id,product_name,product_type,sale_price,
(select avg(sale_price)from product p2 
where p1.product_type=p2.product_type
group by product_type)as avg_sale_price
from product p1
```  






















 
