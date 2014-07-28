PHP安装

./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-mysql=/usr/local/mysql --with-mysqli=/usr/bin/mysql_config --with-iconv-dir=/usr/local --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --disable-rpath --enable-discard-path --enable-safe-mode --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --with-curlwrappers --enable-mbregex --enable-fastcgi --enable-fpm --enable-force-cgi-redirect --enable-mbstring --with-mcrypt --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-ldap --with-ldap-sasl --with-xmlrpc --enable-zip --enable-soap --without-pear --with-zlib --enable-pdo --with-pdo-mysql --with-mysql 
#mysqli扩展技术不仅可以调用MySQL的存储过程、处理MySQL事务，而且还可以使访问数据库工作变得更加稳定。 
make ZEND_EXTRA_LIBS='-liconv' 
make install  


--prefix=/usr/local/php

指定 php 安装目录 


--with-apxs2=/usr/local/apache/bin/apxs

整合 apache，apxs功能是使用mod_so中的LoadModule指令，加载指定模块到 apache，要求 apache 要打开SO模块


--with-config-file-path=/usr/local/php/etc               

指定php.ini位置


--with-MySQL=/usr/local/mysql

mysql安装目录，对mysql的支持


--with-mysqli=/usr/local/mysql/bin/mysql_config            

mysqli扩展技术不仅可以调用MySQL的存储过程、处理MySQL事务，而且还可以使访问数据库工作变得更加稳定。 

--enable-safe-mode   打开安全模式 

--enable-ftp   打开ftp的支持 

--enable-zip   打开对zip的支持 

--with-bz2    打开对bz2文件的支持        

--with-jpeg-dir   打开对jpeg图片的支持 

--with-png-dir   打开对png图片的支持 

--with-freetype-dir   打开对freetype字体库的支持 

--without-iconv   关闭iconv函数，种字符集间的转换 

--with-libXML-dir   打开libxml2库的支持 

--with-XMLrpc    打开xml-rpc的c语言 

--with-zlib-dir   打开zlib库的支持 

--with-gd    打开gd库的支持 

--enable-gd-native-ttf   支持TrueType字符串函数库 

--with-curl    打开curl浏览工具的支持 

--with-curlwrappers    运用curl工具打开url流 

--with-ttf     打开freetype1.*的支持，可以不加了 

--with-xsl     打开XSLT 文件支持，扩展了libXML2库 ，需要libxslt软件 

--with-gettext     打开gnu 的gettext 支持，编码库用到 

--with-pear    打开pear命令的支持，PHP扩展用的 

--enable-calendar    打开日历扩展功能 

--enable-mbstring    多字节，字符串的支持 

--enable-bcmath    打开图片大小调整,用到zabbix监控的时候用到了这个模块

--enable-sockets     打开 sockets 支持

--enable-exif    图片的元数据支持 

--enable-magic-quotes    魔术引用的支持 

--disable-rpath    关闭额外的运行库文件 

--disable-debug    关闭调试模式 

--with-mime-magic=/usr/share/file/magic.mime      魔术头文件位置


CGI方式安装才用的参数

--enable-fpm                       

打上PHP-fpm 补丁后才有这个参数，CGI方式安装的启动程序



--enable-fastCGI                   

支持fastcgi方式启动PHP



--enable-force-CGI-redirect        

重定向方式启动PHP



--with-ncurses                     

支持ncurses 屏幕绘制以及基于文本终端的图形互动功能的动态库

--enable-pcntl                     freeTDS需要用到的，可能是链接mssql 才用到


mhash和mcrypt算法的扩展

--with-mcrypt                     算法

--with-mhash                      算法

以上函数库需要安装




--with-gmp  应该是支持一种规范

--enable-inline-optimization  优化线程

--with-openssl                     openssl的支持，加密传输时用到的

--enable-dbase                     建立DBA 作为共享模块

--with-pcre-dir=/usr/local/bin/pcre-config      perl的正则库案安装位置

--disable-dmalloc

--with-gdbm                     dba的gdbm支持

--enable-sigchild

--enable-sysvsem

--enable-sysvshm

--enable-zend-multibyte         支持zend的多字节

--enable-mbregex

--enable-wddx

--enable-shmop

--enable-soap

指定了--with-apxs2=/usr/local/apache/bin/apxs以后，就不要再激活--enable-fpm和--enable-fastCGI，apxs是以php module的模式加载PHP的。

Mysql在编译了Mysql开发library以后，可以不用指定mysql的路径。

PHP编译存在基础的依赖的关系，编译PHP首先需要安装XML扩展，因为php5核心默认打开了XML的支持，其他的基础库，相应需要：

GD -> zlib, Png, Jpg, 如果需要支持其他，仍需要根据实际情况编译扩展库，ttf库需要freetype库的支持。

--enable-magic-quotes，是一个极其不推荐的参数，当然，如果你需要PHP为你做这些底下的工作，实际上他也没有很彻底的解决问题。

--with-openssl，需要openssl库。

mysqli是MySQL团队提供的MySQL驱动，具有很多实用的功能和典型特征。不过他不是MySQL于PHP平台最好的选择，PDO被证实，是一个简易、高并发性，而且易于创建和回收的标准接口。不过PDO也经历了5.3以前的内存溢出的问题，在5.3以后，在读取Oracle的LOB资源时，若不对内存进行限制，仍会内存溢出。

如果是产品模式，好像pear、shmop、ftp等，都不推荐使用，他们要做的事情，用C/C++，用Java，甚至其他脚本语言，都有很好很快速的选择，无需局限于使用PHP去实现。不熟悉的类库和不常用的库，也不推荐使用。magic-quote、session.auto_start、PHP服务器信息、PHP报错信息等在编译完成后，应该第一时间关闭，避免暴露服务器信息。

PHP对应的Web Server模式，Module、fastcgi、fpm只需要一种即可，服务器不是你的试验田。fastcgi可以选择Nginx和lighttpd，其实Nginx也是使用lighttpd的spwan-fcgi进行fcgi进程管理的。fpm是使用PHP自身去管理多进程，有点类似一个后端代理。无论什么模式，在发布产品服务器，都应该做进程和线程调优，做足够多的压力测试，找出最好的进程数组合。

选好一种PHP OPCode cache的扩展，这个也是很重要的，linux 2.6核心下，fcgi下，xcache有较好的实践经验，其他的在并发数增加以后，性能衰减严重。

如果真的想体验，宁可编译多几个PHP版本，也不要针对一个版本的PHP集合各种扩展，适应各种环境，这会让把你自己逼进窘境的。

 

编译扩展库：

/usr/local/php/bin/phpize

./configure  --with-php-config=/usr/local/php/bin/php-config

make

make install

ln -s ../ext/sockets/modules/sockets.so sockets.so 建立so动态链接库的软连接。

编译php：

./configure --prefix=/usr/local/php --with-curl=/usr/local/curl --enable-mbstring --enable-shmop --enable-sysvsem --enable-sysvshm --enable-sysvmsg --with-mysql=/usr/local/mysql --with-mysqli=/usr/bin/mysql_config  --enable-sockets 

make

make install

which php确保php是最新的，可以建立软链接。