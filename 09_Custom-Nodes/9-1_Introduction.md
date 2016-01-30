## Custom Nodes

## 自定义节点

Dynamo offers many core nodes for a wide-range of visual programming tasks. Sometimes a quicker, more elegant, or more easily shared solution is to build your own nodes. These can be reused among different projects, they make your graph clearer and cleaner, and they can be pushed to the package manager and shared with the global Dynamo community.

Dynamo提供了很多核心的节点供广泛的可视化编任务，一个更快、更便捷、更容易的解决方案是建立自定义节点的前提。这些在不同的项目中可以通用的，他们让你的图形界面更加清晰，思路更加明了，可以共享到Dynamo论坛社区.

![](images/9-1/cn.jpg)

###Cleaning up Your Graph

### 整理节点

Custom Nodes are constructed by nesting other nodes and custom nodes inside of a "Dynamo Custom Node," which we can think of conceptually as a container. When this container node is executed in your graph, everything inside it will be executed to allow you to reuse and share a useful combination of nodes.

自定义节点是嵌其他节点和节内部定制节点，我们从概念上可以理解为一个容器，当这个容器节点去执行你的图，执行自定义的每个节点，从达成用户的目的.

###Adapting to Change

### 自适应

When you have multiple copies of a custom node in your graph, you can update all of them by editing the base custom node. This allows you to update your graph seamlessly by adapting to any changes that may occur in workflow or design.

在你的图中多次使用同一类似的节点时，你可以通过编辑基本的定制节点，让形成一个自定义节点，这可以更新你的工作流程和在设计中可能发生的任何变化.

###Work Sharing

### 工作公用

Arguably the best feature of custom nodes is their work sharing capabilities. If a "power user" creates a complex Dynamo graph and hands it off to a designer who is new to Dynamo, he/she can condense the graph to the bare essentials for design interaction.  The custom node can be opened to edit the internal graph, but the "container" can be kept simple.  With this process, custom nodes allow Dynamo users to design a graph that is clean and intuitive.

可以说它们的工作能力就是能够更好的定制节点，如果一个“超级用户”创造了一个复杂的电机图和手，一个设计师可以凝结最基本的图形设计交互，自定义节点可以打开编辑的内部图，单可以保证最简单节点内部。在这一过程中，自定义节点允许Dynamo设计一个更加干净和直观的节点.


![](images/9-1/customNodeDiagram.jpg)

###Many Ways to Build a Node

### 建立一个节点可以有许多方法

There are a wide variety of ways to build custom nodes in Dynamo. In the examples in this chapter, we'll create custom nodes directly from the Dynamo UI.  If you are a programmer and you are interested in C# or Zero-Touch formatting, you can reference [this page ](https://github.com/DynamoDS/Dynamo/wiki/How-To-Create-Your-Own-Nodes)on the Dynamo Wiki for a more in-depth review.

有各种各样的方法来构建Dynamo自定义节点，在本章的例子中，我们讲从Dynamo创建自定义节点,如果你是个程序员，你感兴趣的是C#或Zero-Touch格式，你可以参考（这一页）(https://github.com/DynamoDS/Dynamo/wiki/How-To-Create-Your-Own-Nodes）的Dynamo更深入的研究.

### Custom Node Environment

### 定制节点环境

Let's jump into the custom node environment and make a simple node to calculate a percentage.  The custom node environment is different from the Dynamo graph environment, but the interaction is fundamentally the same. With that said, let's create our first custom node!

让我们进入环境，做一个简单的自定义节点。自定义节点环境不同于Dynamo的图形界面，但互动基本上是相同的，让我们来创建第一个定制节点。


![Custom Nodes Intro](images/9-1/CustomNodes01.png)

> To create a Custom Node from scratch, Launch Dynamo and select Custom Node, or type Ctrl + Shift + N from the canvas.

> 从头开始创建一个自定义节点,启动发电机并选择自定义节点,或类型Ctrl + Shift + N的画布

![Custom Nodes Dialog](images/9-1/CustomNodes02.png)

> Assign a name, description, and category in the Custom Node Properties dialog.

> 分配一个名称、描述和分类在定制节点属性对话框。
1. **Name:** Percentage
1. **名称:** 百分比.
2. **Description**: Calculate the percentage of one value in relation to another.
2. **说明书**: 计算一个值的比例关系到另一个地方。 
3. **Category:** Core.Math
3. **分类:** 数学核心

![Custom Nodes Canvas](images/9-1/CustomNodes03.png)

> This will open a canvas with a yellow background, indicating that you are working inside a custom node. In this canvas you have access to all of the core Dynamo nodes, as well as the **Input** and **Output** nodes, which label the data flowing into and out of the custom node.  They can be found in *Core>Input*.

这讲打开一个黄色的背景画布，这表明你已经在一个工作的定制节点，在这个画布上你可以访问所有的Dynamao核心节点，以及输入节点、输出节点，那个数据流入和流出的定制节点，这是它们最核心的。


![Custom Nodes Canvas](images/9-1/CustomNodes04.png)

> 1. **Inputs:** input nodes create input ports on the custom node. The syntax for an input node is *input_name : datatype = default_value(optional)*
> 1. **Inputs:**在输入端口输入定制节点，一个输入节点的语法* input_name:数据类型= default_value(默认值)*
2. **Outputs:** Similar to inputs, these will create and name output ports on the custom node.
2. **Outputs:** 类似于输出,定制节点输出端口.

You can save this custom node as a .dyf (as opposed to the standard .dyn) file and it will automatically be added to your session and future sessions. You will find the custom node in your library in the category that is specified in the custom node's properties.

你可以保存这个定制节点，它是一个标准的.dyn文件，它会自添加到你的文件目录，你会发现在你的节点库中可以找到你保存的自定义节点.

![Add to Library](images/9-1/CustomNodes05.png)

> Left: The Core > Math category of the default library
Right: Core > Math with the new custom node

> 左:核心的数学类别>默认库：
  右:核心>数学新定制节点


###Moving Forward

### 下一个话题

Now that we've created our first custom node, the next sections will dive deeper into custom node functionality and how to publish generic workflows.  In the following section, we'll look at developing a custom node that transfers geometry from one surface to another.

现在我们已经创建了第一个定制节点，接下来我们讲深入研究定制节点的功能和如何发布，在一下的部分中，我们讲看看开发一个自定义节点的传输几何表面从一个地方到另一个地方,这一点，我们下一章将详细讲诉.




