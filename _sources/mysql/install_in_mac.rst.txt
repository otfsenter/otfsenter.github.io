.. _mysql-install-in-mac:


********************
install mysql in mac
********************


.. code::

    brew install mysql-connector-c

    brew install mysql

To connect run:

.. code::

    mysql -uroot

To have launchd start mysql now and restart at login:

.. code::

    brew services start mysql

Or, if you don't want/need a background service you can just run:

.. code::

    mysql.server start



