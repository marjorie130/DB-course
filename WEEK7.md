### 题目一

```sql
CREATE TABLE product (
    product_no VARCHAR(20) PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL
);
```
实例数据
```txt
P001,Laptop,899.99
P002,Smartphone,499.50
P003,Wireless Headphones,149.00
P004,Tablet,299.75
P005,Smart Watch,199.99
```
![image-6](https://github.com/user-attachments/assets/557d046b-861e-48f0-8de3-2f1cde55f2cf)



![image-7](https://github.com/user-attachments/assets/12747b94-4d0d-4781-9f4b-beae5019cfc2)




### 题目二

1. 
```sql
INSERT INTO product (product_no, name, price)
VALUES ('666', 'cake', NULL);
```
运行结果：


![image-8](https://github.com/user-attachments/assets/e3cab285-959c-45b3-b09b-edf89090e589)

2.

```sql
INSERT INTO product (product_no, name, price)
VALUES 
  ('P101', 'Wireless Mouse', 29.99),
  ('P202', 'Bluetooth Speaker', 89.50),
  ('P303', 'USB-C Cable', 12.00);
```
运行结果：

![image-9](https://github.com/user-attachments/assets/f58679ac-7205-40cf-80d4-b1779d5864d3)

3. 
```sql
UPDATE product
SET price = price * 0.8
WHERE price IS NOT NULL;  -- 仅更新已知价格的商品
```

运行结果：

![image-10](https://github.com/user-attachments/assets/c1cfc98e-5c1b-4b6c-8ea5-1133fd0b6143)

4. 

```sql
UPDATE product
SET price = CASE 
  WHEN price > 100 THEN price * 1.02
  ELSE price * 1.04
END
WHERE price IS NOT NULL;  -- 仅更新已知价格的商品
```
运行结果：

![image-11](https://github.com/user-attachments/assets/22b535e7-8325-4289-9ef9-44ed351f1f8b)


5.
```sql
DELETE FROM product
WHERE name ILIKE '%cake%';  
```

运行结果：


![image-12](https://github.com/user-attachments/assets/ed9f1ece-5809-49e9-9896-e02cb154e684)

6. 
```sql
DELETE FROM product
WHERE price > (
  SELECT AVG(price) 
  FROM product
  WHERE price IS NOT NULL  -- 排除 NULL 值计算平均
);
```
运行结果：


![image-13](https://github.com/user-attachments/assets/04fbf93b-4cf8-41bb-bf03-b65e14169cc9)

### 题目3

```sql
-- PostgreSQL Only
INSERT INTO product (name, price)
SELECT
    'Product' || generate_series, -- 生成名称 Product1, Product2, ...
    ROUND((random() * 1000)::numeric, 2) -- 生成0到1000之间的随机价格，保留2位小数
FROM generate_series(1, 100000);
```

添加10万条数据，比较delete与truncate的速度

DELETE：逐行删除：逐行扫描并删除满足条件的记录（如果有 WHERE 子句）。因此在没有条件的情况效率较低


TRUNCATE：整表清空：直接释放数据页（物理删除），而非逐行操作。效率较高

