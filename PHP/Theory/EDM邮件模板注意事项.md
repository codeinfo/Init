邮件模板，请严格按照下面的规则执行。邮件客户端和Web页面的需求不同，在编写代码的时候，考虑的方向也不一样。

!Doctype声明
为了向前兼容和避免某些浏览器的怪癖，使用html5的!doctype声明，格式如下：
<!DOCTYPE  HTML>

原则，及思维出发点
1.  不需要考虑DOM节点的精简和结构的优化。
  以完成设计样式为最优先。必要时，不必吝啬使用表格嵌套，不必吝啬使用空的表格元素来占据空间。

2.  宁可冗余，也不可缺少必要定义。

3.  充分利用表格的私有属性来布局。width,  height,  bgcolor,  background,  align,  valign等

4.  可替代性：
  在编写html的时候，请思考当你页面的所有图片都被屏蔽时，是否用户还能了解页面的主要内容。
  请务必在所有要设置背景图片的元素上，定义背景颜色。

5.  可利用Dreamweaver等工具来协助编写html，但切记，一定要时候做好每行代码的检查。

Mackup
1.  主体页面，包括细节处理，尽量使用<table>布局。

2.  不允许在<tr>元素上定义CSS样式，请将样式尽量定义在<td>元素上。（Gmail等邮件客户端会过滤<tr>上的属性）

3.  禁止使用<style  type=”text/css”>来处理主要样式，所有的Web邮件系统都会过滤该标签。因此邮件模板中不能使用伪类（pseudo  class）和伪元素（pseudo  elements），以及高级选择符。

但是，

我们仍然可以使用<style>来提升一些比较先进的邮件PC客户端的体验，比如伪类。
但，必须使用表格和元素样式来完成所有基本样式和布局。

4.  禁止使用<link>来加载外联CSS

5.  可以使用<div>来实现细节的，具有典型块级元素(block)的布局样式。而尽量避免使用<p>，因为我们不容易清除<p>在不同浏览器的默认样式

6.  注意定义图片的替换文字（alt），及替换文字的颜色。

样式

1.  文字的处理。
font-*  族的CSS属性不允许使用缩写，请分别定义  font-size,  font-weight,  line-height,  font-family(font-family有可能被过滤)

2.  继承性
注意表格不会继承外部的font等属性，请务必，在每个<td>元素上都定义字体属性和颜色。

3.  背景的处理

  不允许使用style=”background:url(http://…)”，请使用<td>的属性(attribute)  background=“http://…”。（由于CSS背景图片是一种会影响页面渲染速度的定义，因此大多数Web邮件系统会过滤它。）

  背景颜色，也请使用表格的bgcolor属性。

4.  对于复杂样式的处理，可以大胆地、大块地切图。

5.  避免尝试让两个table-cell的元素对齐，如果,  一个元素是用具体的宽度定义（width=”100″），另一个元素是用百分比来定位(  width=”50%”)

6.  避免使用list-style来处理列表样式，请使用  “  •  ”  字符来替代。

7.  避免使用<img>元素拼接的方式，来实现背景大图的分割，尽量使用表格的background
  我们知道，在<img>元素下4px空白的问题。

禁用的，和不建议使用的CSS样式（见参考文献1）
这些样式，大都是可能引起元素偏移到容器外的样式

禁止使用  position,  background,  float

特别说明：
margin:  margin的使用要非常谨慎，不允许使用margin作为重要的布局依据，不允许使用负margin，避免使用非零和非auto的margin属性。

图片版本控制（点评网业务需求）
  如果邮件模板中的图片，使用  CDN  网络地址——如  http://dajie.me/4oa0kg…/abc.png——那么，更新这张图片的时候，请联系DBA（数据库工程师）刷新该图片的版本号。
  并且，在新的邮件模板中，将该图片的版本号加1，比如：

  将  http://dajie.me/4oa0kh…/edm/top.png  更新为  http://dajie.me/4oa0kh…/edm/top.v1.png
  将  http://dajie.me/4oa0kh…/edm/bot.v12.png  更新为  http://dajie.me/4oa0kh…/edm/top.v13.png

常见问题
1.  如何让邮件在Gmail等Web页面中居中
有几种方式：
  a>  在  body上定义style=”width:apx;  margin:auto”。注意，在Web邮件中，会自动为你生成一个<div  style=”width:apx;  margin:auto”>  的元素在最外层。(可以有效利用这一特性，定义背景颜色等样式，和实现其他可能的事情)

  而不要尝试自己在邮件模板最外层添加一个带有margin:auto的<div>元素。

  b>  使用<center>

2.  如何在邮件的布局中占据空白
请使用空白的<td>元素，设置height属性来起到站位的作用。