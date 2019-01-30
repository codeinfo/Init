#ngnix CPU负载百分百

## 服务器环境

    Linux
    宝塔面板
    ngnix
    php-fpm

## 发生原因

    因服务器受到并发攻击，并发连接数约为5000次/s，导致CPU满载100%运行，php-fpm 运行阻塞，进程进入sleep状态。

    因为系统内涉及微信，在流量和CPU达到峰值时，PHP访问微信服务会发生错误，在proc中即可看到。

## Linux 相关命令
    
    w 查看当前负载

    top 查看当前进程 占用内存级cpu

    proc 内核管理进程，反馈进程执行

## 解决方案

    1. 使用宝塔面板中 nginx 防火墙
    2. 启用nginx服务器中的过滤功能-waf



