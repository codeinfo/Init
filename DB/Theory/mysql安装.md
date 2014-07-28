linux下使用yum安装mysql
 
1、安装
查看有没有安装过：
          yum list installed mysql*
          rpm -qa | grep mysql*
 
查看有没有安装包：
          yum list mysql*
 
安装mysql客户端：
          yum install mysql
 
安装mysql 服务器端：
          yum install mysql-server
 
          yum install mysql-devel
  www.2cto.com  
2、启动&&停止
 
数据库字符集设置
          mysql配置文件/etc/my.cnf中加入default-character-set=utf8
 
启动mysql服务：
          service mysqld start或者/etc/init.d/mysqld start
开机启动：
          chkconfig -add mysqld，查看开机启动设置是否成功chkconfig --list | grep mysql*
 
          mysqld             0:关闭    1:关闭    2:启用    3:启用    4:启用    5:启用    6:关闭
停止：
          service mysqld stop
2、登录
 
创建root管理员：
          mysqladmin -u root password 123456
  www.2cto.com  
登录：
          mysql -u root -p输入密码即可。
忘记密码：
          service mysqld stop
 
          mysqld_safe --user=root --skip-grant-tables
 
          mysql -u root
 
          use mysql
 
          update user set password=password("new_pass") where user="root";
 
          flush privileges;  
 
3、远程访问
 
开放防火墙的端口号
mysql增加权限：mysql库中的user表新增一条记录host为“%”，user为“root”。
4、Linux MySQL的几个重要目录
  www.2cto.com  
数据库目录
         /var/lib/mysql/
配置文件
         /usr/share /mysql（mysql.server命令及配置文件）
相关命令
         /usr/bin（mysqladmin mysqldump等命令）
启动脚本
         /etc/rc.d/init.d/（启动脚本文件mysql的目录）