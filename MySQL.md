# MySQL学习笔记

## 服务

### 启动服务
命令行以管理员方式运行：`net start MySQL`  
### 停止服务
命令行以管理员方式运行：`net stop MySQL`  
### 登录
 - 1.以MySQL自带的命令行直接输入密码
 - 2.用命令行输入：`mysql -h localhost -P 3306 -u root -pxiaolin`  
   - 简写：`mysql -u root -pxiaolin`
 
 ## 常见命令
 - 查看数据库：`show databases;`
 - 进入仓库：`use <name>;` 	
 - 显示仓库下的表：`show tables;`
 - 显示mysql仓库下的表：`show tables from mysql；`
 - 显示当前所在仓库：`select database();`
 - 创建表：`create table name(id int,name varchar(20)); `
 - 查看表内容：`desc tablename`
 - 查看表得数据：`select * from tablename`
 - 插入数据：`insert into tablename(id ,name) values(1,'jonh');`
 - 修改数据：`update tablename set name='lilei' where id=1;`
 - 删除数据：`delete from tablename where id=1;`
 - 查看版本：`select version();`
 - 注释：`#或者 --（空格） `
 
#进阶1：基础查询
语法：
select 查询列表 from 表名；

特点：
1.查询列表可以是：表中的字段、常量值、函数
2.查询的结果是一个虚拟的表格
###打开库   
打开库：  
`USE myemployees ;`  
- 1.查询表中的单个字段:  
`SELECT last_name FROM employees;`  
- 2.查询表中的多个字段:
```
SELECT 
  last_name,
  salary,
  email`
FROM
  employees ;
```
  
- 3.查询表中的所有字段:  
  `SELECT * FROM employees;`  
- 4.查询常量值  
`SELECT 100;`  
`SELECT 'john';`  
- 5.查询表达式
`SELECT 100%98;`  
- 6.查询函数  
`SELECT VERSION();`  
- 7.别名  
```
方式一：
SELECT 100%98 AS 结果；;
SELECT last_name AS 姓,first_name AS 名 FROM employees;
方式二:
SELECT last_name 姓,first_name 名 FROM employees;
```
案列：查询salary,显示结果为out put,与关键字重名加单或者双引号  
`SELECT salary AS 'out put' FROM employees;`  
- 8.去除重复distinct  
案例：查询部门编号  
`SELECT DISTINCT department_id FROM employees;`  

- 9.+号的作用  
mysql中的+号：  
仅仅只有一个功能：运算符  
`select 100+90 as 和;` 两个为数值，做加法运算  
`select '123'+90;`其中一个为字符，试图将字符转换成数值型，如果转换成功，则继续做加法运算
`select 'john'+90; `如果转换失败，将其中的字符当0使用
`select null+10; `如果其中有一方为null，则结果为null

案例：查询员工名和姓链接成一个字段，并显示为 姓名
```
SELECT 
  last_name + first_name AS 姓名 
FROM
  employees ; 
```  
 - 10.链接用concat
 
```
SELECT 
	CONCAT(last_name,first_name) AS 姓名
FROM
	employess;
  
 SELECT CONCAT('a','b') AS 结果; 
```
  
- 11.如果为NULL显示为0，判断语句  
```
SELECT
	IFNULL(commission_pct,0) AS 奖金,
	commission_pct
FROM 
	employees;
	
SELECT
	CONCAT(`first_name`,',',`last_name`,',',IFNULL(`commission_pct`,0)) AS out_put
FROM employees;
```  
  
  
#进阶2
语法：  ```
	select   
		- 查询列表  
	from  
		- 表名  
	where  
		- 筛选条件;  
		```  
分类：  
	一、条件表达筛选  
	条件运算符：>,<,=,(!=,<>),>=,<=  
	二、逻辑表达式筛选  
	逻辑运算符：用于连接条件表达式  
		     &&, ||, !  
		     and or not  
		     
三、模糊查询:  
	`like, between, and, in, is null  `
		    

一、按条件表达式筛选  
案例1：查询工资>12000的员工信息
```
SELECT 
	*
FROM
	employees
WHERE
	salary >12000;
```	  
案例2：部门编号不等于90号的员工名和部门编号
```
SELECT 	
	last_name,
	department_id
FROM
	employees
WHERE 
	department_id!=90;
```	
二、按逻辑表达式筛选
	
案列1：查询工资在10000到20000之间的员工名，工资，奖金
```
SELECT 	
	last_name,
	salary,
	commission_pct
FROM
	employees
WHERE 
	salary>=10000 AND salary<=20000;
```	
案列2：查询部门编号不在90-110之间的，或者工资高于15000员工信息
```
SELECT
	*
FROM
	employees
WHERE
	department_id>=90 AND department_id<=110 OR salary >15000;
