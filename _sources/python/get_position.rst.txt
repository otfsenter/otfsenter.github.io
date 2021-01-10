.. _get-postion:

获取鼠标的实时坐标
==========================

:ref:`wechat`


.. code-block:: python

    import win32api
    import time

    while 1:
        time.sleep(1)
        x, y = win32api.GetCursorPos()
        print('{}, {}'.format(x, y))

