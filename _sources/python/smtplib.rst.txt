.. _python-smtplib:

用Python发送邮件
==========================

:ref:`wechat`

.. code-block:: python

    #!/usr/bin/env python
    # _*_ coding: utf-8 _*_
    # @Time     : 2017/11/1 15:13
    # @Author   : otfsenter
    # @File     : t123.py

    import smtplib
    from email.mime.multipart import MIMEMultipart
    from email.mime.text import MIMEText

    import my_key

    me = 'mail_address'
    you = ['mail_address1', 'mail_address2']
    text_file = '2.txt'

    msg = MIMEMultipart()
    msg['Subject'] = 'Subject'
    msg['From'] = me
    msg['To'] = ','.join(you)

    message = MIMEText('fp.read()')
    msg.attach(message)

    files = MIMEText(open('t.xls', 'rb').read(), 'base64', 'utf-8')
    files["Content-Type"] = 'application/octet-stream'
    files["Content-Disposition"] = 'attachment;filename="t.xls"'
    msg.attach(files)

    s = smtplib.SMTP('mail_host', 25)
    s.login(my_key.my_account, my_key.my_password)
    s.sendmail(me, you, msg.as_string())
    s.quit()


