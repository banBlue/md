[TOC]

####名词解释:
浏览器默认会有同源策略,协议+域名+端口号(htts://www.baidu.com:80),有任何一项不同就会触发同源策略,此时还想要通过ajax进行接口调用,就需要服务端配合,达到跨域资源共享的目的. 复杂跨域请求

####复杂跨域请求
复杂的跨域请求，条件满足以下三个其中之一：

1.请求方式不是 HEAD 、GET 或 POST  

2.Content-Type 取的值不是以下三个之一：
application/x-www-form-urlencoded
multipart/form-data
text/plain

3.不能自定义 header 字段（最常见的就是自定义加了token、Cookie）

####产生影响:
1.ajax无法请求出去

####解决方案:
服务端设置允许跨域请求资源Access-Control-Allow-Origin
同源策略是由浏览器发起的,所以触发了的情况下,会产生两次请求,先有个预请求options(如果是在node则不会有这种预请求),询问服务端是否允许跨域,同意后才进行第二次真正请求.

