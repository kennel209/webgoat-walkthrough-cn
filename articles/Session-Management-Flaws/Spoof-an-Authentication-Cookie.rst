.. -*- coding: utf-8 -*-

.. _spoof_an_authentication_cookie:

欺骗认证Cookie
==========================

.. _saac_concept:

简介
-----

当存在正确的认证cookie时候，许多应用程序自动使用它进行用户登录。有些时候如果生成这个cookie的算法能够被知晓，那么cookie的值可以被猜到。或者有些时候存在客户机器上cookie被使用其他系统漏洞的攻击者所盗取。又或者cookie被跨站脚本所截获。本次课程试着让你注意到cookie认证的过程，并且找到突破cookie认证的方法。

.. _saac_goal:

课程目标
----------

用户应该能够绕过认证检查，使用 ``webgoat/webgoat`` 帐户来登录，同时观察这个过程中发生了什么。你可能也需要使用 ``aspect/aspect`` 帐户登录。当你弄明白了认证cookie是如何生成的，尝试使用 ``alice`` 登录。

