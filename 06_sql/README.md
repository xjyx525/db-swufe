# 本周作业（第5次作业）
考虑关系模式`product(product_no, name, price)`，完成下面的题目：

## 题目一（1分+2分）
在数据库中创建该关系，并自建上面关系的txt数据文件：
txt数据文件地址'C:\Users\Xu\Desktop\product_data.txt'
CREATE TABLE product (
    product_no VARCHAR(50) PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2) NOT NULL
);

1.使用COPY命令导入数据库（PostgreSQL）；或使用LOAD DATA命令导入数据库（MySQL）。
COPY product FROM 'C:\Users\Xu\Desktop\product_data.txt' 
WITH DELIMITER '|' CSV HEADER;

2.将该关系导出为任意文件（如SQL、Txt、CSV、JSON等）。
COPY product TO 'C:\Users\Xu\Desktop\product_export.csv' 
WITH CSV HEADER;

## 题目二（12分）
1.添加一个新的商品，编号为666，名字为cake，价格不详。
INSERT INTO product (product_no, name, price) 
VALUES ('666', 'cake', NULL);

2.使用一条SQL语句同时添加3个商品，内容自拟。
INSERT INTO product (product_no, name, price) VALUES
('777', '巧克力', 15.00),
('888', '牛奶', 2.50),
('999', '面包', 8.80);

3.将商品价格统一打8折。
UPDATE product 
SET price = price * 0.8 
WHERE price IS NOT NULL;

4.将价格大于100的商品上涨2%，其余上涨4%。
UPDATE product
SET price = CASE 
              WHEN price > 100 THEN price * 1.02
              ELSE price * 1.04
            END
WHERE price IS NOT NULL;

5.将名字包含cake的商品删除。
DELETE FROM product 
WHERE name LIKE '%cake%';

6.将价格高于平均价格的商品删除。
DELETE FROM product
WHERE price > (SELECT AVG(price) FROM product WHERE price IS NOT NULL);

## 题目三（5分）
#针对PostgreSQL
使用参考下面的语句添加10万条商品，

-- PostgreSQL Only
INSERT INTO product (name, price)
SELECT
    'Product' || generate_series, -- 生成名称 Product1, Product2, ...
    ROUND((random() * 1000)::numeric, 2) -- 生成0到1000之间的随机价格，保留2位小数
FROM generate_series(1, 100000);
比较DELETE和TRUNCATE的性能差异。

INSERT INTO product (product_no, name, price)
SELECT
    'P' || LPAD(generate_series::text, 6, '0'),
    'Product' || generate_series,           
    ROUND((random() * 1000)::numeric, 2)      
FROM generate_series(1, 100000);

#在PostgreSQL中测试10万条记录的删除操作
   DELETE测试
EXPLAIN ANALYZE DELETE FROM product;
   TRUNCATE测试
EXPLAIN ANALYZE TRUNCATE product;
DELETE操作是逐行删除的方式，执行时间与数据量成正比，支持WHERE条件筛选，且具有回滚性。
而TRUNCATE通过直接释放整个表的数据页来实现数据清除，执行速度更快，只能全表删除不具备条件筛选能力，不可回滚。

#针对MySQL
参考generate_data.py生成数据，在MySQL比较LOAD DATA和SELECT INTO的性能差异。
