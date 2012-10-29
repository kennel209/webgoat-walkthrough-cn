.. -*- codings: utf-8 -*-

.. _httpbasics:

HTTP基础
=========

.. _hb_concept:

简介
-----

本课将会展示浏览器和web应用程序间的数据通信基础。

.. _how_http_works:

HTTP是怎样工作的
-----------------

所有HTTP事务遵循同样的基本格式。每个客户请求和服务器响应都有3个部分：请求/响应行；http头部区域；http实体部分。服务器如下所示初始化一个事务：

::

    GET /index.html?param=value HTTP/1.0

接着客户端发送可选的头(header)信息来告知服务端自身的配置和他所接受的文档格式。

::

    User-Agent: Mozilla/4.06 Accept: image/gif,image/jpeg, */*

发送完请求和头部之后，客户端可能继续发送额外的数据，这些数据通常使用POST方法，被CGI程序使用。

.. _hp_goal:

课程目标
---------

在输入框中输入你的名字，按go进行提交。服务器接受请求，翻转字符串，发还给用户，来展示处理HTTP请求的基础。

用户应该能够通过操作webgoat页面上方的按钮来查看提示，显示HTTP请求参数和Cookies以及此课程的java源代码。你同样也可以尝试Webscarab来查看这些内容。

