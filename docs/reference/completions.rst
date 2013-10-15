自动完成
===========

自动完成提供了像IDE那样的使用补全列表或者 :kbd:`Tab` 键插入动态内容的功能。

文件格式
***********

补全信息是以 ``.sublime-completions`` 作为扩展名的JSON文件。

补全列表的结构
*******************************

``scope``
	控制补全是否应该在这个文件中发挥作用。参考 :ref:`作用域与作用域选择子` 来了解更多信息。

``completions``
	补全的数组。

下面是从html补全列表中截取出来的一部分::

	{
		"scope": "text.html - source - meta.tag, punctuation.definition.tag.begin",

		"completions":
		[
			{ "trigger": "a", "contents": "<a href=\"$1\">$0</a>" },
			{ "trigger": "abbr", "contents": "<abbr>$0</abbr>" },
			{ "trigger": "acronym", "contents": "<acronym>$0</acronym>" }

		]
	}


补全的类型
********************

纯文本字符串
-------------

当某个补全项 ``trigger`` 的内容与 ``contents`` 的内容完全一样的时候，纯文本字符串与这个补全项
是等价的

	"foo"

	# 等价于：:

	{ "trigger": "foo", "contents": "foo" }

基于触发内容的补全
-------------------------

``trigger``
	在补全列表中显示的文本，在被确认后，对应的 ``contents`` 内容被插入到缓冲区中。

``contents``
	要插入到缓冲区中的文本。可以使用代码片段的特性。


补全的来源
***********************

用户可以控制的补全来源包括:

	* ``.sublime-completions``
	* ``EventListener.on_query_completions()``

除此之外，其他在最终补全列表中可以显示的内容包括：

	* Snippets
	* Words in the buffer

补全来源的优先级
-----------------------------------

	* 代码片段
	* 使用API插入的补全内容
	* ``.sublime-completions`` 文件
	* 缓冲区中的单词

代码片段只有在与设置的tab触发器精确匹配时才会被插入。其他类型的补全则是使用大小写不敏感的模糊
搜索进行匹配。


补全列表
*********************

要使用补全列表需要:

	* Press :kbd:`Ctrl+spacebar` 来打开补全列表
	* Optionally, 再次 press :kbd:`Ctrl+spacebar` 来选择下一个候选项
	* Press :kbd:`Enter` or :kbd:`Tab` 来确认选择

.. note::
	补全列表中被选中的当前项可以用任何没有被绑定到代码片段触发器中的标点符号来确认插入。


代码片段以如下形式出现在补全列表中：``<tab_trigger> : <name>`` 。对于其他补全项，你只能看到要被
插入的文本。


当补全列表被缩减到只有一个候选项时，系统就会绕开自动补全对话框，根据之前介绍的优先级，对应内容
会被直接插入。


为补全列表启用或禁用Tab补全
*****************************************************

``tab_completion`` 选项默认是 ``true`` 。如果你想停止 :kbd:`Tab` 键对最可能选项的索引功能，
就把这个值设置为 ``false`` 。这个设置项对定义在 ``.sublime-snippet`` 文件中的触发器没有效果，
因此按下 :kbd:`Tab` 时，代码片段一定会被插入。

当 ``tab_completion`` 选项开启的时候，上面介绍的优先级顺序仍然有效，但是，与补全列表不同的是，


插入一个Tab（缩进）字符
-----------------------

如果 ``tab_completion`` 值为 ``true`` ，你可以使用 ``Shift+Tab`` 来插入一个缩进字符
