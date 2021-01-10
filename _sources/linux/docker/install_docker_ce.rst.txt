.. _linux-docker-install-docker-ce:

安装docker-ce
=========================


更改镜像源
----------------

.. code-block::

    cd /etc/apt/sources.list

把 archive.ubuntu 替换成  mirrors.aliyun

把 security.ubuntu 替换成 mirrors.aliyun

设置docker的安装源
--------------------------

.. code-block::

    # Install packages to allow apt to use a repository over HTTPS
    $ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    
    # Add Docker's official GPG key
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    # Set up the repository
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

    # Update source lists
    sudo apt-get update

    # Install Docker
    sudo apt-get install docker-ce


