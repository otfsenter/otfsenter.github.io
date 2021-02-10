.. _c:

*********
c and c++
*********

环境搭建-msys2
=================

下载地址::

    https://mirrors.tuna.tsinghua.edu.cn/msys2/distrib/x86_64/

帮助::

    https://mirrors.tuna.tsinghua.edu.cn/help/msys2/

C语言环境变量配置::

    https://blog.csdn.net/weixin_41624493/article/details/80639775

学习建议-学习顺序
======================

先stl，然后template，再学class，最后学操作裸指针

学习建议-内存泄漏
===================

new之后一定要delete

* shared_ptr 不要有循环引用

* weak_ptr

* unique_ptr

野指针相关
=================

stl容器

下标访问越界就会崩溃，根本没机会产生野指针


