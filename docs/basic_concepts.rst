==============
基本概念
==============

概述
========

为了能更清晰完整的明白整个文档手册，你需要熟悉一下本小节中提到的概念。


约定
===========

我们从一个Windows用户的视角来编写文档，大部分说明只需要一点小变化就可适用于其它平台。

相对路径, 比如 *Packages/User*, 如果没有特定说明的话都是开始于 *data目录*。 *data目录* 后面会说明。

当提到快捷键时我们都假定默认的键盘绑定。
如果你适用non-English键盘布局，注意 **有一些键盘绑定与你的键盘区域不匹配**。这要归结于Sublime Text命令的按键映射。


因强大而引发的一些问题
=========================================

对于编程人员来说它无疑是一个多功能的工具，你不需要为了某一个功能而去使用Sublime Text，也不需要做很多配置。如果你是一个hacker，它将会给你带来很多惊喜。

Sublime Text可以无限制的自定义和扩展。在它原始的状态下你也可以非常有效率的开始使用它，不过花一些时间来定制它，以满足更精确的需求，给你带来的好处将会远超过你花费的精力。

这部手册将会教你如何配置Sublime Text。

你不用一天就掌握Sublime Text，不过它是一个基于随处渗透着一致性和易于理解的指导思想构建起来的额系统。

后面几个段落中，我们将会介绍几个关键点，会令你在花了一点时间使用该编辑器之后心旷神怡。乐于尝试，随手翻阅这部手册，最后一切都会水到渠成。


*Data* 目录
====================

基本上所有与用户相关的文件都在data目录下。
根据系统平台的不同：

* **Windows**: *%APPDATA%\\Sublime Text 3*
* **OS X**: *~/Library/Application Support/Sublime Text 3*
* **Linux**: *~/.config/sublime-text-3*

如果是 **portable installations(便携安装的版本)**, 在子目录 *Sublime Text 3/Data*下。这里 *Sublime Text 3* 指的是你解压的便携式压缩包的目录。

注意之后便携式版本有 *Data*子目录。
其它安装版本，data目录在上面对应的位置。


*Packages* 目录
==============================

这是一个 **关键目录**: 所有用于支持编程和标记语言的资源都存放在这里。一个 *package* 就是一个包含对于Sublime Text有特定意义文件的目录。

你可以通过(**Preferences | Browse Packages...**)菜单来访问packages目录，或者通过API调用：
``sublime.packages_path()`` 。在这部手册中，我们把它定义为这个路径定义为 *Packages*, *packages path*, *packages folder* 或者 *packages directory*。

``User`` 包
^^^^^^^^^^^^^^^^^^^^

*Packages/User* 是一个包含自定义插件(plugins)，代码片段(snippets)，宏命令(macros)之类的目录。可以把它认为是在packages目录下你的个人区域。Sublime Text在更新时将不会覆盖 *Packages/User* 下的内容。


Python 控制台和 Python API
=====================================

这部分信息可能对于编程人员来说比较感兴趣。对已其它用户来说，你只需要知道Sublime Text允许用户利用他们的编程技能来给编辑器添加他们自己的特性。(所以学会编程吧，它真的很有趣！)

Sublime Text 内嵌了一个Python解析器。它是一个非常有用的工具，可用于检查编辑器的配置，开发插件时可用于快速的测试API调用。

要打开Python控制台，``Ctrl+``` 或者通过菜单 **View | Show Console** 。

还是困惑? 那我们慢点来讲述下：

*Python* 是一个对于初学者来说容易上手且强大的编程语言。 *API* 是'Application Programming
Interface'的简称，换句话说Sublime Text 3就是用这种方式为用户提供可编程性。Subime Text让用户通过Python来访问其内部。*console(控制台)* 是Sublime Text内的一个小窗口，你可以输入Python代码并运行它们。控制台同时也会显示Sublime Text或者其插件的输出。

系统的Python vs Sublime Text 3内置的Python
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. XXX Double check this
在 **Windows** 和 **Linux**下，Sublime Text 3有它自己的Python解析器，而且是与系统安装的Python是分开的。

**OS X** 下使用的是系统给的Python。修改系统的Python版本，比如替换成MacPorts版本，将会导致Sublime Text出问题。

内置的解析器仅是为与插件API交互而准备的，而不是为一般性编程准备的。


Packages, Plugins, Resources以及其它一些你现在可能还能用得上的东西
================================================================================

几乎Sublime Text的所有方面都可以被修改，扩展和自定义。这一点你现在必须明白。
正因为其广大的灵活性，所以你现在需要学些这么多的配置文件：必须要有个地方来指定你的偏好。

此外，你可以修改编辑器的行为，添加macros(宏命令)和代码片段，扩展菜单...甚至是创建一个全新的特性 -- *特性* 的意思就是 '所有你能想到的'。好了，或许有些事情你是不能做的，不过这已经足够你选择了。

这些配置文件是JSON *格式*的普通文本文件，不过同时你也会发现XML文件和Python文件。

在这部手册中，我们统一把这些配置文件定义为 *resources(资源)*。

Sublime Text会检查packages目录下的资源文件。为了整洁，编辑器有一个 *package(包)*的概念，它是一个把资源文件(它们可能适用于帮助编写邮件，更高效的编写HTML，提升C,Ruby,Go代码编写体验等等)归档在一起的目录。


Textmate兼容性
======================

这部分信息可能对于丢弃Textmate，在Sublime Text中找到一个全新世界的人来说比较有用。Textmate是Mac下的一个编辑器。

Sublime Text与Textmate兼容的非常好，除了命令之外。另外，Sublime Text要求所有语法定义 *.tmLanguage*为格式，所有偏好设置文件为 *.tmPreferences* 格式。这意味着 *.plist* 文件将会被忽略，尽管它们放在 *Syntaxes* 或者 *Preferences* 子目录下。


Vi/Vim 仿真
================

这部分信息主要对恐龙或者那些比较喜欢与RSI术语打交道的人来说有用。
Vi是一个可以让用户所有操作都通过键盘来完成的古老的编辑器。Vim, 是vi的一个更现代的版本，仍然在广泛使用。

Sublime Text通过 *Vintage* 包提供里vi仿真。Vintage包默认是 *ignored* 。可以在官方文档中阅读更多关于 Vintage_ 的信息。

一个Vintage变种，Vintageous_ 提供了更好的Vi编辑体验而且比Vintage更新更频繁。 Vintageous_ 是一个开源项目。

.. _Vintage: http://feliving.github.io/Sublime-Text-3-Documentation/vintage.html
.. _Vintageous: http://guillermooo.bitbucket.org/Vintageous


Emacs
=====

这部分信息对于所有人都很难有点用处。Emacs这玩意...，没人真的知道emacs是啥，不过确实有些人用它来编辑文本。

如果你是一个emacs用户，你可能就不会阅读这些内容了。


用Sublime吧，骚年
=====================

借用下 `Bruce Lee's wisdom`_, Sublime Text can become almost anything
you need it to be. In skilled hands, blah, blah, blah.

Empty your mind; be sublime, my friend.

.. _Bruce Lee's wisdom: http://www.youtube.com/watch?v=7ijCSu87I9k
