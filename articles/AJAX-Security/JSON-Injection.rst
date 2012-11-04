.. -*- coding: utf-8 -*-

.. _json_injection:

JSON注入攻击
============

.. _jsoni_concept:

简介
-------

本次课程将要指导你如何进行JSON注入攻击。

.. _jsoni_attack:

攻击原理
---------

JavaScript Object Notation（JSON，javascript对象标记语言）是简单高效的轻量级数据交换格式。JSON可以用在很多方面比如数组、列表、哈希表和其他数据结构。JSON被广泛应用在AJAX和Web2.0应用程序中。由于它十分容易使用和传输迅速，所有比XML更加受到程序员们喜爱。但是JSON像XML一样容易被注入攻击。一个恶意的攻击者可以在服务器响应中注入任意数据。

.. _jsoni_goal:

课程目标
---------

* 你正从Boston,MA（机场代码BOS）去Seattle,WA（机场代码SEA）旅行。
* 一旦你输入三位机场代码，一个AJAX请求被执行去查询票价。
* 你注意到有两个航班可用，一个途中不停靠但更贵，另一个途中停靠两站但便宜。
* 你的目标是试着以便宜的价格获得不停靠的班次的机票。

