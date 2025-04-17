1. 使用单表查询

```sql
SELECT instructor.id ,count(sec_id)
FROM teaches,instructor
WHERE instructor.id = teaches.id
GROUP BY instructor.id;
```


2. 返回没有上课的老师

```sql
SELECT instructor.id, count(sec_id)
FROM instructor LEFT JOIN teaches
ON instructor.id = teaches.id
GROUP BY instructor.id ;
```

3. 使用标量子查询完成2

```sql
SELECT id,(SELECT count(sec_id) FROM teaches WHERE teaches.id = instructor.id)
FROM instructor;
```


4. 在FROM字句中追加 natural join section 不会出错

   takes 和 section 表中都有 section_id;
   由 natural join 自然连接的特性不会出错

5. 使用‘using’改写SQL

```sql
select *
from section join classroom 
using (building, room_number);  
```

二、应用题

1. 创建两个关系并添加测试数据

```sql
CREATE TABLE emp (
    emp_no varchar(10) PRIMARY KEY,
    ename  varchar(20),
    sal    decimal(10, 2),
    dept_no varchar(10)
);

CREATE TABLE emp_bonus (
    emp_no varchar(10),
    received date,
    type    varchar(10)
)

INSERT INTO emp VALUES ('7934', 'John', 5000, '42'),
                        ('7839', 'Jane', 6000, '42'),
                        ('7782', 'Bob', 5500, '15');

INSERT INTO emp_bonus VALUES ('7934', '17-MAR-2005', '1'),
                             ('7934', '15-FEB-2005', '2'),
                             ('7839', '15-FEB-2005', '3'),
                             ('7782', '15-FEB-2005', '1');
```
2. 列出部门编号42的所有员工的总工资和

```sql
SELECT 
    SUM(e.sal) AS total_salary,
    COUNT(b.emp_no) AS total_bonus_count
FROM emp e
LEFT JOIN emp_bonus b ON e.emp_no = b.emp_no
WHERE e.dept_no = '42';

```