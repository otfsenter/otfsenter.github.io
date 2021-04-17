.. _linux-commands:

********
commands
********

refresh crontab in multiple servers

.. code-block::

    ssh 10.1.2.3 "crontab -l > /tmp/crontab && cp /tmp/crontab /tmp/crontab.20210417 && sed -i '/alarm_history/d' /tmp/crontab && echo '* * * * * sh /opt/idlepig/shell/t.sh >/dev/null 2>&1' >> /tmp/crontab && crontab /tmp/crontab"

