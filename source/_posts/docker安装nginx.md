---
title: docker安装nginx
url: 319.html
id: 319
categories:
  - Linux &amp; VPS
date: 2019-02-20 23:18:07
tags:
---

假设将nginx的相关数据及配置挂载于/docker/nginx目录下，则创建目录结构如下：

    docker
    └── nginx
        ├── conf
        │   ├── conf.d
        │   └── nginx.conf
        ├── logs
        └── www
    

其中nginx.congf为文件，其余为文件夹。 将nginx的默认配置复制至nginx.conf

    server {
        listen       80;
        server_name  localhost;
    
        #charset koi8-r;
        #access_log  /var/log/nginx/host.access.log  main;
    
        location / {
            root   /usr/share/nginx/html;
            index  index.html index.htm;
        }
    
        #error_page  404              /404.html;
    
        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }
    
        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}
    
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}
    
        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
    

运行命令

    docker run -p 80:80 -p 443:443 --name nginx -v $PWD/www:/www -v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf -v $PWD/logs:/wwwlogs -v $PWD/conf/conf.d:/etc/nginx/conf.d -d nginx