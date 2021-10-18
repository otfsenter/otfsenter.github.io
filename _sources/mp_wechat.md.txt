
# wechat official account


## re.split


* 目的

对 line 字符串进行分割，取出每个单词

预计的结果如下:

```python
["Hi", "John", "Kennedy", "Glad", "to", "see", "you"]
```



* 参数说明

`re.split()` 函数一般需要接收两个参数，

第一个参数：正则表达式

第二个参数：字符串

* 方括号

```python
import re

line = 'Hi John Kennedy! Glad to see you'
result = re.split(r'[\s!]', line)
print(result)
```

result

```python
["Hi", "John", "Kennedy", "", "Glad", "to", "see", "you"]
```


第一个参数：`r'[\\s!]'`

在正则表达式中，会匹配方括号中任意一个字符，缺点是不能 以多个字符 为一个单元 作为分隔符，并且是或的关系

结果中也有一个空字符串


* 圆括号

```python
result = re.split(r'(!\s|\s)', line)
print(result)
```

result

```python
['Hi', ' ', 'John', ' ', 'Kennedy', '! ', 'Glad', ' ', 'to', ' ', 'see', ' ', 'you']
```

圆括号可以 用多个字符作为一个分隔符，并且匹配任意一个，

在这里面，就是匹配 !\s 或 \\s 其中任意一个

但是会输出分隔符本身    


* 非捕获组

```python
result = re.split(r'(?:!\s|\s)', line)
print(result)
```

result

```python
['Hi', 'John', 'Kennedy', 'Glad', 'to', 'see', 'you']
```

这个时候就可以用正则表达式里面的 非捕获组（会把匹配上的字符忽略掉），

具体的表现形式是在 圆括号 里面的 最前面 加上 ``?:``

这样结果就会去掉分隔符

达到我们的目的

当然，方法不止一种

```python
result = re.split(r'!\s|\s', line)
print(result)
```

result

```python
['Hi', 'John', 'Kennedy', 'Glad', 'to', 'see', 'you']
```


直接用 | 分割 字符串 ，放入 !\s 和 \\s 也能达到效果

灵活的运用正则表达式，就能对字符串做出各种处理。
