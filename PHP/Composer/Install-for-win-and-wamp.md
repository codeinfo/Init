Install for win and wamp
===

环境要求
---
PHP 5.3.4+ (以更好的使用Composer)
开启 Openssl 扩展

基础软件
---
[Wamp](http://www.wampserver.com/en/)


[Composer](https://getcomposer.org/)

安装问题
---
	1.Composer 需要使用 Openssl
	2.首先安装 Wamp 后，需要开启 Openssl ,需要注意的是 Wamp 在命令行和网站运行的 PHP 配置文件是不同的
	3.Wamp 开启命令行界面的 Openssl
	4. \wamp\bin\php\php5.4.12 打开此文件夹修改 php.ini  PS：不要在图标位置修改
	5.移动 libeay32.dll ssleay32.dll ext/php_openssl.dll 到 C:\windows\system32\ 目录下
	6.重启 Apache 服务器即可开启 Opensll