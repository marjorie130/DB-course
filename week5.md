### WEEK5

**题目一**

1. 因为min()是一个聚合函数而第一个SQL语句中没有使用GROUP BY 对dept_name进行分组，所以会出现错误。

    在datagrip中运行SQL语句出现报错：也说明了要使用聚合函数必须要使用GROUP BY进行分组。

![image-2](https://github.com/user-attachments/assets/e7f5c658-dffe-4dae-91f8-175c94e61ee5)


2. 主要是having字句中出现的name没有在group by字句中出现，也没有在聚合函数中所以会报错。
运行结果：

![image-3](https://github.com/user-attachments/assets/30e25e81-2c2a-4db7-ab15-09cf314e2be6)

4. 首先WHERE子句用于过滤行，其按行进行过滤，而having字句在group by 字句之后进行过滤，其按组进行过滤。故其不能出现在where之后。

![image-4](https://github.com/user-attachments/assets/be8f39bc-388c-487f-bcc1-11b029809215)


**题目二**

1. 找出工资最高的员工（只有一位）

    方法一：嵌套子查询
    ```sql
    SELECT name, dept_name, salary 
    FROM instructor 
    WHERE salary = (SELECT MAX(salary) FROM instructor);
    ```

    方法二：使用ALL聚合函数
    ```sql
    SELECT name, dept_name, salary
    FROM instructor
    WHERE salary >= ALL (
        SELECT salary 
        FROM instructor
    );
    ```
2. 找出工资最高的员工（有多位）
    
    方法一：使用with
    ```sql
    WITH max_salary AS (
        SELECT MAX(salary) AS max_sal
        FROM instructor
    )
    SELECT name, dept_name, salary
    FROM instructor
    WHERE salary = (SELECT max_sal FROM max_salary);
    ```


**题目三**

    ```sql
    SELECT 1 IN (1);

    SELECT 1 = (1);

    SELECT (1, 2) = (1, 2);

    SELECT (1) IN (1, 2);
 
    ```


解释：
1：1在（1）中，所以返回true；

2：1=1，所以返回true，括号不影响比较结果；

3：（1，2）=（1，2），逐元素比较元组内容，所以返回true；

4：1在（1，2）中，所以返回true，括号不影响标量；
