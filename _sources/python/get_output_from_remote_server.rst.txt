.. _python-get-output-from-remote-server:

**************************************
获取远程服务器上面的输出
**************************************


.. code-block:: python

    stdin, stdout, stderr = ssh.exec_command('python -u /home/user/test.py')
    for line in stdout:
        print line.rstrip()