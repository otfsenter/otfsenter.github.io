.. _python-import-module-dynamic:

Python脚本动态导入模块
===================================

:ref:`wechat`

.. code-block:: python

    import sys
    from importlib import import_module
    import os

    # 把当前目录放入系统寻找模块的路径中
    sys.path.append(os.path.dirname(__file__))

    module = sys.argv[1]
    x = int(sys.argv[2])
    y = int(sys.argv[3])

    # 把模块弄成字符串，然后再当作模块导入
    my_module = import_module(module)

    # 使用模块中的函数
    a = my_module.add(x, y)

    # 输出结果
    print(a)
    
