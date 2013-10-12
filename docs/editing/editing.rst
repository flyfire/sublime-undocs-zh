=======
编辑
=======

概述
========

Sublime Text充满着各种编辑功能。这里只粗浅的讲述下哪些是可以做的。

列选择
================

列选择可用于选择一个文件里的矩形区域。列选择并不是通过一个单独模式完成的，而是使用多重选择。

你可以添加选区域来选择多个文本块，或者减少选区来移除选择块。

使用鼠标
---------------

Windows

* 鼠标右键 ``+ ⇧ ``
* 或: 鼠标中键
\

* 添加到选区: ``Ctrl``
* 从选区移除: ``Alt``

Linux

* 鼠标右键 ``+ ⇧``
\

* 添加到选区: ``Ctrl``
* 从选区移除: ``Alt``

OS X

* 鼠标左键  + ``⌥``
* 或: 鼠标中键
\

* 添加到选区: ``⌘``
* 从选区移除: ``⌘ + ⇧``

使用键盘
------------------

Windows: ``Ctrl + Alt + Up`` and ``Ctrl + Alt + Down``

Linux: ``Alt + ⇧ + Up`` and ``Alt + ⇧ + Down``

OS X: ``⌃ + ⇧ + Up`` and ``⌃ + ⇧ + Down``

多区域选择
===================

多重选择可以让你有效率的进行大范围的文本修改。

对多重选择的任何赞美都过于轻淡了，这是因为：

你可以选择某个文本然后 ``Ctrl + D``  **添加更多** 实体(可参考 `官方文档部分 <http://feliving.github.io/Sublime-Text-3-Documentation/multiple_selection_with_the_keyboard.html>`_)。 如果想 **跳过当前实体**, 可以 ``Ctrl + K, Ctrl + D``。

如果选择过多, ``Ctrl + U`` 来 **取消选择** 当前实体。


把多选区分割成行
===========================================

``Ctrl + L`` 扩展选择到行。 ``Ctrl + Shift + L`` 把选区分割成行。

你可以把多重选择的行复制到一个单独的缓冲区，编辑它们，然后再复制编辑后的内容，然后把它们在原来的地方粘贴回去。像下面这样：

.. image:: /_images/copy_edit.gif

其它选择文本的方式
============================

The list is long; all available options can be found under **Selection**. To
name a few:

* Select subwords (``Alt + Shift + <arrow>``)
* Expand selection to brackets (``Ctrl + Shift + M``)
* Expand selection to indentation (``Ctrl + Shift + J``)
* Expand selection to scope (``Ctrl + Shift + Space``)


Transposing Things
==================

Need to swap two letters or, better yet, two words? Experiment with
``Ctrl + T``.


更多...
======================

The **Edit**, **Selection**, **Find** and **Goto** menus are good places to
look for handy editing tools. You might end up using just a few of them,
but the rest will still be there for when you need them.
