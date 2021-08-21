*******************
Python 启动其他程序
*******************

打开计算器
==========

.. code-block:: python3

    import subprocess
    subprocess.Popen(r'C:\Windows\System32\calc.exe')

打开记事本
==========

.. code-block:: python3

    import subprocess
    subprocess.Popen(r'C:\Windows\System32\notepad.exe')

用指定程序打开特定文件
======================

用记事本打开当前路径下的 hello.txt 文本

.. code-block:: python3

    import subprocess
    subprocess.Popen([r'C:\Windows\System32\notepad.exe', 'hello.txt'])

用 sublime text 3 打开当路径下的 python 脚本

.. code-block:: python3

    import subprocess
    subprocess.Popen(['D:\Program Files\Sublime Text 3\sublime_text.exe', 'hello.py'])

用 sublime text 3 打开目标文件夹

.. code-block:: python3

    import subprocess
    subprocess.Popen(['D:\Program Files\Sublime Text 3\sublime_text.exe', r'C:\Users\Administrator\Desktop'])

.. hint:: 以上例子如果没有目标文件(夹)，就会报错。列表中的第一个参数是程序的绝对路径，第二个参数为目标文件(夹)。

用默认程序打开文件
==================

用默认程序打开当前路径下的 hello.txt 文本。以下代码基于 windows。

.. code-block:: python3

    import subprocess
    subprocess.Popen(['start', 'hello.txt'], shell=True)
