## 创建一个自定义节点

Dynamo提供了集中不同的方法来创建定制节点，你可以从开始构建定制节点，从现有的图、或者在C#中。在本节中，我们讲讲解如何在现有Dynamo图中，构建一个自定义节点，这个方法是清理工作空间以及包装一系列的节点.

### 自定义节点UV映射

在下图中，我们从一个表面地图的一个点到另一个点，使用UV坐标。我们讲使用这个概念来创建一个引用panelized表面在xy表面曲线，我们将创建四周panelization这里，但是我们使用相同的逻辑，我们可以创建一个各种各样的面变和UV映射，这个定制节点开发的一个很好的机会，因为我们将能够重复类似的过程更容易在这个图标上或者是在其他工作中能够用到的重要节点，也是可以简化我们工作中的步骤.从而达到提高工作效率.

![](images/9-2/uvMap2-01-01.jpg)

### 创建一个自定义节点从现有的图

> 下载并解压缩示例文件对于这个练习(右击并选择“链接另存为…”)。示例文件的完整列表可以在附录中找到.[UV-CustomNode.zip](datasets/9-2/UV-CustomNode.zip)

我们首先创建一个图，我们想把它做成一个定制节点，在这个例子中，我们讲创建一个图，地图表面要从最基础的多边形开始，在这个UV映射过程中，使用UV坐标，使它适合一个定制节点，表面和UV空间有更多的数据和信息，参见5.5节。* UVmapping_Custom-Node完全图.*zip文件下载.

![Exercise](images/9-2/UVmapping01.png)
> 1. **Code Block:** 创建一个范围的10数字45至- 45使用一个代码块。
2. **Point.ByCoordinates:** 代码块的输出连接到“x”和“y”输入和交叉引用的接头。现在应该有一个网格点
3. **Plane.ByOriginNormal:** *“点”*输出连接到*“起源”*输入.创建一个平面的每个点,默认的法向量(0,0,1)将被使用.
4.  **Rectangle.ByWidthLength:** 连接从上一步进入**平面**输入,并使用一个代码块* 10 *指定宽度和长度。


现在,您应该看到一个矩形网格,使用UV坐标让矩形映射到目标表面.

![Exercise](images/9-2/UVmapping02.png)
>1. **Polygon.Points:** 矩形前一步的输出连接到*“多边形”*输入提取每个矩形的角点.这些点我们将映射到目标表面.
2. **Rectangle.ByWidthLength:** 使用一个代码块的值* 100 *指定一个矩形的宽度和长度。这将是我们的基础表面的边界.
3. **Surface.ByPatch:** 连接矩形从上一步*的closedCurve *输入创建一个基础表面.
4. **Surface.UVParameterAtPoint:** 把* * *多边形的输出点。分*节点和* * *表面的输出“表面”。ByPatch *节点返回每一点.

现在,我们有一个基础表面和一组UV坐标,可以导入一个目标表面和表面之间的映射的点。

![Exercise](images/9-2/UVmapping03.png)
>1. **File Path:**选择您想要导入的文件路径表面.应该.SAT文件类型。点击*“浏览…“*按钮,导航到*UVmapping_srf.*文件从zip文件下载.
2. **Geometry.ImportFromSAT:**将文件路径连接到导入表面。您应该看到表面几何预览.
3. **UV:** 连接* UV参数输出.U *和*.V *节点.
4. **Surface.PointAtParameter:**连接导入的表面以及u和v坐标。现在您应该看到一个3 d网格点表面.


最后一步是使用3 d点构造矩形表面.

![Exercise](images/9-2/UVmapping04.png)
>1.	**PolyCurve.ByPoints:**通过点连接表面的点构造一个polycurve
2. **Boolean:** 一个布尔值添加到工作区并将其连接到*的connectLastToFirst *输入和关闭polycurves切换为True。您现在应该看到矩形映射到表面。
3. **Surface.ByPatch:** 连接polycurves *的closedCurve *输入构建表面.

现在让我们选择想要的节点做成一个定制节点,我们想要的输入和输出节点。我们希望定制节点尽可能灵活,所以它应该可以映射任何多边形,不仅仅是矩形。

![Exercise](images/9-2/UVmapping05.png)

> 选择上面的节点(从* Polygon.Points *),右键单击工作区并选择* *

![Exercise](images/9-2/UVmapping06.png)

>在自定义节点属性对话框中,指定一个名称、描述和分类定制点.

![Exercise](images/9-2/UVmapping07.png)

> 自定义节点大大清理工作区。注意,输入和输出都被命名为基于原始节点。编辑自定义节点使自己更容易记的名称.

![Exercise](images/9-2/UVmapping08.png)

> 双击自定义节点编辑它,这将打开节点的内部.
1. **Inputs:** 输入名称更改为* baseSurface *和* targetSurface *.
2. **Outputs:** 添加一个额外的输出映射的多边形.

>保存自定义工作区节点并返回到界面.

![Exercise](images/9-2/UVmapping09.png)

> **MapPolygonsToSurface** 节点反映了我们刚才做出的更改.























