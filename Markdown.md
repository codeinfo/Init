#Markdown
---
##介绍 Introduction
###	Markdown is a text-to-HTML conversion tool for web writers.
### Markdown 是一款可以转换为HTML的网络书写语言。
### Markdown 具有兼容HTML、特殊字符自动转换的基本功能。
### Markdown 是一块可读性高，且书写简单，不包含大量标签和指令，目标是成为一种适用于网络的通用语言。

#Get started
---
##Markdown 基本语法
###标题
	#这是H1
	##这是H2
	###这是粗体

###列表
	* 这是无序列表
	1. 这是有序列表

###引用
	> 这是引用功能
	
###分割线
---
	段落
	---
	段落
	***
	段落
	————

###字体
	**abc**  加粗
	*abc* 倾斜
	_abc_ 倾斜

###代码
	保持原样输出
	4个空格 或者 一个 制表符
	`这是代码`  

###插入`<br>`回车
	2个空格+回车可以强制换行

###链接
[codeinfo](http://codeinfo.cn "codeinfo")

	[链接文字](网址 "超链接title")

###图片
	插入图片的语法是：
	![字符内容](图片路径 "链接的title")
	链接的title可以省略

###反斜杠
	如果想在非代码区域显示Markdown关键符号本身
	可以在符号前加\ 例如我要显示*****
	如果直接输入*****会输出分隔符
	我们应该这么输入:\*\*\*\*\*\* 