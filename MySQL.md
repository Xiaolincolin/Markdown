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