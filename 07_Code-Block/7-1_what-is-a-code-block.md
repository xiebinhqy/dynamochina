## 什么是Code Block？
Code block is the special sauce of Dynamo.  It is a powerful tool which allows the user to work fluidly and parametrically throughout a project.  While the term 'code block' may be a little intimidating to non-programmers, it is both easy to use and robust.  A beginner can use the code block efficiently with minimal coding, and an advanced user can define scripted definitions to be recalled elsewhere in a Dynamo definition.  We highly recommend that you get familiar with code block as you develop your Dynamo definitions, and this chapter demonstrates how and why the code block is awesome.

Code block是Dynamo中一个特殊的节点。它

![Code Block Intro](images/7-1/daisy.png)

###Code Block概览
In short, code blocks are a text-scripting interface within a visual-scripting environment.  They can be used as numbers, strings, formulas, and other data types.  The code block is designed for Dynamo, so one can define arbitrary variables in the code block, and those variables are automatically added to the inputs of the node:
简单来说，code blocks是一个可视化编程环境中的一个脚本接口。它可以当作数值、字符串、公式等。

With code blocks, a user has the flexibility to decide how to specify inputs. Here are several different ways to make a basic point with coordinates *(10, 5, 0)*:
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

