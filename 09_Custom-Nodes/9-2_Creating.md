## Creating a Custom Node
## 创建一个自定义节点


Dynamo offers several different methods for creating custom nodes. You can build custom nodes from scratch, from an existing graph, or explicitly in C#. In this section we will cover building a custom node in the Dynamo UI from an existing graph. This method is ideal for cleaning up the workspace, as well as packaging a sequence of nodes to reuse elsewhere.

Dynamo提供了集中不同的方法来创建定制节点，你可以从开始构建定制节点，从现有的图、或者在C#中。在本节中，我们讲讲解如何在现有Dynamo图中，构建一个自定义节点，这个方法是清理工作空间以及包装一系列的节点.

###Custom Nodes for UV Mapping

### 自定义节点UV映射

In the image below, we map a point from one surface to another using UV coordinates. We'll use this concept to create a panelized surface which references curves in the XY plane. We'll create quad panels for our panelization here, but using the same logic, we can create a wide variety of panels with UV mapping. This is a great opportunity for custom node development because we will be able to repeat a similar process more easily in this graph or in other Dynamo workflows.

在下图中，我们从一个表面地图的一个点到另一个点，使用UV坐标。我们讲使用这个概念来创建一个引用panelized表面在xy表面曲线，我们将创建四周panelization这里，但是我们使用相同的逻辑，我们可以创建一个各种各样的面变和UV映射，这个定制节点开发的一个很好的机会，因为我们将能够重复类似的过程更容易在这个图标上或者是在其他工作中能够用到的重要节点，也是可以简化我们工作中的步骤.从而达到提高工作效率.

![](images/9-2/uvMap2-01-01.jpg)

### Creating a Custom Node from an Existing Graph

### 创建一个自定义节点从现有的图

> Download and unzip the example files for this exercise (Right click and choose "Save Link As..."). A full list of example files can be found in the Appendix. [UV-CustomNode.zip](datasets/9-2/UV-CustomNode.zip)

> 下载并解压缩示例文件对于这个练习(右击并选择“链接另存为…”)。示例文件的完整列表可以在附录中找到.[UV-CustomNode.zip](datasets/9-2/UV-CustomNode.zip)

Let’s start by creating a graph that we want to nest into a custom node. In this example, we will create a graph that maps polygons from a base surface to a target surface, using UV coordinates. This UV mapping process is something we use frequently, making it a good candidate for a custom node. For more information on surfaces and UV space, see section 5.5. The complete graph is *UVmapping_Custom-Node.dyn* from the .zip file downloaded above.

我们首先创建一个图，我们想把它做成一个定制节点，在这个例子中，我们讲创建一个图，地图表面要从最基础的多边形开始，在这个UV映射过程中，使用UV坐标，使它适合一个定制节点，表面和UV空间有更多的数据和信息，参见5.5节。* UVmapping_Custom-Node完全图.*zip文件下载.

![Exercise](images/9-2/UVmapping01.png)
> 1. **Code Block:** Create a range of 10 numbers between 45 and negative 45 using a code block.
> 1. **Code Block:** 创建一个范围的10数字45至- 45使用一个代码块。
2. **Point.ByCoordinates:** Connect the output of the Code Block to the ‘x’ and ‘y’ inputs and set the lacing to cross-reference. You should now have a grid of points.
2. **Point.ByCoordinates:** 代码块的输出连接到“x”和“y”输入和交叉引用的接头。现在应该有一个网格点
3. **Plane.ByOriginNormal:** Connect the *‘Point’* output to the *‘origin’* input to create a plane at each of the points. The default normal vector of (0,0,1) will be used.
3. **Plane.ByOriginNormal:** *“点”*输出连接到*“起源”*输入.创建一个平面的每个点,默认的法向量(0,0,1)将被使用.
4.  **Rectangle.ByWidthLength:** Connect the planes from the previous step into the *‘plane’* input, and use a Code Block with a value of *10* to specify the width and length.
4.  **Rectangle.ByWidthLength:** 连接从上一步进入**平面**输入,并使用一个代码块* 10 *指定宽度和长度。


You should now see a grid of rectangles. Let’s map these rectangles to a target surface using UV coordinates.

现在,您应该看到一个矩形网格,使用UV坐标让矩形映射到目标表面.

![Exercise](images/9-2/UVmapping02.png)
>1. **Polygon.Points:** Connect the Rectangle output from the previous step to the *‘polygon’* input to extract the corner points of each rectangle. These are the points that we will map to the target surface.
>1. **Polygon.Points:** 矩形前一步的输出连接到*“多边形”*输入提取每个矩形的角点.这些点我们将映射到目标表面.
2. **Rectangle.ByWidthLength:** Use a Code Block with a value of *100* to specify the width and length of a rectangle. This will be the boundary of our base surface.
2. **Rectangle.ByWidthLength:** 使用一个代码块的值* 100 *指定一个矩形的宽度和长度。这将是我们的基础表面的边界.
3. **Surface.ByPatch:** Connect the Rectangle from the previous step to the *‘closedCurve’* input to create a base surface.
3. **Surface.ByPatch:** 连接矩形从上一步*的closedCurve *输入创建一个基础表面.
4. **Surface.UVParameterAtPoint:** Connect the *‘Point’* output of the *Polygon.Points* node and the *‘Surface’* output of the *Surface.ByPatch* node to return the UV parameter at each point.
4. **Surface.UVParameterAtPoint:** 把* * *多边形的输出点。分*节点和* * *表面的输出“表面”。ByPatch *节点返回每一点.

