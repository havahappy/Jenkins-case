# mysql
mysql学习笔记
centos7上安装mysql
一、安装mysql
1. 下载mysql的repo源
$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
2. 安装mysql-community-release-el7-5.noarch.rpm包
$ sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
3. 安装mysql
$ sudo yum install mysql-server

二、设置root密码
1.登陆mysql
$ mysql -u root
1.1登录时有可能报这样的错：ERROR 2002 (HY000): Can‘t connect to local MySQL server through socket ‘/var/lib/mysql/mysql.sock‘ (2)，原因是/var/lib/mysql的访问权限问题。下面的命令把/var/lib/mysql的拥有者改为当前用户：
如果没有报错可忽略1.1和1.2
$ sudo chown -R openscanner:openscanner /var/lib/mysql
1.2重启服务
$ service mysqld restart
2.重置密码
$ mysql -u root
mysql > use mysql;
mysql > update user set password=password('123456') where user='root';
mysql > commit;
mysql > exit;

三、设置可远程访问mysql
$ mysql -u root
mysql > use mysql;
mysql > Grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
mysql > flush privileges;
