# CDN for aliyun

## 能达到的效果

* 浏览器访问`idlepig.cn`可以重定向到`https://www.idlepig.cn/index.html`

即`http://idlepig.cn/`可以重定向

* `http://www.idlepig.cn`可以重定向到`https://www.idlepig.cn`

这个效果是在阿里云全站加速CDN里面设置重定向

* 问题：`https://idlepig.cn`不能重定向到`https://www.idlepig.cn/index.html`


~~因为只有`www.idlepig.cn`设置了CDN，而`idlepig.cn`是通过域名解析设置显性URL和@(主机记录)来实现的重定向的，所以`https://idlepig.cn`重定向暂时**没实现**~~

解决方法：

[万网主机基础设置里面配置301](https://netcn.console.aliyun.com/core/host/list2)

## 修改`/etc/nginx/nginx.conf`文件

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

## 阿里云全站动态加速

[地址](https://dcdn.console.aliyun.com/#/domain/list)

* 给`www.idlepig.cn`配置加速即可
* 证书在里面配置
* 重定向：http -> https
* 可以预热css、js、font、png链接

## 阿里云域名解析

[地址](https://dns.console.aliyun.com/#/dns/domainList)

| 主机记录 | 记录类型 | 解析路线(isp) | 记录值                            | TTL     |
| -------- | -------- | ------------- | --------------------------------- | ------- |
| www      | CNAME    | 默认          | www.idlepig.cn.w.cdngslb.com      | 10 分钟 |
| @        | 显性URL  | 默认          | https://www.idlepig.cn/index.html | 10 分钟 |


## 正常重定向的流程

`http://idlepig.cn/` -> `https://idlepig.cn/`-> `https://www.idlepig.cn/`

`https://idlepig.cn/`-> `https://www.idlepig.cn/`

`http://www.idlepig.cn/` -> `https://www.idlepig.cn/`

`https://www.idlepig.cn/` -> web page




