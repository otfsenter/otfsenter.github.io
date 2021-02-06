.. _vim_skill:

*****
skill
*****

youcompleteme
=============

.. code::

    mkdir -p ~/.vim/bundle/YouCompleteMe/third_party/ycmd/clang_archives

    mv  clang+llvm-*-x86_64-apple-darwin.tar.xz ~/.vim/bundle/YouCompleteMe/third_party/ycmd/clang_archives

download url

https://releases.llvm.org/download.html


lang+llvm-5.0.0-x86_64-apple-darwin.tar.xz


.. code::

    cd ~/.vim/bundle/YouCompleteMe
    ./install.py --clang-completer

config

.. code::

    "默认配置文件路径"
    let g:ycm_global_ycm_extra_conf = '~/.ycm_extra_conf.py'
    "打开vim时不再询问是否加载ycm_extra_conf.py配置"
    let g:ycm_confirm_extra_conf=0
    set completeopt=longest,menu
    "python解释器路径"
    let g:ycm_path_to_python_interpreter='/usr/local/bin/python'
    "是否开启语义补全"
    let g:ycm_seed_identifiers_with_syntax=1
    "是否在注释中也开启补全"
    let g:ycm_complete_in_comments=1
    let g:ycm_collect_identifiers_from_comments_and_strings = 0
    "开始补全的字符数"
    let g:ycm_min_num_of_chars_for_completion=2
    "补全后自动关机预览窗口"
    let g:ycm_autoclose_preview_window_after_completion=1
    " 禁止缓存匹配项,每次都重新生成匹配项"
    let g:ycm_cache_omnifunc=0
    "字符串中也开启补全"
    let g:ycm_complete_in_strings = 1
    "离开插入模式后自动关闭预览窗口"
    autocmd InsertLeave * if pumvisible() == 0|pclose|endif
    "回车即选中当前项"
    inoremap <expr> <CR>       pumvisible() ? '<C-y>' : '\<CR>'
    "上下左右键行为"
    inoremap <expr> <Down>     pumvisible() ? '\<C-n>' : '\<Down>'
    inoremap <expr> <Up>       pumvisible() ? '\<C-p>' : '\<Up>'
    inoremap <expr> <PageDown> pumvisible() ? '\<PageDown>\<C-p>\<C-n>' : '\<PageDown>'
    inoremap <expr> <PageUp>   pumvisible() ? '\<PageUp>\<C-p>\<C-n>' : '\<PageUp>'


rstcheck ignore notice
===============================

vi ~/.rstcheck.cfg

.. code::

    [rstcheck]
    report=warning

settings for find python error automatically
================================================

environment settings
--------------------


.. code::

    export LC_CTYPE="en_US.UTF-8"
    export LANG="en_US.UTF-8"


custom python compiler
----------------------

* python.vim path

    ~/.vim/compiler/python.vim

* windows python vim path

    D:\\Vim\vim82\\compiler\\python.vim


* python.vim code

.. code-block:: python

    if exists("current_compiler")
        finish
    endif
    let current_compiler = "python"

    let s:cpo_save = &cpo
    set cpo&vim

    CompilerSet errorformat=
        \%*\\sFile\ \"%f\"\\,\ line\ %l\\,\ %m,
        \%*\\sFile\ \"%f\"\\,\ line\ %l,

    if g:iswindows
        CompilerSet makeprg=python\ %
    else
        CompilerSet makeprg=python3\ %
    endif

    let &cpo = s:cpo_save
    unlet s:cpo_save

vimrc config
------------

.. code::

    " F5 run python scripts
    set makeprg=python3\ %
    autocmd filetype python nmap <F5> :w!<CR>:compiler python<CR>:make <bar> copen<CR>


fold keymap
================================

.. csv-table::
    :header: keymap, meaning

    za,toggle
    zc,close
    zo,open
    zf,fold
    zM,fold all
    zR,unfold all


打印出匹配的行
================================

:g/sub_str/p


全局替换单词
================================

先*找到，然后::

    :%s//<Ctrl-R><Ctrl-W>/g

每行自动递增序号
================================

::

    :let i=1
    qa
    I<ctrl-r>=i<CR>) <ESC>
    :let i+=1
    q
    :%norm @a



插入模式删除字符、单词、行
================================

* delete letter

ctrl-h

* delete word

ctrl-w

* delete line

ctrl-u


插入-普通模式临时切换
================================

::

    i
    <ctrl-o>zz


插入模式复制
================================

::

    <ctrl-r>0


二合字母
================================

::

    :h digrahs-default

<ctrl-k>然后输入两个字母

命令模式的所有命令
================================

::

    :h ex-cmd-index


拼写检查
================================

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
