.. -*- coding: utf-8 -*-

.. _dom_injection:

DOM注入攻击
============

.. _domi_concept:

简介
-------

本课程将要指导你如何进行DOM注入攻击。

.. _domi_attack:

攻击原理
---------

一些应用程序经常直接使用AJAX进行操作，特别是直接使用javascript，DHTML和eval()方法更新DOM。攻击者往往会利用这一点分析数据并尝试注入一些javascript命令来进行攻击。

.. _domi_goal:

课程目标
---------

* 你的受害者是一个使用激活key来允许操作的系统。
* 你的目标是尝试是激活按钮有效化。
* 花费些时间阅读HTML源代码来弄清楚key认证过程是如何进行的。

