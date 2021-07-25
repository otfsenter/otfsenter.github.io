
# readthedocs


## 设置英文


先手动导入英文版本

生成英文版本的网页

```
make -e SPHINXOPTS="-D language='en'" html
```


项目名称：idlepig

语言：英语

branch：main

详细设置

* Settings

Name: idlepig-en

Repository URL: https://github.com/otfsenter/idlepig.git

Repository type: Git

Description: the blog of IdlePig

Language: English

Programming Language: Only Words

Tags: python, scripts

* Advanced Settings

Default version*: latest

Default branch: main

Analytics code: (apply from google ads)

Documentation type*: Sphinx Html

Python Interpreter*: Cpython 3.x

* Integrations

add by readthedocs automatically

* Translations

idlepig-en(English)






## 设置中文(只记录不同的地方)

项目名称：idlepig_zh-CN

语言：简体中文

branch：main

生成中文版本的网页

```
make -e SPHINXOPTS="-D language='zh_CN'" html
```

详细设置

* Settings

Language: Simplified Chinese



* Advanced Settings

Install Project

Python configuration file: source/conf.py

Enable PDF build: yes

Enable EPUB build: yes



## step 3

然后两个一起build

分别看一下两个文档是否正常

然后在英文文档项目里面设置翻译项：选择简体中文的版本

**这样最后只能在中文文档里面看到翻译选项，英文的看不到**