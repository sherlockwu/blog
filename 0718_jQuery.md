# jQuery 积累
jQuery 的一些资料在js的笔记中

## 一些积累
1. `$(document).ready()` 选取整个文档，ready之后用相应func处理
2. `$.getJSON()`   The getJSON() method is used to get JSON data using an AJAX HTTP GET request.
3. `keycode == 13` 表示按了 enter键
	类似的还有 onKeyup onKeypress 事件 [参考网站](http://blog.sina.com.cn/s/blog_8697aaed0100zmg8.html)
4. `$.ajax` 方法   [参照这个](http://www.w3school.com.cn/jquery/ajax_ajax.asp)
	通过HTTP 请求加载远端数据 
	还有一个所写的 $.getJSON() 以JSON格式   [参考](http://api.jquery.com/jquery.getjson/)
5. `$("#xxx").click(function)` 可以定义这个标签被click触发的函数 （还不一定是button，文字也可以！）
	click别的button也能触发这个function，只需要 将新button的处理函数设成 `$("#前一个button").click()` 即可 
6. `alert(string)` 弹窗
7. `.val()` 可以得到相应的内容，或者设置相应的内容
8. `.ajax()` 可以通过HTTP 异步向或从远端server 发送或接受 数据 	
## JSON 
[一个教程](http://www.w3school.com.cn/json/json_intro.asp)

## Ref
