****************
Python 其他操作
****************

Python 终止程序
===============

在我自己使用的时候，几乎是所有情况下，我想终止程序都是通过

.. code-block:: python

    import sys
    sys.exit()

这种方式的。但是在 《Python Cookbook》里面看到另一种方式，嘛，其实也是本来就存在的方式——引发异常。只不过引发的这种异常以前没有用到过。

.. code-block:: python

    raise SystemExit()

注： ``raise SystemExit('It failed!')`` 这种方式中间可以产生自定义反馈信息。

后来越来越喜欢用第二种方式了...

英文字符串对齐
==============

取自 《Python Cookbook》

一般情况下，字符串对齐默认有 ljust(), rjust() 和 center() 三种方法。

如果不往这些函数中传递参数，则默认用空格填充，传进参数的情况下，则用参数填充。比如：

.. code-block:: bash

    >>> text = 'Hello World'
    >>> text.rjust(20)
    '         Hello World'
    >>> text.rjust(20, '-')
    '---------Hello World'

除此之外，还可以用 format 来进行对齐。默认对齐补充的字符为空格，左对齐，右对齐和居中分别对应三种字符 < > ^

直接看例子就知道 format 对齐的使用方式：

.. code-block:: bash

    >>> format(text, '>20')
    '         Hello World'
    >>> format(text, '->20s')
    '---------Hello World'
    >>> format(text, '-<20s')
    'Hello World---------'
    >>> format(text, '-^20s')
    '----Hello World-----'
