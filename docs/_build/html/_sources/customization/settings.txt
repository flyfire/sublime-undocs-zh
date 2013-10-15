========
配置
========

Sublime Text把配置信息保存在 *.sublime-settings* 文件中。为了拥有较好的灵活性，作为代价，
需要一个略显繁琐的系统来管理配置项。我们先来说一条基本原则吧：

个人定义的配置项文件一定要保存到 *Packages/User* 目录下，这样就能保证在发生冲突的时候，你定
义的文件拥有较高的优先级。

那咱们就来揭开配置项工作的具体原理了，从而满足部分喜欢受虐读者的需求。


格式
======

配置项文件是以 *.sublime-settings* 作为扩展名的的JSON文件。


配置文件的类型
=================

可以通过 *.sublime-settings* 文件的名字看出它的用途。这些文件的名字可能具有一定的描述性（例如
*Preferences (Windows).sublime-settings* 或者 *Minimap.sublime-settings*），亦或是跟
它所控制的内容有关联。以控制文件类型的配置项文件为例，命名时要求必须有与之对应的 *.tmLanguage*
语法定义文件。因此，对于 *.py* 文件类型，它的语法定义信息存放在 *Python.tmLanguage* 文件中，
那么对应的文件类型配置项文件就该被叫做 *Python.sublime-settings* 。

除此之外，某些配置文件只能作用于某个特定的平台。可以通过文件名进行推断，例如：
*Preferences (Windows).sublime-settings* 和 *Preferences (Linux).sublime-settings* 。

有一点特别 **重要** ：存放在 *Packages/User* 目录中的平台相关的配置文件将被忽略。通过这种方式，
就可以保证单个配置文件内容可以覆盖其他所有配置文件的内容了。


如何访问并修改公共的配置文件
============================================

除非你对配置项有非常精确的掌控力，否则，你只需要通过 **Preferences | Settings - User** 和
**Preferences | Settings - More** 菜单项来访问主要的配置文件。编辑
**Preferences - Settings Default** 这个文件并不是一件明智的事情，因为每次版本升级这些修改都
将被重置。不过，你确实可以把这些文件当作一个不错的参考资料：默认配置项文件里面包含了解释所有能
为你所用的全局配置项和文件类型配置项的说明注释。


*.sublime-settings* 文件的优先级顺序
==================================================

名字相同的配置项文件（例如，都叫 *Python.sublime-settings* 的文件）可以在多个位置出现。以相同
名称命名的配置项文件中的内容都将按预定义的规则进行合并或者覆盖。请参考 :ref:`合并与优先级顺序`
这一小节以了解更多信息。

再说明一次，在 *Packages/User* 目录下的配置项文件拥有最高优先级，并且最终会覆盖其他同名配置项
文件中的相同内容。

除了配置项文件以外，Sublime Text还维护 *会话* 数据 —— 一些针对正在编辑的文件集所应用的配置项。
会话数据是在你编辑文件的过程中发生变化的，所以，无论你通过何种方式调整了一个特定文件的配置项
（主要是通过API调用的方式），这些配置项的变更将被记录在当前的会话中，并且将拥有比所有符合条件的
*.sublime-settings* 文件更高的优先级。

如果想要检查针对特定文件当前正在发挥作用的配置项的值，可以在控制台中输入
*view.settings().get(<配置项名称>)* 命令。

最后需要注意的是，某些配置项的值可能会被系统自动进行调整。请记住这一点，这样一来你就能够解释某
些令你困惑的配置项内容了。举例来说，在查看某些与空格相关的配置项的值，以及某些 ``语法`` 配置项
内容的时候，就有可能遇到这种问题。

接下来你将看到Sublime Text是如何处理Windows平台上Python相关的配置项文件的，这里的配置项文件
目录结构是虚构的：

- *Packages/Default/Preferences.sublime-settings*
- *Packages/Default/Preferences (Windows).sublime-settings*
- *Packages/User/Preferences.sublime-settings*
- *Packages/Python/Python.sublime-settings*
- *Packages/User/Python.sublime-settings*
- 当前文件的会话数据
- 由系统自动调整的配置项内容

（译者注：分析下优先级，可以得到结论：全局默认项 < 平台默认项  < 用户配置项 < 语言相关的配置
< 由用户指定的语言相关的配置 < 会话数据 < 系统调整的数据）


全局编辑器配置以及全局文件配置
===============================================

这类全局配置项内容一般被保存在名为 *Preferences.sublime-settings* 和
*Preferences (<platform>).sublime-settings* 的文件中。默认的全局配置项存放在
*Packages/Default* 目录中。


上面所说的 *<platform>* 可能是 ``Linux``, ``OSX``, 或者 ``Windows``.


文件类型配置
==================

如果你想针对某个特定的文件类型进行一些配置，那请根据这个文件类型的语法定义文件名称来对应的命名
*.sublime-settings* 文件。举例来说，如果我们的语法定义文件叫 *Python.tmLanguage* ，那么
配置项文件的名称就应该叫 *Python.sublime-settings* 。

通常情况下，某个特定文件类型的配置项信息一般存放在包组文件夹的一个目录中，例如 *Packages/Python*，
但是，与同一个文件类型相关的多个配置项文件也有可能被存放在不同的位置。

与全局配置项类似，也可以为文件类型配置项信息创建平台相关的内容。例如只有在Linux平台下，保存在
*Python (Linux).sublime-settings* 中的配置项内容才会被系统考虑。

需要特别指出的一点是，在 *Packages/User* 目录下，只有 *Python.sublime-settings* 文件会被
加载，所有以 *Python (<platform>).sublime-settings* 命名的平台相关的变种都不会被考虑。

不管文件类型配置项信息保存在哪里，它拥有比保存在全局配置项文件中的、影响文件类型的配置项都高的
优先级。


用户配置信息应该保存到哪里
=========================================

无论何时，当你想要保存一些配置的时候，尤其是那些在软件升级前后应该被保留的配置，就把它们保存在
*Packages/User* 目录下的对应 *.sublime-settings* 文件中吧。