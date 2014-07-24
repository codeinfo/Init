Windows 环境下安装 Apache2+fastcgi+php5(non thread safe)+MySql5+ZendGuardLoader
----
#准备软件：
	mysql-5.5.20-win32
	httpd-2.2.22-win32-x86-no_ssl
	php-5.4.15-nts-Win32-VC9-x86
	ZendGuardLoader-70429-PHP-5.4-Windows-x86
#安装步骤
##1.安装mysql-5.5.20-win32
##2.安装apache web server httpd-2.2.22-win32-x86-no_ssl
##3.解压缩php-5.4.15-nts-Win32-VC9-x86 到php5目录
##4.配置apache httpd.conf
配置<Directory "D:/app_cms/Apache2.2/htdocs">项
Options ExecCGI FollowSymLinks ExecCGI 
修改：如下
    #Options Indexes FollowSymLinks
 Options ExecCGI FollowSymLinks ExecCGI
修改
 AllowOverride None
改成
 AllowOverride All
 修改
 <IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
改成
 <IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>
去掉注释使其支持虚拟主机
# Virtual hosts
Include conf/extra/httpd-vhosts.conf

最后加上使PHP以CGI方式运行
# FastCGI with Thread Safety disabled
LoadModule fcgid_module modules/mod_fcgid.so
<IfModule mod_fcgid.c> 
      AddHandler fcgid-script .php 
      FCGIWrapper "D:/app_cms/php5/php-cgi.exe" .php 
      FcgidMaxRequestLen  1024000000
</IfModule>
 
##5.下载mod_fcgid-2.3.6-win32-x86.zip(mod_fcgid.so)
http://archive.apache.org/dist/httpd/binaries/win32/
解压缩mod_fcgid-2.3.6-win32-x86.zip
把mod_fcgid.so文件复制到D:\app_cms\Apache2.2\modules 下

##6.ZendGuardLoader 支持
解压缩包，找到ZendLoader.dll文件，拷贝到，PHP安装目录D:\app_cms\php5\ext下
再在php.ini文件最后加上以下设置：
[Zend.loader]
zend_loader.enable=1
zend_loader.disable_licensing=1
zend_loader.obfuscation_level_support=3
zend_loader.license_path=
zend_extension="ext\ZendLoader.dll"