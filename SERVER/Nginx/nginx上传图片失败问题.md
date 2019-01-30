# nginx上传图片失败

## BUG记录

### 环境状态 

    宝塔linux 初始环境
    
    nginx 1.14

### 问题描述

    当nginx开启 SSL时 图片上传出现BUG
    
    图片上传被服务器拦截


## 解决方法

    /www/server/nginx/
    
    proxy.conf文件

    修改 client_body_buffer_size 5120k;