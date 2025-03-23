### 
![alt text](image.png)

#### 题目一

CREATE TABLE users(
    name      VARCHAR(255) NOT NULL,
    pswd      VARCHAR(255) NOT NULL,
    gender    VARCHAR(10) NOT NULL,
    PRIMARY KEY (name)
);

#### 题目二

1. 

SELECT course_id 
FROM course 
WHERE dept_name = 'ComputerScience' and credits > 2
order by credits asc;

2. 

SELECT DISTINCT student.ID
FROM student
JOIN takes ON student.ID = ST
JOIN teaches ON takes.course_id = teaches.course_id
JOIN course ON teaches.course_id = course.course_id
WHERE instructor.name = 'Turing'


#### 题目三
含义是查询所有教师（instructor 表）中薪资高于至少一名在“会计”学院（dept_name = '会计'）工作的教师名字（name）