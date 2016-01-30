<style>
img{display:block;margin-left: auto;   margin-right: auto }
</style>

##Python and Revit

既然我们已经演示了如何在Dynamo使用Python脚本,让我们看看Revit库连接到脚本环境中。记住,我们Dynamo核心节点的前三行下面的代码块。导入Revit节点、Revit元素和Revit 文件管理,我们需要添加更多的线

```
import clr
clr.AddReference('ProtoGeometry')
from Autodesk.DesignScript.Geometry import *

# Import RevitNodes
clr.AddReference("RevitNodes")
import Revit

# Import Revit elements
from Revit.Elements import *

# Import DocumentManager
clr.AddReference("RevitServices")
import RevitServices
from RevitServices.Persistence import DocumentManager

import System
```

为任何Revit任务提供了自定义脚本。通过结合视觉Revit API脚本编程,协作和工具开发显著提高。例如,BIM经理和设计师可以一起同一平台上公平。他们可以提高模型的设计和执行。

![Exercise](images/9-4/pythonRevit.png)

### 特定于平台的api

Dynamo项目是扩大了平台实现的范围。Dynamo增加程序,用户将获得特定于平台的api放置于Python脚本环境。虽然Revit是本节的个案例,我们可以预测未来更多的章节提供全面的脚本在其他平台上的教程。


