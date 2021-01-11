.. _sphinx-locale:


*******
locale
*******


.. code-block::

    sphinx-build -b gettext . locale
    sphinx-intl update -p locale -l zh_CN


官方链接

https://www.sphinx-doc.org/en/master/usage/advanced/intl.html

https://docs.readthedocs.io/en/stable/localization.html


build different language
============================


.. code-block::

    make -e SPHINXOPTS="-D language='zh_CN'" html
    make -e SPHINXOPTS="-D language='en'" html



在readthedocs上面设置中英文
======================================

先手动导入英文版本
-----------------------

项目名称：idlepig

语言：英语

branch：main


再导入中文版本
-----------------------

项目名称：idlepig_zh-CN

语言：简体中文

branch：main

然后两个一起build

分别看一下两个文档是否正常

然后在英文文档项目里面设置翻译项：选择简体中文的版本

**这样最后只能在中文文档里面看到翻译选项，英文的看不到**
