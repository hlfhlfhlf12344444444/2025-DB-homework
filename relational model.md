# Relational Model

<font size="5">42233063-数据科学与大数据技术-韩璐帆</font>
## 题目一
考虑一个银行数据库，其关系模式如下所示：

- branch (branch_name, branch_city, assets)
- customer (ID, customer_name, customer_street, customer_city)
- loan (loan_number, branch_name, amount)
- borrower (ID, loan_number)
- account (account_number, branch_name, balance)
- depositor (ID, account_number)

使用关系代数完成下面的查询：

1. 找到位于成都市的支行的名字。
$$
\pi_{\text{branch\_name}} (\sigma_{\text{branch\_city}="成都"} (\text{branch}))
$$

2. 找到在杨柳支行有贷款（loan）的借款人（borrower）的ID。
$$
\pi_{\text{ID}} ((\sigma_{\text{branch\_name}="杨柳"}(\text{loan}))\bowtie \text{borrower})
$$
或者：
$$
\pi_{\text{ID}} (\sigma_{\text{branch\_name}="杨柳"} (\text{borrower} \bowtie \text{loan}))
$$
## 题目二
假设数据库中存储用户名和密码的关系模式是 users(name, pswd, gender)，请结合关系代数简述实现用户登录逻辑的思路。
# ANSWER1
1.用户输入用户名
 → 查询数据库，验证用户名：$$\sigma_{\text{name}="XXX"} (\text{users})$$
→→查询成功，进入步骤2 
→→查询不到匹配的记录，登录失败，提示“_不存在该用户_ ”
2.用户输入密码
 → 查询数据库，验证密码：$$\sigma_{\text{pswd}="XXX"} (\sigma_{\text{name}="XXX"}(\text{users}))$$
→→查询成功，登录成功，跳转到主页：
$$
\pi_{\text{gender}}(\sigma_{\text{pswd}="XXX"} (\sigma_{\text{name}="XXX"}(\text{users})))$$
提示“_欢迎XXX(用户名)先生/女士_ ”

→→查询不到匹配的记录，登录失败，提示“_密码错误_ ”

# ANSWER2
用户输入用户名和密码
 → 查询数据库，验证用户名和密码：
$$\sigma_{\text{name}="XXX"\wedge \text{pswd}="XXX"} (\text{users})$$
→→查询成功，登录成功，跳转到主页：
$$
\pi_{\text{gender}}(\sigma_{\text{name}="XXX"\wedge \text{pswd}="XXX"} (\text{users}))$$
提示“_欢迎XXX(用户名)先生/女士_ ”

→→查询不到匹配的记录，登录失败，提示“_用户名或密码错误_ ”