#第一章 网页设计概述
web浏览器先把URL发送给服务器，服务器返回指定html文档  
超文本是一种电子文档，允许其中文字可以包含有可以链接到其他字段或者文档的超文本链接  
HTMl是一种标记语言，有自己的词汇（符号）和语法（规则）  
所谓标记，就是做记号  
<title>简单的列子</title>  
HTML文件的结构  
	<html>	#HTML文档标记
		<head>	#文档首部标记	
			<title>标题</title>	#标题标记
		</head>
		<body>	#文档内容标记
			文档部分
		</body>
	</html>
***
一个主机可以有多个ip地址，但一个ip地址只能分配给一个主机  
域名与IP地址映射：多对多  
一个域名映射到多个IP：访问负载均衡  
浏览器先把域名发送给DNS服务器，服务器获取域名后返回指定ip地址，然后浏览器再把ip地址和域名一起发送给web服务器，缺一不可，因为有些服务器绑定了多个ip地址。