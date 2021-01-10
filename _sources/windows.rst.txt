.. _windows:

********
windows
********

字体
=======

fonts

`Windows10字体渲染优化 <https://www.jianshu.com/p/7be5dca21094>`_ 解释了字体模糊的原因，字体渲染的修改


`如何在 Windows 上享受更棒的字体渲染 <https://sspai.com/post/52557>`_ 这个也解释了字体模糊的原因

比如一块 1920 x 1080 的 15.6 寸显示器，它的 PPI 就是 √(1920² + 1080²) / 15.6 = 141.21。从这个公式中可以看出「同等分辨率的屏幕越大，PPI 就越低」。

计算方法::

    import math

    # 台式机的ppi（Pixels Per Inch）：92.55912479337388
    math.sqrt(1920**2 + 1080**2) / 23.8
    
    # 笔记本的ppi（Pixels Per Inch）：165.6321180513006
    math.sqrt(1920**2 + 1080**2) / 13.3

**important**

windows系统下，字体渲染很容易模糊，没有好的解决方案

重置网络
=========

reset net

.. code-block::

    ipconfig/flushdns

    netsh winsock reset

