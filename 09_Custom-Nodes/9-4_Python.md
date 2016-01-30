<style>
img{display:block;margin-left: auto;   margin-right: auto }
</style>

##Python

![](images/9-4/pythonlogo.png)

Python is a widely used programming language whose popularity has a lot to do with its style of syntax. It's highly readable, which makes it easier to learn than many other languages. Python supports modules and packages, and can be embedded into existing applications. The examples in this section assume a basic familiarity with Python. For information about how to get up and running with Python, a good resource is the ["Getting Started"](https://www.python.org/about/gettingstarted/) page on [Python.org](https://www.python.org/).


Python是一种广泛使用的编程语言,这是高度可读的,这使得它比许多其他语言更容易学习。Python支持模块和包,可以嵌入到现有的应用程序。本节中的示例要先熟悉Python。如何使用Python,资源(“入门”)(https://www.python.org/about/gettingstarted/)[Python.org]页面(https://www.python.org/)。



###Visual vs. Textual Programming

### 视觉和文本编程

Why would you use textual programming in Dynamo's visual programming environment? As we discussed in chapter 1.1, visual programming has many advantages. It allows you to create programs without learning special syntax in an intuitive visual interface. However, a visual program can become cluttered, and can at times fall short in functionality. For example, Python offers much more achieveable methods for writing conditional statements (if/then) and looping.  Python is a powerful tool that can extend the capabilities of Dynamo and allow you to replace many nodes with a few concise lines of code. 

为什么要使用文本编程可视化编程环境？正如我们在1.1章所讨论的,可视化编程也有很多优点。它允许您创建程序没有特殊的语法学习。然而,视觉程序可以变得杂乱,达不到的功能。例如,Python提供了更多成为可能的方法来编写条件语句(if/then)和while。Python是一种强大的工具,可以扩展Dynamo的功能,允许您替换许多节点和一些简洁的代码行.

**Visual Program:**

**可视化程序:**
![](images/9-4/python-nodes.png)

**Textual Program:**

**文本的程序**
```
import clr
clr.AddReference('ProtoGeometry')
from Autodesk.DesignScript.Geometry import *

solid = IN[0]
seed = IN[1]
xCount = IN[2]
yCount = IN[3]

solids = []

yDist = solid.BoundingBox.MaxPoint.Y-solid.BoundingBox.MinPoint.Y
xDist = solid.BoundingBox.MaxPoint.X-solid.BoundingBox.MinPoint.X

for i in xRange:
	for j in yRange:
		fromCoord = solid.ContextCoordinateSystem
		toCoord = fromCoord.Rotate(solid.ContextCoordinateSystem.Origin,Vector.ByCoordinates(0,0,1),(90*(i+j%val)))
		vec = Vector.ByCoordinates((xDist*i),(yDist*j),0)
		toCoord = toCoord.Translate(vec)
		solids.append(solid.Transform(fromCoord,toCoord))

OUT = solids
```

###The Python Node
### Python的节点

Like code blocks, Python nodes are a scripting interface within a visual programming environment.
The Python node can be found under *Core>Scripting* in the library. Double clicking the node opens the python script editor (you can also right click on the node and select *Edit...*).

像代码块,Python节点是一个编程接口在一个可视化的编程环境。　　Python节点可以找到在节点库下*核心>脚本*。双击节点打开python脚本编辑器(你也可以右键单击节点并选择*编辑…*)。

![Script Editor](images/9-4/Exercise/Python/python04.png)

> You’ll notice some boilerplate text at the top, which is meant to help you reference the libraries you’ll need. Inputs are stored in the IN array. Values are returned to Dynamo by assigning them to the OUT variable.

> 你会注意到一些样板文本,旨在帮助你，需要引用节点库。输入存储在数组中。值返回给发Dynamo给变量。

The Autodesk.DesignScript.Geometry library allows you to use dot notation similar to Code Blocks. For more information on Dynamo syntax, refer to chapter 7.2 as well as the

Autodesk.DesignScript几何库允许您使用点符号。有关发Dynamo语法的更多信息,请参考章节7.2.输入一个几何类型如“点。将弹出一个列表的创建和查询点的方法。

[DesignScript Guide](http://dynamobim.org/wp-content/uploads/forum-assets/colin-mccroneautodesk-com/07/10/Dynamo_language_guide_version_1.pdf).

![](images/9-4/Exercise/Python/python14.png)

> Methods include constructors such as *ByCoordinates*, actions like *Add*, and queries like *X*, *Y* and *Z* coordinates.
>方法包括构造函数,如* ByCoordinates * *添加*等操作,和查询* X *,* Y *和* * Z坐标。


###Exercise

### 练习

>下载示例文件,伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。 [Python_Custom-Node.dyn](datasets/9-4/Python-CustomNode.dyn)

In this example, we will write a python script that creates patterns from a solid module, and turn it into a custom node.
First, let’s create our solid module using Dynamo nodes.

　在这个例子中,我们将编写一个python脚本,创建模式从一个模块,并将其转化为一个自定义节点。
　首先,让我们创建我们模块使用Dynamo节点。

![](images/9-4/Exercise/Python/python01.png)

> 1. **Rectangle.ByWidthLength:** Create a rectangle that will be the base of our solid.
> 1. **Rectangle.ByWidthLength:**矩形,将是创建的基础。
2.	**Surface.ByPatch:** Connect the rectangle to the ‘*closedCurve*’ input to create the bottom surface.
2.	**Surface.ByPatch:** 矩形连接到“* closedCurve *”输入创建底面。


![](images/9-4/Exercise/Python/python02.png)


>1.	**Geometry.Translate:** Connect the rectangle to the ‘*geometry*’ input to move it up, using a code block to specify the base thickness of our solid.
>1.	**Geometry.Translate:**矩形连接到“*几何*”输入移动它,使用一个代码块来指定我们厚度。
2.	**Polygon.Points:** Query the translated rectangle to extract the corner points.
2.	**Polygon.Points:** 查询矩形提取角点。
3.	**Geometry.Translate:** Use a code block to create a list of four values corresponding to the four points, translating one corner of the solid up.
3.	**Geometry.Translate:**使用一个代码块来创建一个列表,四个值对应于四个点.
4.	**Polygon.ByPoints:** Use the translated points to reconstruct the top polygon.
4.	**Polygon.ByPoints:** 用点重建多边形。.
5.	**Surface.ByPatch:** Connect the polygon to create the top surface.
5.	**Surface.ByPatch:** 连接多边形创建顶面。

Now that we have our top and bottom surfaces, let’s loft between the two profiles to create the sides of the solid.

现在,我们有了自己的顶部和底部表面,创建的固体。

![](images/9-4/Exercise/Python/python03.png)
>1.	**List.Create:** Connect the bottom rectangle and the top polygon to the index inputs.
>1.	**List.Create:** 矩形和多边形顶部底部连接到索引输入。
2.	**Surface.ByLoft:** Loft the two profiles to create the sides of the solid.
2.	**Surface.ByLoft:**两个文件创建的固体。
3.	**List.Create:** Connect the top, side, and bottom surfaces to the index inputs to create a list of surfaces.
3.	**List.Create:**连接前,一边,和底部表面的索引输入，创建一个List.
4.	**Solid.ByJoinedSurfaces:** Join the surfaces to create the solid module.
4.	**Solid.ByJoinedSurfaces:** 加入表面创建模块.

Now that we have our solid, let’s drop a Python Script node onto the workspace. 

把Python脚本节点拖放到工作区。


![](images/9-4/Exercise/Python/python05.png)
> To add additional inputs to the node, close the editor and click the + icon on the node. The inputs are named IN[0], IN[1], etc. to indicate that they represent items in a list.
> 添加额外的输入节点,关闭编辑器并单击+图标的节点上。输入[0],[1],等代表在一个列表上的项目

Let’s start by defining our inputs and output. Double click the node to open the python editor. 

让我们首先定义输入和输出。双击打开python编辑器的节点。

![](images/9-4/Exercise/Python/python06.png)
```
import clr
clr.AddReference('ProtoGeometry')
from Autodesk.DesignScript.Geometry import *

#The solid module to be arrayed
solid = IN[0]
#A number that determines which rotation pattern to use
seed = IN[1]
#The number of solids to array in the X and Y axes
xCount = IN[2]
yCount = IN[3]

#Create an empty list for the arrayed solids
solids = []

#Assign your output to the OUT variable.
OUT = solids
```

This code will make more sense as we progress in the exercise.  Next we need to think about what information is required in order to array our solid module. First, we will need to know the dimensions of the solid to determine the translation distance. Due to a bounding box bug, we will have to use the edge curve geometry to create a bounding box.

接下来我们需要考虑哪些信息？首先,我们需要知道固体的尺寸来确定距离。我们将不得不使用边缘曲线几何创建一个边界框。

![](images/9-4/Exercise/Python/python07.png)
> A look at the Python node in Dynamo. Notice that we're using the same syntax as we see in the titles of the nodes in Dynamo. The commented code is below.
> 看看Python节点，请注意,我们使用相同的语法，下面的注释代码。

```
import clr
clr.AddReference('ProtoGeometry')
from Autodesk.DesignScript.Geometry import *

#Inputs
solid = IN[0]
seed = IN[1]
xCount = IN[2]
yCount = IN[3]

#Create an empty list for the arrayed solids
solids = []
# Create an empty list for the edge curves
crvs = []

#Loop through edges and append corresponding curve geometry to the list
for edge in solid.Edges:
	crvs.append(edge.CurveGeometry)
	
#Get the bounding box of the curves
bbox = BoundingBox.ByGeometry(crvs)

#Get the X and Y translation distance based on the bounding box
yDist = bbox.MaxPoint.Y-bbox.MinPoint.Y
xDist = bbox.MaxPoint.X-bbox.MinPoint.X

#Assign your output to the OUT variable.
OUT = solids
```

Since we will be both translating and rotating the solid modules, let’s use the Geometry.Transform operation. By looking at the Geometry.Transform node, we know that we will need a source coordinate system and a target coordinate system to transform the solid. The source is the context coordinate system of our solid, while the target will be a different coordinate system for each arrayed module. That means we will have to loop through the x and y values to transform the coordinate system differently each time. 

我们将翻译和旋转固体,用几何、变换操作。通过查看几何学。转换节点,我们知道我们需要一个源坐标系统和目标坐标系。将固体上下坐标系固定,而目标为每个模块排列不同的坐标系统。


![](images/9-4/Exercise/Python/python15.png)
> A look at the Python node in Dynamo. The commented code is below.

> 看看Python节点，下面的注释代码。

```
import clr
clr.AddReference('ProtoGeometry')
from Autodesk.DesignScript.Geometry import *

#Inputs
solid = IN[0]
seed = IN[1]
xCount = IN[2]
yCount = IN[3]

#Create an empty list for the arrayed solids
solids = []
# Create an empty list for the edge curves
crvs = []

#Loop through edges and append corresponding curve geometry to the list
for edge in solid.Edges:
	crvs.append(edge.CurveGeometry)
	
#Get the bounding box of the curves
bbox = BoundingBox.ByGeometry(crvs)

#Get the X and Y translation distance based on the bounding box
yDist = bbox.MaxPoint.Y-bbox.MinPoint.Y
xDist = bbox.MaxPoint.X-bbox.MinPoint.X

#get the source coordinate system
fromCoord = solid.ContextCoordinateSystem
 
#Loop through X and Y
for i in range(xCount):
	for j in range(yCount):
		#Rotate and translate the coordinate system
		toCoord = fromCoord.Rotate(solid.ContextCoordinateSystem.Origin,Vector.ByCoordinates(0,0,1),(90*(i+j%seed)))
		vec = Vector.ByCoordinates((xDist*i),(yDist*j),0)
		toCoord = toCoord.Translate(vec)
		#Transform the solid from the source coord system to the target coord system and append to the list
		solids.append(solid.Transform(fromCoord,toCoord))
	
```

![](images/9-4/Exercise/Python/python09.png)

> Save the Python script by clicking ‘Accept Changes’ and plug the input values into the node. You should see a pattern of solids.
> 保存Python脚本通过点击接受变化和输入值插入节点。您应该看到一个固定的模式.

![](images/9-4/Exercise/Python/python10.png)

> Try changing the seed value to create different patterns. You can also change the parameters of the solid module itself for different effects.
> 尝试改变数值来创建不同的模式。你也可以改变固体模块本身的参数来达到不同效果。

Now that we have created a useful python script, let’s save it as a custom node. Select the python script node, right-click and select ‘New Node From Selection.’ 

现在,我们已经创建了一个有用的python脚本,让我们将其保存为一个自定义节点。选择python脚本节点,右键单击并选择“新节点的选择。”


![](images/9-4/Exercise/Python/python11.png)

> Assign a name, description, and category.

> 分配一个名称、描述和分类。

This will open a new workspace in which to edit the custom node. 

打开新编辑自定义节点的工作空间。


![](images/9-4/Exercise/Python/python12.png)

> 1. **Inputs:** Change the input names to be more descriptive and add data types and default values. 
> 1. **Inputs:**改变输入的名字是更具描述性和添加数据类型、默认值。
2.	**Output:** Change the output name Save the node as a .dyf file.
2.	**Output:** 改变输出名称保存节点.

![](images/9-4/Exercise/Python/python13.png)

> The custom node reflects the changes we just made.

> 自定义节点反映了我们刚才做出的更改。