```	
	
三、模糊查询
```
like
特点：
1、一般和通配符一起使用
	通配符：
	% 任意多个字符，包含0个字符
	— 任意单个字符
between and
in
is null | is not nyll
```

案例1：查询员工名中包含字符a的员工信息
```
SELECT
	last_name
FROM 
	employees
WHERE
	last_name LIKE '%a%';
```	
案列2：查询员工名中第三个字符为n,第五个字符为l的员工名和工资	
```	
SELECT
	last_name,
	salary
FROM
	employees
WHERE
	last_name LIKE '__n_l%';
```	
案例3：查询员工中第二个字符为_的员工名（_本身就是通配符用\转义）  
```
方式一：
SELECT 
	last_name
FROM
	employees
WHERE
	last_name LIKE '_\_%';
```	
方式二:
```
SELECT 
	last_name
FROM
	employees
WHERE
	last_name LIKE '_$_%' ESCAPE '$';	
```
2.between and (包含临界值)  
案列1:查询员工编号在100-120之间员工信息  
方式一：
```
SELECT 
	*
FROM
	employees
WHERE
	employee_id>=100 AND employee_id<=120;
```
方式二：
```
SELECT 
	*
FROM
	employees
WHERE
	employee_id BETWEEN 100 AND 120;
```
3.in(值类型必须统一或者兼容（可以隐士的转换）且不能用通配符)   
案列；查询员工的工种编号是:IT_PROG,AD_PRES,AD_VP中的一个员工名和工种编号   
方式一：  
```
SELECT
	last_name,
	job_id
FROM
	employees
WHERE
	job_id = 'IT_PROT' OR job_id='AD_PRES' OR job_id='AD_VP';
```
方式二：
```
SELECT
	last_name,
	job_id
FROM
	employees
WHERE
	job_id IN('IT_PROT','AD_PRES','AD_VP');
```
4.is null和is not null  
 - !=和<>不能用于判断null  

案列1：查询没有奖金的员工名和奖金率  
```
SELECT
	last_name,
	salary
FROM
	employees
WHERE
	commission_pct IS NULL;
```
1. 安全等于：<=>相当于等于  
2. 可以判断null值也可以判断普通数值  
案列1：查询没有奖金的员工名和奖金率    
```
SELECT
	last_name,
	salary
FROM
	employees
WHERE
	commission_pct <=> NULL;
```
案列1：查询工资为12000的员工信息  
```
SELECT
	last_name,
	salary
FROM
	employees
WHERE
	salary =12000;
```	
案列2：查询员工号为100的员工的姓名和部门号和年薪
```
SELECT
	last_name,
	department_id,
	salary *12*(1+IFNULL(commission_pct,0)) AS 年薪
FROM
	employees
WHERE
	department_id =100;
```

#进阶3:排序查询
语法：
```
SELECT 
	查询列表
	
FROM 
	表
where
	条件
order
	排序条件(asc升序|desc降序)默认成降序

```
引入表
`use myemployees`  

- 案列1：查询员工信息，按工资升序
```
select
	*
from
	employees
order by
	salary asc;
```
- 案列2：查询部门编号>=90的员工信息，按入职时间升序
```
select
	*
from
	employees
where
	department_id>=90
order by hiredate asc;
```
- 案列3：按年薪的高低显示员工的信息和年薪
方式一：
```
select
	*, salary*12*(1+ifnull(commission_pct,0))as 年薪
from 
	employees
order by 
	salary*12*(1+IFNULL(commission_pct,0)) desc;
```
方式二：
```
select
	*, salary*12*(1+ifnull(commission_pct,0))as 年薪
from 
	employees
order by 
	年薪 desc;
```
- 案列4：按姓名的长度显示员工的姓名和工资（按函数排序）
```
select 
	length(last_name) as 字节长度, 
	last_name,salary
from 
	employees
order by 
	length(last_name) desc;
```
- 案列5：查询员工信息，要求先按工资升序，再按照员工编号排序(先执行第一个条件，再在条件下执行第二个条件)
```
select
	*
from
	employees
order by
	salary asc,
	employee_id desc;

