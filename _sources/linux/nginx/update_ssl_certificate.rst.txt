.. _linux-nginx-update-ssl-certificate:

nginx自动更新ssl证书
=================================

:ref:`wechat`

安装工具
----------------------

.. code-block:: bash

    yum install epel-release

    wget https://dl.eff.org/certbot-auto --no-check-certificate

    chmod +x certbot-auto

    ./certbot-auto -n





生成证书，定时任务
--------------------------------

* 第一次生成证书

.. code-block:: bash

    ./certbot-auto certonly --email my@qq.com --agree-tos --no-eff-email --webroot -w /root/html/ -d www.pydict.com

上面命令中的/root/html/路径表示nginx配置中的root目录

如果有多个域名，命令后面继续加 -d 参数就行


* 自动更新证书

证书会有有效期，所以可以弄一个定时任务自动更新证书

0 3 * * * /root/certbot-auto renew --disable-hook-validation --renew-hook "/usr/sbin/nginx -s reload"

这里表示每天凌晨3点更新一遍证书，如果证书没有失效，不会起作用

/usr/sbin/nginx是nginx的实际路径，可以用 which nginx 来定位位置




https配置
-----------------------------

.. code-block::

    server {
        listen 443 ssl;
        server_name pydict.com;

        ssl_certificate /etc/letsencrypt/live/www.pydict.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/www.pydict.com/privkey.pem;

        ssl_ciphers ECDHE-RSA-AES256-SHA384:AES256-SHA256:RC4:HIGH:!MD5:!aNULL:!eNULL:!NULL:!DH:!EDH:!AESGCM;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        ssl_session_cache shared:SSL:10m;

        access_log  logs/access.log  main;

        gzip on;
        gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png application/vnd.ms-fontobject  application/x-font-ttf  font/ttf     font/opentype font/x-woff  image/svg+xml;

        error_page  404 /404.html;
        error_page  500 502 503 504 /50x.html;

        client_max_body_size 75M;

        root    /root/html/otfsenter.github.io;
        location / {
            index index.html;
        }
    }





http配置
-------------------

.. code-block::

    server {
        listen  80;
        server_name pydict.com;

        access_log  /var/log/nginx/access.log;
        error_log   /var/log/nginx/error.log;

        charset utf-8;

        error_page  404 /404.html;
        error_page  500 502 503 504 /50x.html;

        client_max_body_size 75M;

        location / {
            return 301 https://www.pydict.com$request_uri;
        }
    }

**这个http的配置中，配置了一个301，这样就算访问http也会重定向到https**


