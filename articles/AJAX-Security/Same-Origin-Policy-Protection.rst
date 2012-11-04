.. -*- coding: utf-8 -*-

.. _Same_Origin_Policy_Protection:

同源策略保护
=============

.. _sopp_concept:

简介
-----

AJAX的关键元素是 ``XMLHttpRequest`` (XHR)，它允许javascript在客户端向服务器发送异步请求。作为一个安全防护措施，这些被发送往服务器端的请求应该是和发送请求的页面同源。

.. _sopp_goal:

课程目标
---------

这个练习证明了同源策略保护措施。XHR请求只能被发送到原来的服务器。一些发送到不同源的服务器的请求企图会失败。

