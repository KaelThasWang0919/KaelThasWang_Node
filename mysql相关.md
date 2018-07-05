#1.mysql 外网无法访问


###判断Mysql的端口状态
```
netstat -apn |grep 3306 

```
如果输出结果包括tcp 0 0 127.0.0.1:3306 0.0.0.0:* LISTEN -时，说明监听的host为127.0.0.1，只能本地访问，需要设置监听host：

```
1.需要修改监听的host 
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf 
注释掉bind-address = 127.0.0.1， 即#bind-address = 127.0.0.1
2.重启服务 
sudo /etc/init.d/mysql restart
3.查看端口状态 
netstat -apn |grep 3306 
此时应为：tcp6 0 0 :::3306 :::* LISTEN -
```
###修改用户表
当远程访问出现not allowed的提示消息时，说明远程用户无权限，则需要修改用户表：
 
1. 登录数据库 

	`mysql -u root -p `

2. 选择数据库
 
	`use mysql; `
	
3. 修改root用户可以在所有机器登录（root只是举例，%表示所有机器） 

	`update user set host = '%' where user = 'root';`

4. 重启服务 

	`sudo /etc/init.d/mysql restart`
	

原文链接 `https://blog.csdn.net/u013760355/article/details/79111499`