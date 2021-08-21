***************
Python 文件操作
***************

CSV 文件读写
=============

写入数据
--------

.. code-block:: python

    import csv
    with open('target.csv', 'w', encoding='utf-8', newline='')as fl:
        writer = csv.writer(fl)
        writer.writerow((1, 2, 3))
        writer.writerow((4, 5, 6))


.. hint:: 如果不加 ``newline=''`` 的话，目标文件将会写一行空一行。


读取数据
--------

.. code-block:: python

    with open('target.csv', encoding='utf-8', newline='')as fl:
        reader = csv.reader(fl)
        for row in reader:
            print(row)

控制台输出

.. code-block:: bash

    ['1', '2', '3']
    ['4', '5', '6']


Excel 文件读写
==============

写入数据
--------

.. code-block:: python

    import openpyxl

    filename = 'target.xlsx'
    wb = openpyxl.Workbook()
    ws = wb.active

    ws.append([1, 2, 3])
    ws.append([4, 5, 6])

    wb.save(filename)


读取数据
--------

.. code-block:: python

    import openpyxl

    filename = 'target.xlsx'
    wb = openpyxl.load_workbook(filename)
    ws = wb.active

    for row in ws.iter_rows():
        print([cell.value for cell in row])

    # 另一种常用的读取方式，用来读取特定的列的值
    # 上面的这种感觉多数情况下要去掉第一行标题行
    # 需要增加一些额外的代码。可以直接用 enumerate
    # for row in range(2, ws.max_row + 1):
    #     ws.cell(row=row, column=xxx)

    wb.close()

.. code-block:: bash

    [1, 2, 3]
    [4, 5, 6]


Json 文件读写
=============

将字典数据写进 json 文件
------------------------

.. code-block:: python

    import json
    month = {
        'Jan': '一月',
        'Feb': '二月',
        'Mar': '三月'
    }
    with open('target.json', 'w', encoding='utf-8')as fl:
        json.dump(month, fl, indent=4, ensure_ascii=False)

打开 target.json 文件，我们可以看到文件中的内容

.. code-block:: json

    {
        "Jan": "一月",
        "Feb": "二月",
        "Mar": "三月"
    }

.. note:: ``ensure_ascii=False`` 可以防止写进文件之后中文乱码，``indent=4`` 将缩进设置为 4 比较符合我们平常的观察习惯。


读取 json 文件内容
------------------

.. code-block:: python

    with open('target.json', encoding='utf-8')as fl:
        data = json.load(fl)
    print(data)

.. code-block:: bash

    {'Jan': '一月', 'Feb': '二月', 'Mar': '三月'}

创建文件夹
==========

创建文件夹的两个命令


第一个命令：

.. code-block:: python

    os.mkdir(path)

第二个命令：

.. code-block:: python

    os.makedirs(path)


``os.mkdir(path)`` 这个语句可以创建一个文件夹，当 path 有多层路径时，只要当中有一层路径是不存在的话，就会产生异常。

``os.makedirs(path)`` 这个语句可以创建一个文件夹，当 path 有多层路径时，无论有多少层，该语句会一直创建知道最后一层文件夹创建完成。

两个命令有这不同的应用场景，自己使用时很容易知道在什么时候用哪个比较好。但是要总结，一时间却不知道该如何说起。

复制，重命名，删除文件和文件夹
==============================

.. code-block:: python

    import os
    improt shutil
    
    # 复制文件
    shutil.copy(src, dst)
    # 复制非空文件夹
    shutil.copytree(src, dst)

    # 移动，重命名文件(夹)
    shutil.move(src, dst)

    # 删除文件
    os.remove(path)
    # 删除非空文件夹
    shutil.rmtree(path)

.. note:: 在使用删除命令时需要特别小心，os, shutil 在删除目标是后台删除，没有去到回收站，无法恢复！！！使用这个最好保证原来的数据有备份，随时可以重来。有个第三方包 send2trash 可以将删除的对象送到回收站的，需要的话可以看一下这个包。
