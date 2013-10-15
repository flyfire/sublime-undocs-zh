构建系统
=============

构建系统可以让你通过外部程序来运行文件并且在Sublime Text中看到输出结果。

构建系统包括两个必要部分和第三个可选部分：

* JSON格式的配置数据(*.sublime-build*文件)
* 一个Sublime Text命令来驱动构建过程
* 可选，外部可执行文件(脚本，二进制文件)

从本质上讲，*.sublime-build*文件即是外部程序的配置数据也是前面提到的Sublime Text命令的配置。在其中，需要指定开关，选项，和要传入的环境配置信息。

然后Sublime Text命令从*.sublime-build*文件读取数据。此时，就可以做任何需要*构建*文件的事情了。默认情况下，构建系统会使用``exec``命令，由*Packages/Default/exec.py*中实现。 下面会提到，你可以重写此命令。

最后，外部程序可能是一个你写好的处理文件的shell脚本，或者一些著名的工具，比如``make``或者``tidy``。 通常，这些可执行文件都要接受文件或者目录路径， 开关和选项一起运行。

需要注意的是除非其它原因构建系统不需要调用外部程序；你完全可以通过Sublime Text command来实现一个构建系统。


文件格式
***********

*.build-system* JSON文件。下面是一个简单的示例：

.. sourcecode:: python

    {
        "cmd": ["python", "-u", "$file"],
        "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
        "selector": "source.python"
    }


选项(Options)
*******

``cmd``
    包含需要运行的命令和其参数的数组。如果不指定绝对路径，外部程序会从`PATH`环境变量中搜索。

    Windows下GUI会被抑制。

``file_regex``
    可选。获取``cmd``错误输出的正则表达式(Perl风格)。参看下一部分。

``line_regex``
    可选。If ``file_regex`` doesn't match on the current line, but
    ``line_regex`` exists, and it does match on the current line, then
    walk backwards through the buffer until a line matching ``file regex`` is
    found, and use these two matches to determine the file and line to go to.

``selector``
    可选。当**Tools | Build System | Automatic** 设为``true``时使用。
    Sublime Text在此范围内为当前的view选择合适的构建系统。

``working_dir``
    可选。 运行``cmd``前需要切换的当前目录。之后会恢复到原来目录。

``encoding``
    可选。``cmd``输出的编码。必须是有效的python编码字符。
    默认``UTF-8``。

``target``
    可选。 需要运行的Sublime Text命令。默认是``exec`` (*Packages/Default/exec.py*)。
    这个命令接受*.build-system*文件的配置数据。

    如果需要覆盖默认的命令来构建，需要在*.sublime-build*文件中指定你特有的变量。

``env``
    可选。 执行``cmd``需要合并进来的环境变量。

    可以使用它在不修改系统设置的情况下来添加或者修改环境变量。

``shell``
    可选。如果是``true``, ``cmd``会通过shell来运行(``cmd.exe``, ``bash``\ …)。

``path``
    可选。这个字符串在运行``cmd``前会替换系统变量：`PATH`。之后会把`PATH`恢复原值。

    可以使用这个选项在不修改系统设置的情况下，添加目录到`PATH`变量中。

``variants``
    可选。 字典列表，用于覆盖主构件系统的选项。Variant的``name`会显示在构建系统选择时命令面板上。

``name``
    **只在variant内有效** (参看``variants``)。标识variant构建系统。如果``name``是*Run*，这个variant将显示在**Tools | Build System**菜单下，并且绑定到*Ctrl + Shift + B*上。

使用``file_regex``获取错误输出
------------------------------------------

``file_regex``选项使用正则表达式来获取构建程序输出的错误信息的4个域，分别为：*file name*, *line number*, *column number* 和 *error message*。 可以通过匹配分组来获取这些信息。*file name*和*line number*是必须的。

当捕获到错误信息时，可通过``F4``和``Shift+F4``导航到项目文件的错误实例位置。如果有的话，*error message* 会显示在状态栏。

特定平台选项
-------------------------

可以使用``windows``, ``osx``和 ``linux``来指定特定平台的配置数据。下面是示例::


    {
        "cmd": ["ant"],
        "file_regex": "^ *\\[javac\\] (.+):([0-9]+):() (.*)$",
        "working_dir": "${project_path:${folder}}",
        "selector": "source.java",

        "windows":
        {
            "cmd": ["ant.bat"]
        }
    }

示例中，``ant``会在所有除了Windows之外的所有平台下执行，windows下则会执行``ant.bat``。

Variants
--------

下面是variants的示例::

    {
        "selector": "source.python",
        "cmd": ["date"],

        "variants": [

            { "cmd": ["ls -l *.py"],
              "name": "List Python Files",
              "shell": true
            },

            { "cmd": ["wc", "$file"],
              "name": "Word Count (current file)"
            },

            { "cmd": ["python", "-u", "$file"],
              "name": "Run"
            }
        ]
    }


上面这些配置，*Ctrl + B* 将运行*date*命令，*Crtl + Shift + B*将运行Python解析器并且其它的variants将在激活构建系统时出现在命令面板上。

.. _build-system-variables:

构建系统变量
**********************

构建系统会在*.sublime-build*文件中扩展下面这些变量：

====================== =====================================================================================
``$file_path``         当前文件目录，比如，*C:\Files*.
``$file``              当前文件完整路径，比如，*C:\Files\Chapter1.txt*.
``$file_name``         当前文件的完整文件名，比如，*Chapter1.txt*.
``$file_extension``    当前文件的扩展名，比如，*txt*.
``$file_base_name``    当前文件的名称，比如，*Document*.
``$packages``          *Packages*目录的完整路径。
``$project``           当前project文件完整路径.
``$project_path``      当前porject文件所在的完整目录。
``$project_name``      project文件的完整文件名。
``$project_extension`` 当前project文件的扩展名。
``$project_base_name`` 当前project文件的基本文件名。
====================== =====================================================================================

变量占位符
---------------------------

可以像下面这样使用这些变量::

    ${project_name:Default}

如果有的话将使用当前项目文件名，如果没有则使用``默认``。

::

    ${file/\.php/\.txt/}

把当前文正文件路径中*.php*替换成*.txt*。

运行构建系统
*********************

从**Tools | Build System**选择期望的构建系统，然后选择**Tools | Build**或者``F7``。


.. _troubleshooting-build-systems:

构建系统故障排除
*****************************

构建系统会在系统变量`PATH`路径下搜寻可执行文件，除非你指定了特定的可执行目录。所以，`PATH`系统变量要配置正确。

有些系统中，`PATH`变量的值在终端中与图形应用中会有不同。所有，尽管你在命令行中使用的构建命令运行正常，但也有可能在Sublime Text运行不正常。这跟用户的shell配置有关。

要解决这个问题，所有要确保你设定的`PATH`是期望的，让Sublime Text这种图形界面程序可以找到。参考下面的连接获取更多信息。

另外，也可以使用*.sublime-build*文件中的``path``配置项来指定`PATH`，不过这只在构建系统运行期间有效，运行完之后会恢复系统原来的值。

.. 参考::

    `Managing Environment Variables in Windows <http://goo.gl/F77EM>`_
        Search Microsoft knowledge base for this topic.

    `Setting environment variables in OSX <http://stackoverflow.com/q/135688/1670>`_
        StackOverflow topic.
