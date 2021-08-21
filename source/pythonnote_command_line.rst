*****************
Python 命令行参数
*****************

编写属于自己的全局命令(最小实现)
================================

以在 windows 下编写一个极简的 ls 命令为例

1.新建以下的文件和文件夹
------------------------

.. code-block:: bash

    ─mycmds
    │  │  setup.py
    │  │
    │  └─mycmds
    │      │  __init__.py
    │      │
    │      └─commands
    │              ls.py
    │              __init__.py

2.编写代码
----------

.. code-block:: python

    # mycmds/setup.py
    import setuptools

    setuptools.setup(
        name="mycmds",
        version="0.0.1",
        author="",
        author_email="",
        description="",
        packages=setuptools.find_packages(),
        include_package_data=True,
        entry_points={
            "console_scripts": [
                "ls=mycmds.commands.ls:main",
            ]
        },
    )

.. code-block:: python

    # mycmds/mycmds/__init__.py
    from . import commands

.. code-block:: python

    # mycmds/mycmds/commands/__init__.py
    from . import ls

.. code-block:: python

    # mycmds/mycmds/commands/ls.py
    import os
    import argparse


    def main():

        parser = argparse.ArgumentParser(description='A ls command on windows')

        parser.add_argument('path', nargs='?',
                            help='the path to list files, default .')
        parser.add_argument('-l', '--list', action='store_true',
                            help='list per file in new line')

        args = parser.parse_args()

        path = args.path
        if path is None:
            path = os.path.abspath('.')

        file_list = os.listdir(path)

        if args.list:
            for each in file_list:
                print(each)
        else:
            print('  '.join(file_list))

    if __name__ == '__main__':
        main()

3.安装 mycmds
---------------

切换到 setup.py 的路径下，运行

.. code-block:: bash

    python setup.py install


4.测试
------

安装完成后，可以在命令行开始测试了。输入

.. code-block:: bash

    ls -h

就能看到以下结果：

.. code-block:: bash

    usage: ls.py [-h] [-l] [path]

    A simple command to show the list of files in target path

    positional arguments:
      path        the path to show the files

    optional arguments:
      -h, --help  show this help message and exit
      -l          each one print in a new line

在 windows 下的 console 窗口中，能直接调用的是后缀名为 exe 的文件。只有 exe 才能全局调用。单纯编写 ls.py 可以在该文件所在的路径下直接通过 ``python ls.py`` 来使用命令行参数，想全局调用恐怕得用 ``python [ls.py path]`` 这种绝对路径的方式。

通过写成 package 打包安装有个很明显的好处，就是会自动在 python 路径下一个文件夹里生成 .exe 文件，这个文件夹所在路径是加入到 path 路径中的，所以我们可以在 ``win+r`` 或者 ``win+r cmd`` 里全局使用，方便了相当多。
