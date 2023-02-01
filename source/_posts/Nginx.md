---
title: Nginx
date: 2023-01-31 19:57:52
tags: Nginx
---

最近在搞小程序，有一些 NodeJs 服务部署在 Linux 服务器上，遇到了一些觉得需要记录的东西。

## sites-available 与 sites-enable

建立软连接：

```bash
ln -s /etc/nginx/sites-available/blog.conf /etc/nginx/sites-enabled/
```

## location 配置

我的小程序的前端请求中加入了/api，但是我的后台服务接口并没有以/api 开头。

最终在参考了 [zhengaoly 的简书文章](https://www.jianshu.com/p/fc91f00016e4)，进行了修改：

```nginx

 location  /api/ {
   #网站主页路径。此路径仅供参考，具体请您按照实际目录操作。
   #例如，您的网站主页在 Nginx 服务器的 /etc/www 目录下，则请修改 root 后面的 html 为 /etc/www。
  # root html;
   #index index.html index.htm;
    proxy_pass http://localhost:3000/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Port $server_port;
 }
```
