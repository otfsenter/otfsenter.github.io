.. _vim-skill:

skill
============

打印出匹配的行
----------------

:g/sub_str/p


全局替换单词
---------------

先*找到，然后::

    :%s//<Ctrl-R><Ctrl-W>/g

每行自动递增序号
-----------------------

::

    :let i=1
    qa
    I<ctrl-r>=i<CR>) <ESC>
    :let i+=1
    q
    :%norm @a



插入模式删除字符、单词、行
----------------------------------

* delete letter

ctrl-h

* delete word

ctrl-w

* delete line

ctrl-u


插入-普通模式临时切换
------------------------------

::

    i
    <ctrl-o>zz


插入模式复制
-------------------

::

    <ctrl-r>0


二合字母
--------------

::

    :h digrahs-default

<ctrl-k>然后输入两个字母

命令模式的所有命令
-------------------

::

    :h ex-cmd-index


拼写检查
-------------------

set spell

set spelllang=en_us,cjk

set spellcapcheck=

插入模式下，<ctrl-x>s

.. csv-table::
    :header: command, description

    [s, 查找上一个拼写错误的
    ]s, 查找下一个拼写错误的
    z=, 普通模式，给出拼写提示
    zg, 添加到词典
    zw, 从词典删除
    zug, 撤销zg或zw的动作




