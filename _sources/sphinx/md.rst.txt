.. _sphinx-md:

****************
include markdown
****************


module
=========

.. code::

    pip3 install m2r2


config
==========

.. code::

    extensions = ['m2r2']

    source_suffix = ['rst', 'md']


directives
=============

.. code::

    .. mdinclude:: t.md

ignore
==========

in index.st

.. code::

    .. toctree::
        :hidden:

        test.md

demo
=======

source/vim/test1.rst

source/vim/test.md
