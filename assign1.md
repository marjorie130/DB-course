![alt text](image-1.png)
### 题目一
1. $\Pi_{branch\_name}(\sigma_{branch\_city='成都'}(branch))$

2. $\Pi_{ID}(\sigma_{branch\_name} = \text{'杨柳'}}(loan \bowtie borrower))$

### 题目二
1. **用户说明**：用户提供用户名 (input_name) 和密码 (input_pswd)

2. **用关系代数进行查询**：$\sigma_{\text{name} = \text{input\_name} \land \text{pswd} = \text{input\_pswd}}(users)$

3. 如果查询内容不为空则登录成功
