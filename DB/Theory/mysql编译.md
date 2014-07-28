安装mysql,并启动之，然后给mysql的root账号设密码
# groupadd mysql
# useradd -m mysql -g mysql -d /usr/local/mysql
#tar xvfz mysql-5.0.87.tar.gz
#cd mysql-5.0.87
#./configure --prefix=/usr/local/mysql --localstatedir=/home/var --with-charset=utf8 --with-extra-charsets=all --with-berkeley-db --with-innodb --without-readline --enable-assembler --with-pthread --enable-thread-safe-client --with-client-ldflags=-all-static
#make
#make install
#检查/etc/my.cnf是否存在，若存在则修正里面的路径指向,否则数据库表文件可能不装在/home/var下

#/usr/local/mysql/bin/mysql_install_db --user=mysql
#chown -R mysql:mysql /home/var //设权限否则后面的mysqld_safe无法执行
#/usr/local/mysql/bin/mysqld_safe --user=mysql &
#cp ./support-files/mysql.server /etc/rc.d/init.d/mysql //以下两行：设置mysql自启动
#chmod +x /etc/rc.d/init.d/mysql
#chkconfig --add mysql 
//把mysql加到服务列表中, --add后面如果是mysql系统就会找/etc/rc.d/init.d/mysql 
#service mysql start
#/usr/local/mysql/bin/mysqladmin -u root password stoneage2
#cd /usr/local/include //建立快捷连接 /usr/local/include/mysql -> /usr/local/mysql/include
# ln -s /usr/local/mysql/include/mysql mysql  