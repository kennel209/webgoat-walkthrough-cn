.. -*- coding: utf-8 -*-

.. _createalesson:

创建WebGoat课程
================

给WebGoat创建新的课程非常容易。如果你有合适作为课程的好主意，不妨按照下列步骤来实现它。

* 下载 `WebGoat`__ 源代码
* 搭建框架平台: 请参照项目相关 ``HOW TO create the WebGoat workspace.txt`` 。
* 为每个新课程新建2个文件:
    - 在 ``org.owasp.webgoat.lessons`` 中加入 ``YourLesson.java`` 
    - 在 ``WebContent/lesson_plans`` 中加入 ``YourLesson.html``

__ http://code.google.com/p/webgoat/

.. _detail:

详细课程创建指南
-----------------

创建新的课程很简单，只需简单的代码。事实上，大多数课程通过遵循 `WebGoat用户指南`__ 就很容易构建。如果你愿意的话，也可以将你的课程想法发送给 webgoat@owasp.org

__ http://www.owasp.org/index.php/WebGoat_User_and_Install_Guide_Table_of_Contents

你需要做的所有事情就是实现 ``LessonAdapter`` 中的抽象方法。就像下面一样。

WebGoat使用jakarta项目中的 ``Element Construciton Set`` 。你应该读一下ECS的 `API文档`__ 。此外你也可以参考其他课程中如何使用ECS的例子。

__ http://jakarta.apache.org/site/downloads/downloads_ecs.cgi

.. _step1:

第一步: 建立框架
#################

::

    import java.util.*;
    import org.apache.ecs.*;
    import org.apache.ecs.html.*;

    // 在这里可以添加版权信息，参考其他课程

    public class NewLesson extends LessonAdapter
    {

        protected Element createContent(WebSession s)
        {
            return( new StringElement( "Hello World" ) );
        }

        public String getCategory()
        {
        }

        protected List getHints()
        {
        }

        protected String getInstructions()
        {
        }

        protected Element getMenuItem()
        {
        }

        protected Integer getRanking()
        {
        }

        public String getTitle()
        {
        }
    }


.. _step2:

第二步: 实现 ``createContent``
################################

创建课程内容也很简单。主要分2部分:
(1) 处理用户上个的请求的输入部分
(2) 生成下一阶段页面

这就是 ``createContent`` 方法干的所有事情。记住每个课程应该在单个页面中独立处理，你需要按照这个要求来设计课程。一个好的通用模版如下所示:

::

    // 定义输入域的名
    private static final String INPUT = "input";
        
    protected Element createContent(WebSession s)
    {
        ElementContainer ec = new ElementContainer();
        try
        {
            // 获得用户输入，更多细节请参考ParameterParser 
            String userInput = s.getParser().getStringParameter(INPUT, "");

            // 针对输入进行操作
            //   -- SQL查询?
            //   -- 实时运行程序 Runtime.exec?
            //   -- 一些其他的危险操作
                
            // 生成输出页面，包含字符串信息和输入信息区域
            ec.addElement(new StringElement("Enter a string: "));
            ec.addElement( new Input(Input.TEXT, INPUT, userInput) );
                
            // 当用户顺利完成课程时，告诉lesson tracker课程已经完成
            makeSuccess(s);

        }
        catch (Exception e)
        {
            s.setMessage("Error generating " + this.getClass().getName());
            e.printStackTrace();
        }
        return (ec);
    }

ECS十分强大，可以参考编码教学课程的例子来创建带输出的表格。

.. _step3:

第三步: 实现其他方法
#####################

在 ``LessonAdapter`` 类中的其他方法能帮助课程更好的和WebGoat框架结合，并且很容易实现。

::

    public String getCategory()
    {
        // 默认类别目录是"General"，如果你希望建立新目录，请重载
        // 这个方法
            
        return( "NewCategory" );  // or use an existing category
    }

    protected List getHints()
    {
        // 提示会被按照这里的编写顺序依次显示
        // 用户必须点击"next hint"才会显示下一条提示
            
        List hints = new ArrayList();
        hints.add("A general hint to put users on the right track");
        hints.add("A hint that gives away a little piece of the problem");
        hints.add("A hint that basically gives the answer");
        return hints;
    }

    protected String getInstructions()
    {
        // 课程指导会以html格式显示在实际课程区域上方
        // 一般包含课程基本情况和目标
            
        return("The text that goes at the top of the page");
    }

    protected Element getMenuItem()
    {
        // 左侧目录中的课程名字，注意长度可能影响折行
            
        return( "MyLesson" );
    }

    protected Integer getRanking()
    {
        // 权重影响该课程在目录中的位置，越小越前面
            
        return new Integer(10);
    }

    public String getTitle()
    {
        // 课程标题，将会表示成html显示在标题栏上
            
        return ("My Lesson's Short Title");
    }

.. _step4:

第四步: 编译和测试
####################

一旦你实现了你的课程，你可以使用(Eclipse)中的Tomcat服务器进行测试。参见WegGoat中的 ``readme.txt`` 。

.. _step5:

第五步: 创建课程计划
#####################

所有的课程都应该有一个描述课程目的的课程计划。创建计划并将它放在每个所支持语言的 ``lesson_plans`` 目录下。

.. _step6:

第六步: 反馈给社区
###################

如果你有了一个有助于帮助人们理解web应用程序安全的课程，请将它贡献给社区。你可以将课程发送给维护WebGoat项目的负责人。

非常感谢！

WebGoat团队。

**恭喜你完成了本次课程**

