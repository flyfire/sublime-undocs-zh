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

This is a **key directory**: all resources for supported programming and
markup languages are stored here. A *package* is a directory containing
related files having a special meaning for Sublime Text.

You can access the packages directory from the main menu
(**Preferences | Browse Packages...**), or by means of an API call:
``sublime.packages_path()``. In this guide, we refer to this location as
*Packages*, *packages path*, *packages folder* or *packages directory*.

The ``User`` Package
^^^^^^^^^^^^^^^^^^^^

*Packages/User* is a catch-all directory for custom plugins, snippets,
macros, etc. Consider it your personal area in the packages folder. Sublime
Text will never overwrite the contents of *Packages/User* during upgrades.


The Python Console and the Python API
=====================================

This information is especially interesting for programmers. For other users,
you just need to know that Sublime Text enables users with programming skills
to add their own features to the editor. (So go learn how to program; it's
great fun!)

Sublime Text comes with an embedded Python interpreter. It's an useful tool
to inspect the editor's settings and to quickly test API calls while
developing plugins.

To open the Python console, press ``Ctrl+``` or select **View | Show Console**
from the main menu.

Confused? Let's try again more slowly:

*Python* is a programming language known to be easy for beginners and very
powerful at the same time. *API* is short for 'Application Programming
Interface', which is a fancy way of saying that Sublime Text 3 is prepared to
be programmed by the user. Put differently, Subime Text gives the user access
to its internals through Python. Finally, a *console* is a little window
inside Sublime Text that lets you type in short snippets of Python code and
run them. The console also shows text output by Sublime Text or its plugins.

Your System's Python vs the Sublime Text 3 Embedded Python
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. XXX Double check this
On **Windows** and **Linux**, Sublime Text 3 comes with its own Python
interpreter and it's separate from your system's Python installation.

On **OS X**, the system Python is used instead. Modifying your system version
of Python, such as replacing it with the MacPorts version, can cause problems
for Sublime Text.

The embedded interpreter is intended only to interact with the plugin API, not
for general development.


Packages, Plugins, Resources and Other Things That May Not Make Sense to You Now
================================================================================

Almost every aspect of Sublime Text can be tweaked, extended or customized.
This is all you need to understand for now. Well, that and that this vast
flexibility is the reason why you'll learn about so many configuration files:
there simply must be a place to specify all your preferences.

Among other things, you can modify the editor's behavior, add macros and
snippets, extend menus... and even create whole new features --where *feature*
means 'anything you can think of'. OK, right, there might be things you can't
do, but you're definitely spoiled for choice.

These configuration files are simple text files following a special structure
or *format*: JSON predominates, but you'll find XML files and Python files
too.

In this guide, for brevity we refer collectively to all these disparate
configuration files as *resources*.

Sublime Text will look for resources inside the packages folder. To keep
things tidy, the editor has a notion of a *package*, which is a folder
containing resources that belong together (maybe they all help compose emails
faster, write HTML efficiently, enhance the coding experience for C, Ruby,
Go...).


Textmate Compatibility
======================

This information is mainly useful for Textmate expats who've found a new home
in Sublime Text. Textmate is an editor for the Mac.

Sublime Text compatibility with Textmate bundles is good excluding commands,
which are incompatible. Additionally, Sublime Text requires all syntax
definitions to have the *.tmLanguage* extension, and all preferences files to
have the *.tmPreferences* extension. This means that *.plist* files will be
ignored, even if they are located under a *Syntaxes* or *Preferences*
subdirectory.


Vi/Vim Emulation
================

This information is mainly useful for dinosaurs and people who like to drop
the term RSI in conversations. Vi is an ancient modal editor that lets the
user perform all operations from the keyboard. Vim, a modern version of vi,
is still in widespread use.

Sublime Text provides vi emulation through the *Vintage* package. The Vintage
package is *ignored* by default. Read more about Vintage_ in the official
documentation.

An evolution of Vintage called Vintageous_ offers a better Vi editing
experience and is updated more often than Vintage. Vintageous_ is an open
source project, just as Vintage_.

.. _Vintage: http://www.sublimetext.com/docs/3/vintage.html
.. _Vintageous: http://guillermooo.bitbucket.org/Vintageous


Emacs
=====

This information is hardly useful for anyone. Emacs is... Well, nobody really
knows what emacs is, but some people edit text with it.

If you are an emacs user, you're probably not reading this.


Be Sublime, My Friend
=====================

Borrowing from `Bruce Lee's wisdom`_, Sublime Text can become almost anything
you need it to be. In skilled hands, blah, blah, blah.

Empty your mind; be sublime, my friend.

.. _Bruce Lee's wisdom: http://www.youtube.com/watch?v=7ijCSu87I9k
