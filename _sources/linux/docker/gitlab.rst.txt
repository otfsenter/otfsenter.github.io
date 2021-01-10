.. _linux-docker-gitlab:

gitlab
==================


pull
-----------

.. code-block::

    docker pull gitlab/gitlab-ce

start container
-----------------------

.. code-block::

    docker run -itd --name gitlab -p 8080:80 gitlab/gitlab-ce

enter container
------------------------

.. code-block::

    docker exec -it gitlab /bin/bash

modify configuration
------------------------

.. code-block::

    vim /etc/gitlab/gitlab.rb to uncomment follow

    external_url 'http://idlepig.cn:8080'

start and reconfigure
---------------------------------

.. code-block::

    gitlab-ctl start
    gitlab-ctl reconfigure