```


# 进阶4：常见函数
概念：将一组逻辑语句封装在方法中，对外保罗方法名。  
调用：SELECT 函数名（实参列表） FROM 表  
分类：  
	1,、单行函数  
	如：CONCAT,LENGTH、IFNULL等  
	2、分组函数  
	功能：做统计使用，又称统计函数，聚合函数，组函数  
	

- 一、字符函数  
  -1.0 LENGTH 获取参数值的字节个数  
  ```
  select length('john');--4
  SELECT LENGTH('徐小林ha');--11	
  ```
  
  -2.0 CONCAT拼接  
  `SELECT concat (last_name,'_',fist_name) as 姓名 from employees;`  
  
  - 3.0 UPPER,LOWER大小写转换  
  ```
  SELECT UPPER('john');
  SELECT LOWER('JOHN');
  ```
  - 4.0函数嵌套调用，  
  `SELECT CONCAT(UPPER(last_name),LOWER(first_name))AS 姓名 FROM employees;`
  
  - 5.0 SUBSTR（截取字符返回，下表从1开始）、SUBSTRING  
  ```
  select
	substr('李莫愁爱上了炉渣男',7) out_put;
  SELECT
	SUBSTR('李莫愁爱上了炉渣男',1,3) out_put;(从1处开始截取3个字符)
  ```
  - 6.0 姓名中首字符大写，其他字符小写然后用_拼接，显示出来
  ```
  select
	concat (upper(substr(last_name,1,1)),'_',lower(substr(last_name,2)))
  from 
	employees;
  ```	
  
  -7.0 INSTR(找到返回位置，找不到返回0)  
  `select instr('杨不悔爱上了殷六侠','殷六侠') as out_put;`
  
  -8.0 TRIM（去掉空格或者指定东西 ）
  ```  
  select length(trim('   张翠山   ')) as out_put;
  SELECT TRIM('a' from 'aaaa张翠山aaaa额aaaaa') AS out_put;
  ```
  
  -9.0 LPAD(左填充，只能输出指定大小字节，不够用指定字符填充)
	
	`select lpad('小林','10','*');`  
  -10. RPAD(右填充)
  `select rpad('小林','10','*');`
  
  -11.0 REPLACE（替换）  
   `select replace('我是小林','小林','帅哥');`

- 二、数学函数
  - 1.0 ROUND 四舍五入  
  `select round(-1.456);`
  `select round(1.456,2);`保留2位
  - 2.0 CEIL 向上取正  
   `select ceil (1.02);`
  - 3.0 FLOOR 向下取整数  
   `SELECT floor(9.99);`
  - 4.0 TRUNCATE 截断
  ` SELECT truncate (1.69999,1);` 
  
  - 5.0 MOD 取余  
   `SELECT mod(10,3);`
   
- 三、日期函数
  - 1.0 NOW 返回当前系统日期+时间  
 ` SELECT NOW();`
  - 2.0 CURDATE 返回当前日期不包含时间  
  `SELECT CURDATE();`
  - 3.0 CURTIME 返回时间不返回日期  
  `SELECT CURTIME();`
  - 4.0 可以获取指定的不发，年。月，日，小时，分，秒  
  ```
  SELECT YEAR(NOW());
  SELECT MONTH(NOW());
  SELECT YEAR('1991-1-1');
  SELECT YEAR(hiredate) 年 FROM employees;
  ```
  - 5.0 STR_TO_DATE(将字符通过指定格式转换成日期)  
  ```
  SELECT STR_TO_DATE('3-1998-28','%c-%Y-%d') AS put_out;
  SELECT * FROM employees WHERE hiredate = '1992-4-3';
  ```
  -6.0 DATE_FORMAT将日期转换成字符  
  `SELECT DATE_FORMAT(NOW(),'%y年%m月%d日') AS out_out;`

- 四、其他函数
```
	SELECT VERSION();
	SELECT DATABASE();
	SELECT USER();
```
- 五、流程控制函数   
  - 1.0 IF函数：IF ELSE 的效果
  ```
  SELECT IF(10>5,'大','小')；
  SELECT 
	last_name,
	commission_pct,
	IF(commission_pct IS NULL,'没奖金','有奖金') AS 备注
   FROM employees;
   ```
  - 2.0 CASE 函数：
  ```
	1. 类似于switch CASE
	2. 不同点是：
	CASE 变量
	WHEN 变量 THEN 值或者函数
	WHEN 变量 THEN 值或者函数
	...
	ELSE 变量
	END
	列子：查询员工的工资，要求
	部门号为30，显示1.1倍工资
	部门号为40，显示1.2倍工资
	部门号为40，显示1.2倍工资
	其他部门，显示原工资
	```
	```
	SELECT 
		salary 原工资,
		department_id,
		CASE department_id
		WHEN 30 THEN salary*1.1
		WHEN 40 THEN salary*1.2
		WHEN 50 THEN salary*1.3
		ELSE salary
		END AS 新工资
	FROM employees;
    ```
  - 3.0 CASE的多重使用  
  ```
    语法：
    CASE
    WHEN 条件1 THEN 先显示的值1或语句；
    ...
    ELSE 要显示的值n或者语句n；
    
    列子：查询员工工资的情况
    如果工资>20000,要显示A级别  
    如果工资>150000,要显示B级别
    如果工资>10000,要显示C级别
    否则D级别
    SELECT salary,
    CASE 
    WHEN salary>20000 THEN 'A'
    WHEN salary>15000 THEN 'B'
    WHEN salary>10000 THEN 'C'
    ELSE 'D' 
    END AS 工资级别
    FROM employees;		
```
































	
	
	
	
	
	
	  
  