<style>
img{display:block;margin-left: auto;   margin-right: auto }
</style>

##Python

![](images/9-4/pythonlogo.png)

Python是一种广泛使用的编程语言,这是高度可读的,这使得它比许多其他语言更容易学习。Python支持模块和包,可以嵌入到现有的应用程序。本节中的示例要先熟悉Python。如何使用Python,资源(“入门”)(https://www.python.org/about/gettingstarted/)[Python.org]页面(https://www.python.org/)。

### 视觉和文本编程

为什么要使用文本编程可视化编程环境？正如我们在1.1章所讨论的,可视化编程也有很多优点。它允许您创建程序没有特殊的语法学习。然而,视觉程序可以变得杂乱,达不到的功能。例如,Python提供了更多成为可能的方法来编写条件语句(if/then)和while。Python是一种强大的工具,可以扩展Dynamo的功能,允许您替换许多节点和一些简洁的代码行.

**可视化程序:**
![](images/9-4/python-nodes.png)

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

### Python的节点

像代码块,Python节点是一个编程接口在一个可视化的编程环境。　　Python节点可以找到在节点库下*核心>脚本*。双击节点打开python脚本编辑器(你也可以右键单击节点并选择*编辑…*)。

![Script Editor](images/9-4/Exercise/Python/python04.png)

> 你会注意到一些样板文本,旨在帮助你，需要引用节点库。输入存储在数组中。值返回给发Dynamo给变量。

Autodesk.DesignScript几何库允许您使用点符号。有关发Dynamo语法的更多信息,请参考章节7.2.输入一个几何类型如“点。将弹出一个列表的创建和查询点的方法。

[DesignScript Guide](http://dynamobim.org/wp-content/uploads/forum-assets/colin-mccroneautodesk-com/07/10/Dynamo_language_guide_version_1.pdf).

![](images/9-4/Exercise/Python/python14.png)

>方法包括构造函数,如* ByCoordinates * *添加*等操作,和查询* X *,* Y *和* * Z坐标。

### 练习

>下载示例文件,伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。 [Python_Custom-Node.dyn](datasets/9-4/Python-CustomNode.dyn)

　在这个例子中,我们将编写一个python脚本,创建模式从一个模块,并将其转化为一个自定义节点。
　首先,让我们创建我们模块使用Dynamo节点。

![](images/9-4/Exercise/Python/python01.png)

> 1. **Rectangle.ByWidthLength:**矩形,将是创建的基础。.
  2.	**Surface.ByPatch:** 矩形连接到“* closedCurve
*”输入创建底面。


![](images/9-4/Exercise/Python/python02.png)


>1.	**Geometry.Translate:**矩形连接到“*几何*”输入移动它,使用一个代码块来指定我们厚度。
2.	**Polygon.Points:** 查询矩形提取角点。
3.	**Geometry.Translate:**使用一个代码块来创建一个列表,四个值对应于四个点.
4.	**Polygon.ByPoints:** 用点重建多边形。.
5.	**Surface.ByPatch:** 连接多边形创建顶面。


现在,我们有了自己的顶部和底部表面,创建的固体。

![](images/9-4/Exercise/Python/python03.png)
>1.	**List.Create:** 矩形和多边形顶部底部连接到索引输入。
2.	**Surface.ByLoft:**两个文件创建的固体。
3.	**List.Create:**连接前,一边,和底部表面的索引输入，创建一个List.
4.	**Solid.ByJoinedSurfaces:** 加入表面创建模块.

把Python脚本节点拖放到工作区。

![](images/9-4/Exercise/Python/python05.png)
> 添加额外的输入节点,关闭编辑器并单击+图标的节点上。输入[0],[1],等代表在一个列表上的项目

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


接下来我们需要考虑哪些信息？首先,我们需要知道固体的尺寸来确定距离。我们将不得不使用边缘曲线几何创建一个边界框。

![](images/9-4/Exercise/Python/python07.png)
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


我们将翻译和旋转固体,用几何、变换操作。通过查看几何学。转换节点,我们知道我们需要一个源坐标系统和目标坐标系。将固体上下坐标系固定,而目标为每个模块排列不同的坐标系统。


![](images/9-4/Exercise/Python/python15.png)
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

> 保存Python脚本通过点击接受变化和输入值插入节点。您应该看到一个固定的模式.

![](images/9-4/Exercise/Python/python10.png)

> 尝试改变数值来创建不同的模式。你也可以改变固体模块本身的参数来达到不同效果。

现在,我们已经创建了一个有用的python脚本,让我们将其保存为一个自定义节点。选择python脚本节点,右键单击并选择“新节点的选择。”


![](images/9-4/Exercise/Python/python11.png)

> 分配一个名称、描述和分类。

打开新编辑自定义节点的工作空间。


![](images/9-4/Exercise/Python/python12.png)

> 1. **Inputs:**改变输入的名字是更具描述性和添加数据类型、默认值。
2.	**Output:** 改变输出名称保存节点.

![](images/9-4/Exercise/Python/python13.png)

> 自定义节点反映了我们刚才做出的更改。


