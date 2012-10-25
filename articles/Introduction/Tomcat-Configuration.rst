.. -*- coding: utf-8 -*-

.. _tomcat :

Tomcat 配置
=============

.. _intro :

介绍
-----

WebGoat已经附带了默认Tomcat配置文件。这篇课程将要解释默认配置和指导你进行其他的配置。虽然只是很简短介绍，但是应该足以应付大部分情况了。如果你想要深入了解更加高级的配置，欢迎参考Tomcat相关文档。

所有的课程解答都是基于80端口的默认配置。如果你使用其他端口请注意根据自己情况参考解答。

.. _standardconf :

标准配置
---------

WebGoat自带了两种标准的Tomcat配置选择。他们均被配置为localhost本地浏览。唯一不同的是一个监听80端口和443（ssl）端口，另外一种则是8080和8443。

在Linux中，如果你想使用80和443端口的配置的话，你必须以root身份或运行sudo程序来运行Tomcat。因为以root权限来运行程序是非常危险的事。我们强烈推荐使用8080和8443端口的配置。

在Windows中你可以运行 ``WebGoat.bat`` 来运行80端口的配置， ``WebGoat_8080.bat`` 来运行8080端口的配置。在Linux中，你可以使用 ``webgoat.sh start80`` 或者 ``webgoat.sh start8080`` 来选择。默认配置中的用户名为 ``guest`` 密码也为 ``guest`` 。

.. Note::

    Linux中1024以下端口为特权端口，使用这些端口需要特殊权限。

.. _serverconf :

服务器配置
-----------

如果你只是一个人使用WebGoat，那么默认的标准配置已经足够。但是如果你希望在班级中或者实验室中使用，那么你需要对配置文件做一些小小改动。在修改文件前，我们强烈建议预先备份相关配置文件，以免发生以外状况。

.. _change_ports :

更改服务端口
#############

打开 ``tomcat/conf`` 目录下的 ``server_80.xml`` ，更改 ``non-SSL port`` 。比如我们希望使用8079端口：

::

	<!-- Define a non-SSL HTTP/1.1 Connector on port 8079 --> 
	<Connector address="127.0.0.1" port="8079"...

你也可以修改SSL链接端口，比如我们希望使用8442端口：

::

	<!-- Define a SSL HTTP/1.1 Connector on port 8442 --> 
	<Connector address="127.0.0.1" port="8442"... 

.. _reachableforother :

使非本地客户端访问
###################

.. Warning::

    使用此设置会使服务器真正被攻击！除非你清楚你正要做的事情，否则请不要做出任何修改。以下配置应该仅仅用于安全的网络环境！

WebGoat在默认配置下只能由本机通过localhost访问。如果是在教室中或者实验室中使用，我们可能有一台服务器和多个客户端。在这种情况下我们需要使WebGoat能被非本地客户端访问。

我们通过设置 ``server_80.xml`` 中non-SSL和SSL ``address`` 参数来限制WebGoat仅能被本地访问。在标准配置文件中被设置为了 ``127.0.0.1`` 。一旦这里的地址参数被设置，Tomcat应用程序只会监听被设置的地址。如果你 **去除** 这个参数，那么服务器会监听所有的地址。

.. _permitclients :

限制特定客户端连接
###################

你已经会设置WebGoat对所有地址开放，但是现在你希望它只对特定的IP地址的客户端开放。你可以通过使用“远程地址过滤器”来达到这一目的。你可以选择白名单或者黑名单方法来过滤。我们在这里只讨论使用白名单。你需要将下面的内容加入 ``server_80.xml`` 的 ``Host`` 配置区域。

::

    <Host ...>
	    <Valve className="org.apache.catalina.valves.RemoteAddrValve"
	    allow="127.0.0.1,ip1,ip2"/>
    </Host>

在上面的配置中，我们只允许localhost，ip1，ip2连接服务器。

.. _defaultuser :

Tomcat中WebGoat的默认用户和角色
---------------------------------

WebGoat需要以下用户和角色来保证程序可以正常运行。

::

    <role rolename="webgoat_basic"/>
    <role rolename="webgoat_admin"/>
    <role rolename="webgoat_user"/>
    <user username="webgoat" password="webgoat" roles="webgoat_admin"/>
    <user username="basic" password="basic" roles="webgoat_user,webgoat_basic"/>
    <user username="guest" password="guest" roles="webgoat_user"/>

.. _adduser :

添加用户
---------

通常你只需要通过 ``guest`` 用户来使用。或许在一个实验室中你已经有一台服务器和许多客户端，你希望每个客户端配置一个不同的用户，那么你需要修改 ``tomcat-users.xml`` 文件。这个文件存在于 ``tomcat/conf`` 中，管理着用户信息。 **我们强烈建议不要使用真实的密码，因为密码将明文方式存储在这个文件中！**

添加用户非常简单，你可以参照guest条目。新增的用户的角色设置成与guest用户角色相同即可。例如新增以下条目：

::

	<user name="student1" password="password1" roles="webgoat_user"/>
	<user name="student2" password="password2" roles="webgoat_user"/>
	...

**恭喜你完成了本次课程！**

