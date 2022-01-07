### xss

1、概念

2、攻击类型

3、如何防范

4、自己工作中是否遇到？如何解决？



cross-site scripting(跨站脚本攻击)，攻击者想尽一切办法将可执行代码注入到网页中。



**攻击场景**

1、评论区植入js代码(可输入的地方)

2、url上拼接代码



**技术上的xss攻击类型**

1、存储型 Server

论坛发帖、商品评价、用户私信等这些用户保存数据的网站



攻击步骤：

* 攻击者将恶意代码提交到目标网站的数据库中
* 用户打开目标网站时，服务端将评论(恶意代码)从数据库取出，拼接到html返回给浏览器
* 用户浏览器收到html后，混在其中的恶意代码就会被执行。
* 窃取用户数据，发送到攻击者网站



2、反射型 Server

攻击者结合各种手段诱导用户点击恶意url。

通过url传参的功能，比如网站的搜索或者跳转等。



攻击步骤：

* 攻击者构造出自己的恶意url
* 用户打开url，直接执行可执行的恶意代码



3、Dom型 Browser

取出和执行恶意代码的操作，由浏览器完成

攻击步骤：

* 获取url参数，url拼接啥的。



### 如何去防范xss攻击

主旨：防止攻击者提交恶意代码，防止浏览器执行恶意代码

1、对数据进行严格的输入编码，比如html元素，js，css，url

vue  vue-html

React  dangerousHtml

2、CSP Content Security Policy  (X-XSS-Protection)

Default-src 'self' 所有加载的内容必须来自站点的同一个源

3、输入验证

4、开启浏览器的XSS防御：Http Only Cookie

5、验证码



### CSRF

Cross Site Request Forgery，跨站请求伪造



### 攻击步骤：

1、受害者登录 a.com ，并且保留了登录凭证 cookie

2、攻击者诱导受害者 访问了b.com

3、b.com向a.com发送请求，a.com/xxxx，浏览器就会直接将a.com的cookie带上

4、a.com收到了请求，执行了相应操作

5、攻击者在受害者不知情的情况下，冒充受害者让a.com执行了自己定义的操作



### 攻击类型

1、GET型：在页面中的某个img发起一个get请求

2、POST型：自动提交表单到恶意网站

### 如何防范

CSRF一般发生在第三方域名，攻击者无法获取到cookie信息的，只不过利用浏览器自动携带了。

1、阻止第三方域名的访问

	* 同源检测
	* Cookie SameSite

2、提交请求的时候附加额外信息

* CSRF Token

  用户打开页面的时候，服务器利用加密算法生成一个Token

  用户每次加载的时候，前端把获取到的Toke，放到能够发送请求的HTML元素上

  每次js发送请求，也都携带Token

  服务器每次接受请求时，就检验Token的有效性

* 双重Cookie

  用户在访问网站的时候，服务器向浏览器注入一个额外的Cookie，内容随便，如name=“BBB”

  每次前端发起请求，都拼上一个参数name=“BBB”

  服务校验csrf cookie是否正确