# mysql密码修改

1．首先确认服务器出于安全的状态，也就是没有人能够任意地连接MySQL数据库。 

因为在重新设置MySQL的root密码的期间，MySQL数据库完全出于没有密码保护的 状态下，

其他的用户也可以任意地登录和修改MySQL的信息。可以采用将MySQL对外的端口封闭，并

且停止Apache以及所有的用户进程的方法实现服务器的准安全状态。最安全的状态是到服

务器的Console上面操作，并且拔掉网线。

2．修改MySQL的登录设置：

    # vi /etc/my.cnf 

在[mysqld]的段中加上一句：skip-grant-tables 保存并且退出vi。

3．重新启动mysqld 

    # /etc/init.d/mysqld restart  ( service mysqld restart )

4．登录并修改MySQL的root密码

    mysql> USE mysql ; 
    mysql> UPDATE user SET Password = password ( 'new-password' ) WHERE User = 'root' ; 
    mysql> flush privileges ; 
    mysql> quit

5．将MySQL的登录设置修改回来 

    # vi /etc/my.cnf 

将刚才在[mysqld]的段中加上的skip-grant-tables删除 

保存并且退出vi。

6．重新启动mysqld 

    # /etc/init.d/mysqld restart   ( service mysqld restart )

7．恢复服务器的正常工作状态

将步骤一中的操作逆向操作。恢复服务器的工作状态。