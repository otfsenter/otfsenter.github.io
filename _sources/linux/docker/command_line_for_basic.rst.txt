.. _docker-command-line-for-basic:

Docker常用的一些命令
=============================

:ref:`wechat`

新建一个container, 映射路径、端口
--------------------------------------

.. code-block::

    docker run -itd --name blog_nginx -v /home/ubuntu/vickey-wu.github.io/:/var/nginx/html/ -p 80:80 nginx

**冒号前的表示本地，冒号后表示 container 里的路径、配置**

-i: interactive

-t: tty

-d: daemon

--name: 为容器起一个名字

-v: volume

-p: port

最后的 nginx ，会从 docker 的官方网站拉去最新的 nginx 镜像


查看 container 的日志
---------------------------

.. code-block::

    docker logs -f --tail 50 blog_nginx

-f: follow

--tail: tail

50: 查看最后50行日志

blog_nginx: 是 container 的名字

进入 container 
---------------------

.. code-block::

    docker exec -it blog_nginx /bin/bash


从 container 里面复制文件出来
--------------------------------

.. code-block::

    docker cp blog_nginx:/etc/nginx/conf.d/default.conf .


