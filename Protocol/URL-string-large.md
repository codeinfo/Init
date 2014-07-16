在http协议中，其实并没有对url长度作出限制，往往url的最大长度和用户浏览器和Web服务器有关，不一样的浏览器，能接受的最大长度往往是不一样的，当然，不一样的Web服务器能够处理的最大长度的URL的能力也是不一样的。
下面就是对各种浏览器和服务器的最大处理能力做一些说明.

Microsoft Internet Explorer (Browser)
IE浏览器对URL的最大限制为2083个字符，如果超过这个数字，提交按钮没有任何反应。在我的测试中，这个数字得到验证。

微软官方也有说明：

Microsoft Internet Explorer has a maximum uniform resource locator (URL) length of 2,083 characters. Internet Explorer also has a maximum path length of 2,048 characters. This limit applies to both POST request and GET request URLs.
If you are using the GET method, you are limited to a maximum of 2,048 characters, minus the number of characters in the actual path.
However, the POST method is not limited by the size of the URL for submitting name/value pairs. These pairs are transferred in the header and not in the URL.

Firefox (Browser)
对于Firefox浏览器URL的长度限制为65,536个字符，但当我测试时，最大只能处理8182个字符，这是因为url的长度除了浏览器限制外，还会受Web服务器的限制，而我本机使用的是ubuntu apache服务器，最大处理能力为8192个字符(相差10个字符，不知道是什么原因)，一旦超过这个长度，服务器就返回如下错误信息。

Safari (Browser)
URL最大长度限制为 80,000个字符。

Opera (Browser)
URL最大长度限制为190,000个字符。

Google (chrome)
url长度一旦超过8182个字符时，出现如下服务器错误：

写道

Request-URI Too Large
The requested URL's length exceeds the capacity limit for this server.
Apache/2.2.12 (Ubuntu) Server at 127.0.1.1 Port 80

Apache (Server)
能接受最大url长度为8,192个字符，但我的测试数据是8,182，10个字符，差别不在，数据具体符合。

Microsoft Internet Information Server(IIS)
能接受最大url的长度为16,384个字符。

通过上面的数据可知，为了让所有的用户都能正常浏览，我们的URL最好不要超过IE的最大长度限制(2038个字符），当然，如果URL不直接提供给用户，而是提供给程序调用，侧这时的长度就只受Web服务器影响了。

注：可能有些朋友会想当然的认为，如果最大长度限制为2038字符，是不是参数差不多可以传递1000个左右的汉字。这样认为其实是不对的，对于中文的传递，最终会为urlencode后的编码形式进行传递，如果浏览器的编码为UTF8的话，一个汉字最终编码后的字符长度为9个字符。