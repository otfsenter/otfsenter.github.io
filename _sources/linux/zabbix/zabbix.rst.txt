.. _linux-zabbix:

****
main
****


install zabbix agent address
============================

https://github.com/dominicpratt/install-zabbix-agent

yum install -y postgresql-server postgresql-contrib

postgresql-setup initdb


systemctl start postgresql


systemctl enable postgresql

./configure --enable-server --with-postgresql --with-net-snmp

./configure --enable-server --with-postgresql=/usr/bin/pg_conf --with-net-snmp


