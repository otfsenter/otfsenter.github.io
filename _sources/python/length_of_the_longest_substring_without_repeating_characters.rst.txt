.. _python-length-of-the-longest-substring-without-repeating-characters:


********************************************************************
没有重复字母的最长子字符串的计算
********************************************************************

length of the longest substring without repeating characters


代码
=====

时间复杂度：O(n+d) ，其中n为输入字符串的长度，d为输入字符串字母表的字符数。

例如，如果字符串由小写英文字符组成，那么d的值是26。

空间复杂度：O(d) 。


.. code-block:: python

    # Here, we are planning to implement a simple sliding window methodology 

    def longestUniqueSubsttr(string): 
        
        # Creating a set to store the last positions of occurrence 
        seen = {} 
        maximum_length = 0

        # starting the inital point of window to index 0 
        start = 0
        
        for end in range(len(string)): 

            # Checking if we have already seen the element or not 
            if string[end] in seen: 

                # If we have seen the number, move the start pointer 
                # to position after the last occurrence 
                start = max(start, seen[string[end]] + 1) 

            # Updating the last seen value of the character 
            seen[string[end]] = end 
            maximum_length = max(maximum_length, end-start + 1) 
        return maximum_length 

    # Driver Code 
    string = "geeksforgeeks"
    print("The input string is", string) 
    length = longestUniqueSubsttr(string) 
    print("The length of the longest non-repeating character substring is", length) 

如何算最大的长度
==================

子字符串长度 = 末尾的索引 - 开始的索引 + 1

末尾的索引：end

开始的索引：start

这样只要遍历不重复的字符串长度，然后用max保存最大的值就行

maximum_length=max(maximum_length, end - start + 1)

end怎么来的
============

每次遍历的索引值就是end

start怎么来
=============

弄一个字典，记录每个字母对应索引，如果重复了，就更新字母对应的索引位置


为什么start也要max
===================

.. csv-table::
    :header: g, e, e, k, s, f, o, r, g, e, e, k, s

    0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12

当第二次g出现的时候，start=0+1=1，

但其实e已经出现了两次，start=2了，

这样会从第一个e开始算，导致出现问题

为什么maximum_length也要用max
================================

为了保存最大值

start为什么不直接用end
==========================

用了end之后start，end值的变化如下：

.. code-block:: python

    [0, 0],
    [0, 1],
    [2, 2],
    [2, 3],
    [2, 4],
    [2, 5],
    [2, 6],
    [2, 7],
    [8, 8],
    [9, 9],
    [10, 10],
    [11, 11],
    [12, 12]

.. csv-table::
    :header: g, e, e, k, s, f, o, r, g, e, e, k, s

    0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12

.. csv-table::
    :header: 字母, 第一次, 第二次

    g, 0, 8
    start，end, start=0，end=0, start=8，end=8
    e, 1, 2
    start，end, start=0，end=1, start=2，end=2

第二个g，

到g的时候，上次start=2，end=7，最大长度就是6，

一旦到g，start=8，end=8，其实这里第二个e到第二个g，最大长度是7，这样就出现了问题，少算了第二个g，导致少了1位。

为什么start用的是上一次的值+1
===============================


这就相当于如果后面有重复，就去掉第一个重复的值，从第二个开始，

比如gekga

就相当于去掉第一个g，从ekga计算

start，end值的变化如下：


.. code-block:: python

    [0, 0],
    [0, 1],
    [2, 2],
    [2, 3],
    [2, 4],
    [2, 5],
    [2, 6],
    [2, 7],
    [2, 8],
    [3, 9],
    [10, 10],
    [10, 11],
    [10, 12]

.. csv-table::
    :header: g, e, e, k, s, f, o, r, g, e, e, k, s

    0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12

g第一次出现是0，第二次出现, 在第一次出现的基础上+1，start=1，但其实这里包含了两个重复的e,

但是e已经出现了两次，start=2，

取最大值，start=2，

end是8，算出来最大值8-2+1=7


解耦
=====

* 得先解决一个特定的问题，循环中的一个例子
* 每个阶段一个py文件，一个日志文件，最好是csv文件，方便整理成任何想要的格式，或者“｜｜”分隔，也方便整理，方便分阶段调试
* 每个阶段通过输出的文件连接，方便解耦
* 每个功能一个函数
* 最后输出到文件里面，一定要有日志，方便随时断开，随时从有问题的地方开始
* 最后整理的配置文件一定是从日志生成，不能依赖程序执行完生成配置文件