# locale

## common usage

在source/locale目录下创建待翻译的文件

```
sphinx-build -b gettext . locale
```

更新中文 -> 英文的翻译文件

```
sphinx-intl update -p locale -l en
```

<s>更新英文 -> 中文的翻译文件，一般不需要</s>

```
sphinx-intl update -p locale -l zh_CN
```


## 官方链接

https://www.sphinx-doc.org/en/master/usage/advanced/intl.html

https://docs.readthedocs.io/en/stable/localization.html


