.. _sphinx-pandoc:

pandoc
***********

to pdf
========


输出默认模板

.. code::

    pandoc -D latex > template.tex

在模板中找到"% if luatex of xetex" 下添加：

模板,仅供参考，很鸡肋

.. code::

  \usepackage{fontspec} 	% 允許設定字體
  \usepackage{xeCJK} 		% 分開設置中英文字型
  \setCJKmainfont{LiHei Pro} 	% 設定中文字型
  \setmainfont{Georgia} 	% 設定英文字型
  \setromanfont{Georgia} 	% 字型
  \setmonofont{Courier New}
  \linespread{1.2}\selectfont 	% 行距
  \XeTeXlinebreaklocale "zh" 	% 針對中文自動換行
  \XeTeXlinebreakskip = 0pt plus 1pt % 字與字之間加入0pt至1pt的間距，確保左右對整齊
  \parindent 0em 		% 段落縮進
  \setlength{\parskip}{20pt} 	% 段落之間的距離
  \ifxetex
    \usepackage{xltxtra,xunicode}
  \fi
  \defaultfontfeatures{Mapping=tex-text,Scale=MatchLowercase}
  \newcommand{\euro}{€}



转换的命令

.. code::

   pandoc -V CJKmainfont="Hiragino Sans GB" c.rst --pdf-engine=xelatex -o c.pdf

to docx
=======

simple

.. code-block::

   pandoc c.rst -o c.docx


稍微复杂一点的

.. code::

   pandoc -o c.docx -f rst+east_asian_line_breaks -s c.rst


markdown preview enhanced

convert markdown to docx by pandoc

.. code::

    ---
    title: "0-todo"
    author: zhouxinzheng
    date: June 19, 2021
    output: 
      word_document:
        pandoc_args: ["-o", "0-todo.docx", "-f", "markdown", "-s", "0-todo.md", "--reference-doc", "mystyles.docx"]
    ---
