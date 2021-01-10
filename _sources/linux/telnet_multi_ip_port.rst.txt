.. _telnet-multi-ip-port:

**************************************
telnet多个IP和端口
**************************************


telnet的结果，如果是错误，丢弃，
如果是正常的输出，附加到1.txt，
然后等待2秒，直接kill掉当前telnet的进程，
而且是在后台kill掉的。

.. code-block:: shell

    #!/bin/sh


    for i in `cat ip1`
    do
        echo $i
        telnet $i 22022 >>1.txt 2>/dev/null & (sleep 2; kill $!)&
    done