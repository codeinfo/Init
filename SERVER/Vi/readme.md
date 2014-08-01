Vi / vim
---

vi / vim 删除以及其它命令

删除一行：dd

 

删除一个单词/光标之后的单词剩余部分：dw

 

删除当前字符：x

 

光标之后的该行部分：d$

 

 

文本删除

dd 删除一行

d$ 删除以当前字符开始的一行字符

 

ndd 删除以当前行开始的n行

dw 删除以当前字符开始的一个字

ndw 删除以当前字符开始的n个字

 

D 与d$同义

 

d) 删除到下一句的开始

 

d} 删除到下一段的开始

d回车 删除2行

ndw 或 ndW 删除光标处开始及其后的 n-1 个字符。
d0 删至行首。
d$ 删至行尾。
ndd 删除当前行及其后 n-1 行。
x 或 X 删除一个字符。
Ctrl+u 删除输入方式下所输入的文本。
^R 恢复u的操作
J 把下一行合并到当前行尾
V 选择一行
^V 按下^V后即可进行矩形的选择了
aw 选择单词
iw 内部单词(无空格)
as 选择句子
is 选择句子(无空格)
ap 选择段落
ip 选择段落(无空格)
D 删除到行尾
x,y 删除与复制包含高亮区

dl 删除当前字符（与x命令功能相同）
d0 删除到某一行的开始位置
d^ 删除到某一行的第一个字符位置（不包括空格或TAB字符）
dw 删除到某个单词的结尾位置
d3w 删除到第三个单词的结尾位置
db 删除到某个单词的开始位置
dW 删除到某个以空格作为分隔符的单词的结尾位置
dB 删除到某个以空格作为分隔符的单词的开始位置
d7B 删除到前面7个以空格作为分隔符的单词的开始位置
d） 删除到某个语句的结尾位置
d4） 删除到第四个语句的结尾位置
d（ 删除到某个语句的开始位置
d） 删除到某个段落的结尾位置
d{ 删除到某个段落的开始位置
d7{ 删除到当前段落起始位置之前的第7个段落位置
dd 删除当前行
d/text 删除从文本中出现“text”中所指定字样的位置，
一直向前直到下一个该字样所出现的位置（但不包括该字样）之间的内容
dfc 删除从文本中出现字符“c”的位置，一直向前直到下一个该字符所出现的位置（包括该字符）之间的内容
dtc 删除当前行直到下一个字符“c”所出现位置之间的内容
D 删除到某一行的结尾
d$ 删除到某一行的结尾
5dd 删除从当前行所开始的5行内容
dL 删除直到屏幕上最后一行的内容
dH 删除直到屏幕上第一行的内容
dG 删除直到工作缓存区结尾的内容
d1G 删除直到工作缓存区开始的内容

 

 
在Vi 中移动光标

  k        上
h   l    左  右
  j        下

^        移动到该行第一个非空格的字符处
w        向前移动一个单词，将符号或标点当作单词处理
W        向前移动一个单词，不把符号或标点当作单词处理
b        向后移动一个单词，把符号或标点当作单词处理
B        向后移动一个单词，不把符号或标点当作单词处理
(        光标移至句首
)        光标移至句尾
{        光标移至段落开头
}        光标移至段落结尾
H        光标移至屏幕顶行
M        光标移至屏幕中间行
L        光标移至屏幕最后行 
0        到行首
$        到行尾
gg       到页首
G        到页末
行号+G   跳转到指定行
n+       光标下移n行
n-       光标上移n行 
Ctrl+g   查询当前行信息和当前文件信息

fx       向右跳到本行字符x处（x可以是任何字符）
Fx       向左跳到本行字符x处（x可以是任何字符）

tx       和fx相同，区别是跳到字符x前
Tx       和Fx相同，区别是跳到字符x后

C-b      向上滚动一屏
C-f      向下滚动一屏
C-u      向上滚动半屏
C-d      向下滚动半屏
C-y      向上滚动一行
C-e      向下滚动一行

nz       将第n行滚至屏幕顶部，不指定n时将当前行滚至屏幕顶部。 

进入和退出Vi命令

vi filename               打开或新建文件，并将光标置于第一行首
vi +n filename            打开文件，并将光标置于第n行首
vi + filename             打开文件，并将光标置于最后一行首
vi +/pattern filename     打开文件，并将光标置于第一个与pattern匹配的串处
vi -r filename            在上次正用vi编辑时发生系统崩溃，恢复filename
vi filename ... filename  打开多个文件，依次进行编辑 

ZZ                        退出vi并保存
:q!                       退出vi，不保存
:wq                       退出vi并保存

重复操作

.        重复上一次操作

自动补齐

C-n      匹配下一个关键字
C-p      匹配上一个关键字

插入

o        在光标下方新开一行并将光标置于新行行首，进入插入模式。
O        同上，在光标上方。

a        在光标之后进入插入模式。
A        同上，在光标之前。


R        进入替换模式，直到按下Esc
set xxx  设置XXX选项。

行合并

J        把下面一行合并到本行后面

Vi中查找及替换命令

/pattern         从光标开始处向文件尾搜索pattern
?pattern         从光标开始处向文件首搜索pattern
n                在同一方向重复上一次搜索命令
N                在反方向上重复上一次搜索命令
%                查找配对的括号
:s/p1/p2/g       将当前行中所有p1均用p2替代，若要每个替换都向用户询问则应该用gc选项
:n1,n2s/p1/p2/g  将第n1至n2行中所有p1均用p2替代
:g/p1/s//p2/g    将文件中所有p1均用p2替换

.*[]^%~$ 在Vi中具有特殊含义，若需要查找则应该加上转义字符"\"

查找的一些选项
设置高亮

:set hlsearch    设置高亮
:set nohlsearch  关闭高亮
:nohlsearch      关闭当前已经设置的高亮

增量查找

:set incsearch   设置增量查找
:set noincsearch 关闭增量查找

在Vi中删除

x        删除当前光标下的字符
dw       删除光标之后的单词剩余部分。
d$       删除光标之后的该行剩余部分。
dd       删除当前行。

c        功能和d相同，区别在于完成删除操作后进入INSERT MODE
cc       也是删除当前行，然后进入INSERT MODE

更改字符

rx       将当前光标下的字符更改为x（x为任意字符） 
~        更改当前光标下的字符的大小写 

 
键盘宏操作

qcharacter  开始录制宏，character为a到z的任意字符
q           终止录制宏
@character  调用先前录制的宏

恢复误操作

u        撤销最后执行的命令
U        修正之前对该行的操作
Ctrl+R   Redo

在Vi中操作Frame

c-w c-n  增加frame
c-w c-c  减少frame
c-w c-w  切换frame
c-w c-r  交换两个frame

VIM中的块操作

Vim支持多达26个剪贴板

  选块   先用v，C-v，V选择一块，然后用y复制，再用p粘贴。
  yy     复制当前整行
  nyy    复制当前行开始的n行内容
  ?nyy   将光标当前行及其下n行的内容保存到寄存器?中，其中?为一个字母，n为一个数字
  ?nyw   将光标当前行及其下n个词保存到寄存器?中，其中?为一个字母，n为一个数字
  ?nyl   将光标当前行及其下n个字符保存到寄存器?中，其中?为一个字母，n为一个数字
  ?p     将寄存器?中的内容粘贴到光标位置之后。如果?是用yy复制的完整行，
         则粘贴在光标所在行下面。这里?可以是一个字母，也可以是一个数字 
  ?P     将寄存器a中的内容粘贴到光标位置之前。如果?是用yy复制的完整行，
         则粘贴在光标所在行上面。这里?可以是一个字母，也可以是一个数字 
  ay[motion]
            ay$    复制光标位置到行末并保存在寄存器a中
            ayft   复制光标位置到当前行第一个字母t并保存在寄存器a中

以上指令皆可去掉a工作，则y,p对未命名寄存器工作（所有d,c,x,y的对象都被保存在这里）。
剪切/复制/粘贴

所有删除的内容自动被保存，可以用p键粘贴
Vi的选项设置

all         列出所有选项设置情况
term        设置终端类型
ignorance   在搜索中忽略大小写
list        显示制表位(Ctrl+I)和行尾标志($)
number      显示行号
report      显示由面向行的命令修改过的数目
terse       显示简短的警告信息
warn        在转到别的文件时若没保存当前文件则显示NO write信息
nomagic     允许在搜索模式中，使用前面不带“\”的特殊字符
nowrapscan  禁止vi在搜索到达文件两端时，又从另一端开始
mesg        允许vi显示其他用户用write写到自己终端上的信息 

tips

对代码自动格式化 gg=G

 

 

在vi/vim中，跳到文件首尾快捷键:

 

文件开始:shift + g

文件结束:g g