[IronPython](http://ironpython.net/) 


以下示例展示的方法来实现从Dynamo使用Python Revit-specific操作。更详细检查Dynamo和Revit Python的关系,请参考

[Dynamo Wiki page](https://github.com/DynamoDS/Dynamo/wiki/Python-0.6.3-to-0.7.x-Migration).Python Revit是另一个有用的资源 [Revit Python Shell ](https://github.com/architecture-building-systems/revitpythonshell)

### 练习 01

>创建一个新的Revit项目。下载示例文件,伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。

[Revit-Doc.dyn](datasets/9-5/Revit-Doc.dyn)

在这些练习中,我们将探讨基本的Python脚本Revit、Dynamo。将关注Revit文件和处理ID,以及Revit和Dynamo之间的关系.



![Exercise](images/9-4/Exercise/Revit/Images/RevitPython - 10.png)

> 这是一个切割和干燥方法获取*doc*,* uiapp *,app* Revit文件与你的发电机sesson。程序员在Revit API可能会注意到之前看中的商品列表。如果这些项目不熟悉,我们将使用其他的例子在下面的练习。

我们如何导入Revit在Dynamo服务和检索文档的数据:

![Exercise](images/9-4/Exercise/Revit/Images/RevitPython - 06.png)

> 看看Python节点,下面的注释代码。

```
import clr
# Import DocumentManager
clr.AddReference("RevitServices")
import RevitServices
from RevitServices.Persistence import DocumentManager

doc = DocumentManager.Instance.CurrentDBDocument
uiapp = DocumentManager.Instance.CurrentUIApplication
app = uiapp.Application

#Assign your output to the OUT variable
#OUT is defined as a list of three items
OUT=[doc,uiapp,app]
```


### 练习  02

> Appendix.>下载示例文件,伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。 [Revit-ReferenceCurve.dyn](datasets/9-5/Revit-ReferenceCurve.dyn)

在这个练习中,我们将做一个简单的模型曲线Revit Python使用Dynamo节点。

![](images/9-4/Exercise/Revit/Images/RevitPython - 08.png)

> 我们将首先创建两个参考点在Dynamo中节点.

> 开始创建一个新的概念在Revit。上图中创建的一组节点。我们将首先两个参考点从Dynamo中创建在Revit。
1. **重要提示-当执行Revit操作,确定运行模式设置为“手动”。否则程序将比较卡.**
2. 创建一个代码块,并给它一个值“0;”
3. 把这个值代入ReferencePoint。ByCoordinates节点X,Y,和Z输入。
4. 创建三个滑块,从-100年到100年,增长为1。
5. ReferencePoint连接每一个滑块。ByCoordinates节点
6. Python节点添加到工作区,点击“+”按钮。节点上添加另一个输入和两个引用点输入。打开Python节点。

![Exercise](images/9-4/Exercise/Revit/Images/RevitPython - 07.png)

>看看Python,下面的注释代码.

> 1. **System.Array:**Revit系统需要一个数组作为输入(而不是一个Python列表)。这仅仅是一个多行代码,但是注意参数类型将促进在Revit Python编程。

```
import clr

# Import RevitNodes
clr.AddReference("RevitNodes")
import Revit
# Import Revit elements
from Revit.Elements import *
import System

#define inputs
startRefPt = IN[0]
endRefPt = IN[1]

#define system array to match with required inputs
refPtArray = System.Array[ReferencePoint]([startRefPt, endRefPt])
#create curve by reference points in Revit
OUT = CurveByPoints.ByReferencePoints(refPtArray)

```

![Exercise](images/9-4/Exercise/Revit/Images/RevitPython - 09.png)
> 我们已经创建了两个参考点,一条线连接使用Python。让我们看这一点进一步在接下来的练习。

### 练习  03
> 下载并解压缩示例文件伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。 [Revit-StructuralFraming.zip](datasets/9-5/Revit-StructuralFraming.zip)

>这个练习使它简单,但要连接数据和几何Revit。让我们首先打开Revit-StructuralFraming.rvt。一旦打开Dynamno文件和 Revit-StructuralFraming.dyn.

![](images/9-4/Exercise/Revit/Images/RevitPython - 04.png)
> 这个Revit文件是基本的。两个参考曲线:想让这些曲线进入Dynamo　

![](images/9-4/Exercise/Revit/Images/RevitPython - 01a.png)
> 在这个文件中,我们有一组节点插入5个输入Python的节点。
1. **Select Model Element Nodes:**点击选择按钮为每个Revit并选择相应的曲线
2. **Code Block:** 使用语法*“0 . . 1 . .# x;“*,连接一个整数滑块从0到20 * x *输入。这指定数量的两条曲线之间的梁画.
3. **Structural Framing Types:** 我们将选择默认W12x26梁从下拉菜单中。
4. **Levels:** 选择 "Level 1".【平面】

![](images/9-4/Exercise/Revit/Images/RevitPython - 00.png)

> 这段代码在Python中更密集：

```
import clr
#import Dynamo Geometry
clr.AddReference('ProtoGeometry')
from Autodesk.DesignScript.Geometry import *
# Import RevitNodes
clr.AddReference("RevitNodes")
import Revit
# Import Revit elements
from Revit.Elements import *
import System

#Query Revit elements and convert them to Dynamo Curves
crvA=IN[0].Curves[0]
crvB=IN[1].Curves[0]

#Define input Parameters
framingType=IN[3]
designLevel=IN[4]

#Define "out" as a list
OUT=[]

for val in IN[2]:
	#Define Dynamo Points on each curve
	ptA=Curve.PointAtParameter(crvA,val)
	ptB=Curve.PointAtParameter(crvB,val)
	#Create Dynamo line
	beamCrv=Line.ByStartPointEndPoint(ptA,ptB)
	#create Revit Element from Dynamo Curves
	beam = StructuralFraming.BeamByCurve(beamCrv,designLevel,framingType)
	#convert Revit Element into list of Dynamo Surfaces
	OUT.append(beam.Faces)

```
![](images/9-4/Exercise/Revit/Images/RevitPython - 03.png)

> 梁在Revit中,我们有一个数组生成两条曲线的结构元素。注意:这不是一个实际的例子…结构元素作为一个例子用于本机Revit实例

![](images/9-4/Exercise/Revit/Images/RevitPython - 05.png)

> 在Dynamo中,我们可以看到结果。Watch3D梁的节点指的是查询Revit元素。

注意,我们有一个持续的数据从Revit环境转换至Dynamo。总之,如何处理流程方面:

2. 选择Revit元素
3. Revit元素转换为Dynamo曲线
4. Dynamo曲线划分为一系列的Dynamo点
5. 使用Dynamo分两条曲线之间创建Dynamo线
6. 创建Revit光束可以引用Dynamo
7. 输出Dynamo表面通过查询Revit梁



这听起来可能有点重了,编辑曲线Revit使它变得更简单,重新运行.

![](images/9-4/Exercise/Revit/Images/RevitPython - 01.png)

> 更新在Revit refernce曲线,得到梁的新数组。





