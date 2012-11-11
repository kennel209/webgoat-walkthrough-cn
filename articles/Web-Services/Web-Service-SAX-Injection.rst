.. -*- coding: utf-8 -*-

.. _web_service_sax_injection:

Web服务SAX注入
==========================

.. _saxi_concept:

简介
-----

Web服务通过SOAP请求进行通信。这些请求尝试执行用WSDL（web service description language）定义的函数。我们将要学习一些关于WSDL文件的知识。请参考WebGoat的WSDL文件进行学习。

.. _saxi_goal:

课程目标
----------

一些web接口在后台利用Web服务。如果前端信赖web服务所有的输入验证，那么它可能通过篡改web接口发送的XML来被破坏。

在这个练习中，试着更改除了101以外的用户的密码。

