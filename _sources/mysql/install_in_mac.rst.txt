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



modify password


.. code::

    SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpass');


if mysql installed


.. code::

    brew link --overwrite mysql

if error happened

.. code::

    sudo chown -R '${username}' /usr/local

    unset TMPDIR

    bash mysql_install_db --verbose --user=root
    --basedir="$(brew --prefix mysql)"--datadir=/usr/local/var/mysql --tmpdir=/tmp


unset auth

update mysql.user set authentication_string=null where User='tag';

ALTER USER 'tag'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'ms88888888';