Now that we have a base surface and a set of UV coordinates, we can import a target surface and map the points between surfaces.

现在,我们有一个基础表面和一组UV坐标,可以导入一个目标表面和表面之间的映射的点。

![Exercise](images/9-2/UVmapping03.png)
>1. **File Path:** Select the file path of the surface you want to import. The file type should be .SAT. Click the *"Browse..."* button and navigate to the *UVmapping_srf.sat* file from the .zip file downloaded above.
>1. **File Path:**选择您想要导入的文件路径表面.应该.SAT文件类型。点击*“浏览…“*按钮,导航到*UVmapping_srf.*文件从zip文件下载.
2. **Geometry.ImportFromSAT:** Connect the file path to import the surface. You should see the imported surface in the geometry preview.
2. **Geometry.ImportFromSAT:**将文件路径连接到导入表面。您应该看到表面几何预览.
3. **UV:** Connect the UV parameter output to a *UV.U* and a *UV.V* node.
3. **UV:** 连接* UV参数输出.U *和*.V *节点.
4. **Surface.PointAtParameter:** Connect the imported surface as well as the u and v coordinates. You should now see a grid of 3D points on the target surface.\
4. **Surface.PointAtParameter:**连接导入的表面以及u和v坐标。现在您应该看到一个3 d网格点表面.

The final step is to use the 3D points to construct rectangular surface patches.

最后一步是使用3 d点构造矩形表面.


![Exercise](images/9-2/UVmapping04.png)
>1.	**PolyCurve.ByPoints:** Connect the points on the surface to construct a polycurve through the points.
>1.	**PolyCurve.ByPoints:**通过点连接表面的点构造一个polycurve
2. **Boolean:** Add a Boolean to the workspace and connect it to the *‘connectLastToFirst’* input and toggle to True to close the polycurves. You should now see rectangles mapped to the surface.
2. **Boolean:** 一个布尔值添加到工作区并将其连接到*的connectLastToFirst *输入和关闭polycurves切换为True。您现在应该看到矩形映射到表面。
3. **Surface.ByPatch:** Connect the polycurves to the *‘closedCurve’* input to construct surface patches.
3. **Surface.ByPatch:** 连接polycurves *的closedCurve *输入构建表面.

Now let’s select the nodes that we want to nest into a Custom Node, thinking about what we want to be the inputs and outputs of our node. We want our Custom Node to be as flexible as possible, so it should be able to map any polygons, not just rectangles.

现在让我们选择想要的节点做成一个定制节点,我们想要的输入和输出节点。我们希望定制节点尽可能灵活,所以它应该可以映射任何多边形,不仅仅是矩形。

![Exercise](images/9-2/UVmapping05.png)
> Select the above nodes (beginning with *Polygon.Points*), right click on the workspace and select *‘node from selection’*.
> 选择上面的节点(从* Polygon.Points *),右键单击工作区并选择* *

![Exercise](images/9-2/UVmapping06.png)
> In the Custom Node Properties dialog, assign a name, description, and category to the Custom Node.
>在自定义节点属性对话框中,指定一个名称、描述和分类定制点.

![Exercise](images/9-2/UVmapping07.png)
> The Custom Node has considerably cleaned up the workspace. Notice that the inputs and outputs have been named based on the original nodes. Let’s edit the Custom Node to make the names more descriptive.
> 自定义节点大大清理工作区。注意,输入和输出都被命名为基于原始节点。编辑自定义节点使自己更容易记的名称.

![Exercise](images/9-2/UVmapping08.png)
> Double click the Custom Node to edit it. This will open a workspace with a yellow background representing the inside of the node.
> 双击自定义节点编辑它,这将打开节点的内部.
1. **Inputs:** Change the input names to *baseSurface* and *targetSurface*.
1. **Inputs:** 输入名称更改为* baseSurface *和* targetSurface *.
2. **Outputs:** Add an additional output for the mapped polygons.
2. **Outputs:** 添加一个额外的输出映射的多边形.

>Save the custom node and return to the home workspace.
>保存自定义工作区节点并返回到界面.

![Exercise](images/9-2/UVmapping09.png)
> The **MapPolygonsToSurface** node reflects the changes we just made.

> **MapPolygonsToSurface** 节点反映了我们刚才做出的更改.























