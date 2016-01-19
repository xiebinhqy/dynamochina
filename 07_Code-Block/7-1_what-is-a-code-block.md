## 什么是*Code Block*？

*Code block*是Dynamo中一个特殊的节点。它是帮助我们项目参数化的工具。虽然它名字中的“代码”二字可能会吓到一些非码农，但其实它既易用也实用。初学者可以使用少量的代码让工作变得高效，而熟练的使用者可以用它来调用dynamo的节点。我们非常建议您熟悉*Code block*这个节点的用法，本章节就将向您介绍这方面的内容。

![Code Block Intro](images/7-1/daisy.png)

###Code Block概览
简单来说，*Code Block*是一个可视化编程环境中的一个脚本接口。它可以当作数值、字符串、公式等。当你在*Code Block*中定义任何变量时，该变量将自动添加到输入的节点中：

使用*Code Block*节点用户可以灵活的指定输入的内容。以下展示了几种不同的方法来创建一个坐标为(10,5,0)的点:
![Flexibility](images/7-2/flexibility.png)

As you learn more of the available functions in the library, you might even find that typing “Point.ByCoordinates” is faster than searching in the library and finding the proper node.  When you type in *"Point."* for example, Dynamo will display a list of possible functions to apply to a Point.  This makes the scripting more intuitive and will help with learning how to apply functions in Dynamo.

### 创建Code Block节点
Code Block节点可以在*Core>Input>Actions>Code Block*下面找到。但是最快的方法是直接双击工作区。由于这个节点经常被用到，所以拥有双击的特权。

![Code Block Intro](images/7-1/uicb.png)

### 数值、字符串和公式
Code block可以灵活地使用数据类型。用户可以快速的定义数值、字符串和公式并将其输出。

在下图中，你能看到通过原有方法（左边图片）创建数据有点繁琐，用户需要搜索指定数据类型的节点添加到工作区，再输入数据。而使用Code block只需要在想添加节点的地方双击工作区，然后输入带简单语法的数据。

![Obsolete Nodes](images/7-3/obsolete01.png)
>  *number*、*string* 和 *formula*这三个节点在有了*Code Block*之后已经过时了。

