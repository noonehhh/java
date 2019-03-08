Servlet

1.Servlet
    1.servlet的生命周期 ：从init开始到distroy结束
 	                      初始化：web容器加载servlet,调用init方法。    
						  处理请求：请求到达时，调用service()方法，service()派遣请求对应的doget或dopost方法进行处理
						  销毁：服务结束，web容器调用destroy()方法销毁servlet。
						  
    	 
2.get和post的区别
     （1）get一般用于从服务器上获取数据，post一般用于向服务器传送数据

     （2）请求的时候参数的位置有区别，get的参数是拼接在url后面，用户在浏览器地址栏可以看到。post是放在http包的包体中。
          比如说用户注册，你不能把用户提交的注册信息用get的方式吧，那不是说把用户的注册信息都显示在Url上了吗，是不安全的。

     （3）能提交的数据有区别，get方式能提交的数据只能是文本，且大小不超过1024个字节，而post不仅可以提交文本还有二进制文件。
          所以说想上传文件的话，那我们就需要使用post请求方式
		  
3.forward和redirect的区别

     转发与重定向

    （1）从地址栏显示来说 
         forward是服务器请求资源,服务器直接访问目标地址的URL,把那个URL的响应内容读取过来,然后把这些内容再发给浏览器.浏览器根本不知道服务器发送
         的内容从哪里来的,所以它的地址栏还是原来的地址.redirect是服务端根据逻辑,发送一个状态码,告诉浏览器重新去请求那个地址.所以地址栏显示的是新的URL.

    （2）从数据共享来说 
         forward:转发页面和转发到的页面可以共享request里面的数据.
         redirect:不能共享数据.

    （3）从运用地方来说 
         forward:一般用于用户登陆的时候,根据角色转发到相应的模块.
         redirect:一般用于用户注销登陆时返回主页面和跳转到其它的网站等.

    （4）从效率来说 
         forward:高.
         redirect:低.

4.什么情况下调用doGet()和doPost()？
     JSP页面中的form标签里的method属性为get时调用doGet()，为post时调用doPost()；超链接跳转页面时调用doGet()
	 
5.页面间对象传递的方法
     request，session，application，cookie等

6.常见网页状态码

200 - 服务器成功返回网页
404 - 请求的网页不存在
503 - 服务器超时

1xx（临时响应）表示临时响应并需要请求者继续执行操作的状态码。
100（继续） 请求者应当继续提出请求。服务器返回此代码表示已收到请求的第一部分，正在等待其余部分。

2xx （成功）表示成功处理了请求的状态码。
200（成功） 服务器已成功处理了请求。通常，这表示服务器提供了请求的网页。如果是对您的 robots.txt 文件显示此状态码，则表示 Googlebot 已成功检索到该文件。

3xx （重定向）
要完成请求，需要进一步操作。通常，这些状态码用来重定向。Google 建议您在每次请求中使用重定向不要超过 5 次。
您可以使用网站管理员工具查看一下 Googlebot 在抓取重定向网页时是否遇到问题。诊断下的网络抓取页列出了由于重定向错误导致 Googlebot 无法抓取的网址。

4xx（请求错误）
这些状态码表示请求可能出错，妨碍了服务器的处理。
400（错误请求） 服务器不理解请求的语法。

5xx（服务器错误）
这些状态码表示服务器在处理请求时发生内部错误。这些错误可能是服务器本身的错误，而不是请求出错。
500（服务器内部错误） 服务器遇到错误，无法完成请求。