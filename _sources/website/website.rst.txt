.. _website:

*****************
网站相关的信息
*****************

idlepig.cn的备案号
==========================

**footer**

.. code::

    D:\Python\Lib\site-packages\sphinx_bootstrap_theme\bootstrap\layout.html

在show_sphinx这个tag里面

.. code-block:: html

    {%- if show_sphinx %}
    <a href="http://www.beian.miit.gov.cn" target="_blank">粤ICP备19052369号-2</a>
    <!-- {% trans sphinx_version=sphinx_version|e %}Created using <a href="http://sphinx-doc.org/">Sphinx</a> {{ sphinx_version }}.{% endtrans %}<br/>-->
    {%- endif %}
    
google ping
==========================

能加大google爬取网站的机率

https://www.google.com/ping?sitemap=http://idlepig.cn/sitemap.xml


jetbrains图标
==================

https://note.youdao.com/ynoteshare1/index.html?id=695cff73d21089a7a85c8e45083a8165&type=notebook#/WEB52da3a0c51d7778eb9db240f7a5d95ab

公众号图标
=================

https://note.youdao.com/yws/api/personal/file/WEBf1a12c76ffc392012344ded4e9f6d823?method=download&shareKey=695cff73d21089a7a85c8e45083a8165


拉取otfsenter.github.io上面的网页到服务器
=================================================

.. code-block:: shell

    mkdir -p /root/html
    cd /root/html
    git clone https://github.com/otfsenter/otfsenter.github.io.git


通过docker启动nginx服务
============================

nginx.sh

.. literalinclude:: ./scripts/nginx.sh


没有本地的nginx好维护

现在使用本地加cdn的方法 :ref:`linux-nginx-config-cdn`


ctrontab 
===========================================================

定时拉取github上面的otfsenter.github.io.git这个仓库，解决上传之后，服务器不更新的问题

.. code-block::

    * * * * * /root/pull.sh 1>/dev/null 2>&1

pull.sh脚本的内容


.. literalinclude:: ./scripts/pull.sh



