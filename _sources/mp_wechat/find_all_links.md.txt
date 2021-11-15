# find all links

```python

"""
requests：爬网页的第三方模块
re：内置的正则表达式的模块
"""
import requests
import re

# 从交互命令行得到url
url = input('Enter a URL (include `http://`): ')

# 连接url
website = requests.get(url)

# 通过text属性得到网页源码
html = website.text

# 用re里面的findall匹配所有链接
links = re.findall('"((http|ftp)s?://.*?)"', html)

# 打印链接
for link in links:
    print(link[0])

```

执行脚本

```bash
$ python t.py
Enter a URL (include `http://`): https://www.baidu.com
```

输出结果

```
http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === 
```
