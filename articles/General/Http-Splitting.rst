.. -*- codings: utf-8 -*-

.. _httpsplitting:

HTTP Splitting攻击
===================

.. _hs_concept:

简介
-----

本课将要指导如何实施HTTP Splitting攻击。

.. _how_hs_works:

HTTP Splitting攻击原理
------------------------

攻击者通过在正常的输入中向服务器传递恶意的代码。受害的应用程序将不会检查回车(CR,carriage return,通常表示为 ``%0d`` 或者 ``\r``)和换行(LF,line feed,通常表示为 ``%0a`` 或者 ``\n``) 字符。这些字符不仅给攻击者控制剩余的头部和应用程序的响应，而且允许他们创建额外的完全受控制的响应。

当和缓冲区毒化(Cache Poisoning)共同进行时，HTTP Splitting攻击将会取得最大的效果。缓冲区毒化攻击的目的是毒化客户端缓冲使客户端的缓冲相信被HTTP Splitting攻击劫持的网页是真实的服务器页面副本。

完成这种毒化攻击只要在HTTP Splitting攻击中加入 ``Last-Modified:`` 头，并将此设置为一个未来的值即可。这将强制浏览器在未来的请求中发送一个错误的 ``If-Modified-Since`` 请求头。因为该值是一个未来的值，那么服务器端总是会报告（这个被毒化）的页面并没有被修改，受害者的浏览器就会继续使用缓存中的恶意页面。

一个304响应的例子如下：

::

    HTTP/1.1 304 Not Modified
    Date: Fri, 30 Dec 2005 17:32:47 GMT


    GET /index.html?param=value HTTP/1.0

.. _hs_goal:

课程目标
---------

本课程分为二个阶段。阶段一将要教你如何实施HTTP Splitting攻击，阶段二则是教你如何将将缓冲区毒化融合入攻击中。

输入任何语言，你会注意到应用程序将会重定向你的请求到服务器上的另一个页面。你能够输入CR(%0d)和LF(%0a)字符来执行这一攻击。你的目标是强制服务器返回一个2-- OK响应。如果你已经顺利劫持了服务器，成功执行了HTTP Splitting攻击，简单返回主页即可，就会进入阶段二。在阶段二完成后，页面左边会出现完成标记。

1. 利用CRLF字符伪造应答进行HTTP Splitting攻击
2. 同时结合缓存区毒化攻击

你会发现  `PHP 字符编码转换器`__ 非常有用。使用Encode和DecodeURIComponent按钮来转换CR和LF字符。

__ http://yehg.net/encoding/

