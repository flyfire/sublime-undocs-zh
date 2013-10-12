==================
搜索和替换
==================

Sublime Text提供2种类型的搜索：

.. toctree::
   :maxdepth: 1

	搜索 - 单个文件 <search_and_replace>
	搜索 - 多文件 <search_and_replace_files>

我们将依次讲解它们，不过我们先讲下一个强大的搜索利器：正则表达式。

.. _snr-regexes:

正则表达式
===================

正则表达式可查找文本中的 *复杂模式*。要全面的掌握Sublime Text的搜索功能，你至少应该学会基本的正则表达式。本手册中我们不讲解如何使用正则表达式。


下面就是一个正则的样子::

	(?:Sw|P)i(?:tch|s{2})\s(?:it\s)?of{2}!

正则以令人痛苦而出名。

要使用正则，首先你要在搜索面板的模式中激活它。否则，搜索词将按字面意思查找。

Sublime Text使用正则表达式中的 `Boost语法`_ 。

.. _Boost语法: http://www.boost.org/doc/libs/1_47_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html

（译者注：正则表达式有很多类型的方言）