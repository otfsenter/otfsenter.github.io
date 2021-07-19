# default config

## 安装nginx

```
dnf install nginx -y
```

## 修改html文件目录权限

```
chmod 755 /root
chmod 755 /root/html
chmod 644 /root/html/*
```

## 修改`/etc/nginx/nginx.conf`文件

* server 80


`user nginx;`修改成`user root;`

`root    /usr/share/nginx/html;`修改成`root    /root/html;`

```
location / {
}
```

修改成

```
location / {
    index   index.html;
}
```


* server 443

阿里云上面申请免费的证书，上传服务器，然后修改配置

```
ssl_certificate "/root/cert/t.pem";
ssl_certificate_key "/root/cert/t.key"
```

`root    /usr/share/nginx/html;`修改成`root    /root/html;`

```
location / {
}
```

修改成

```
location / {
    index   index.html;
}
```


如果开启了443

server 80里面需要修改的如下

```
rewrite ^(.*)$  https://$host$1 permanent;
```