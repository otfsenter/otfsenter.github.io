.. _linux-nginx-config-cdn:

************
config cdn
************


生成一个泛域名的加速域名
===========================

\*.idlepig.cn 对应生成一个加速域名: all.idlepig.cn.w.cdngslb.com

泛域名配置加速域名
===========================

idlepig.cn域名解析中，\*.idlepig.cn配置cname为all.idlepig.cn.w.cdngslb.com


主域名配置A记录
===========================

\@.idlepig.cn主域名配置A记录，放主机IP

nginx配置
==========

主配置文件：nginx.conf

.. code::

    server {
            listen       80;
            server_name www.idlepig.cn;

            add_header Cache-Control public;

            # root         /root/html/otfsenter.github.io/index.html;

            # Load configuration files for the default server block.
            include /etc/nginx/default.d/*.conf;


            location / {
                root /root/html/otfsenter.github.io/;
                index index.html;
            }
            

            error_page 404 /404.html;
            location = /404.html {
            }

            error_page 500 502 503 504 /50x.html;
            location = /50x.html {
            }

        }


副配置文件：conf.d/pandomain.conf

.. code::

    server {
        listen 80;
        server_name idlepig.cn;
        return 301 http://www.idlepig.cn$request_uri;
    }

结果
====

访问idlepig.cn时，解析出主机，到nginx上的副配置，然后永久重定向到www.idlepig.cn，这个时候因为www.idlepig.cn已经配置了cname，就可以和访问www.idlepig.cn一样，直接进行cdn加速。
