<style>
img{display:block;margin-left: auto;   margin-right: auto }
</style>

##Adding to Your Library
# 增加你的节点库

We've just created a custom node and applied it to a specific process in our Dynamo graph. And we like this node so much, we want to keep it in our Dynamo library to reference in other graphs. To do this, we'll publish the node locally. This is a similar process to publishing a package, which we'll walk through in more detail in the next chapter.

在Dynamo中应用到一个特定的过程，我们喜欢这样的节点，我们想让它们在我们在Dynamo节点库中引用其他的图形，要做到这一点，我们就要将节点发布到本地节点，这样的一个过程就是发布一个节点包，比如,LunchBoxs、unfold、等等.我们讲在下一章更详细的讲解.

###Publishing a Custom Node Locally

### 在本地发布定制节点

Let's move forward with the custom node that we created in the previous section. By publishing a node locally, the node will be accessible in your Dynamo library when you open a new session. Without publishing a node, a Dynamo graph which references a custom node must also have that custom node in its folder (or the custom node must be imported into Dynamo using *File>Import Library*).

上传定制节点，我们在前一章节中创建的，在本地通过发布一个节点，该节点将访问你的Dynamo节点库，出线新的一个节点.没有发布一个节点，Dynamo图引用一个定制节点还必须要定制节点的文件夹（或自定义节点必须导入到Dynamo使用的文件路径）*文件>导入库*

>Download the example file that accompanies this exercise (Right click and "Save Link As..."). A full list of example files can be found in the Appendix.
[PointsToSurface.dyf](datasets/9-3/PointsToSurface.dyf)

>下载示例文件,伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。
[PointsToSurface.dyf](datasets/9-3/PointsToSurface.dyf)

![](images/9-3/AddingToLibrary- 05.png)
> After opening the PointsToSurface custom node, we see the graph above in the Dynamo Custom Node Editor.  You can also open up a custom node by double clicking on it in the Dynamo Graph Editor.

> 打开PointsToSurface定制节点,我们看到上图的Dynamo定制节点编辑器，你也可以通过双击打开一个自定义节点的Dynamo图编辑器.

![](images/9-3/AddingToLibrary- 04.png)
> 1. To Publish a custom node locally, simply right click on the canvas and select *"Publish This Custom Node..."*
> 1. 在本地发布自定义节点,只需右键单击画布并选择* *“发布这个定制节点…”

![](images/9-3/AddingToLibrary- 03.png)
> Fill out the relevant information similar to the image above and select *"Publish Locally".*.  Note that the Group field defines the main element accessible from the Dynamo menu.
> 类似于上图填写相关信息并选择*“发布本地”.*.注意,文字定义了Dynamo的主要元素可以从菜单里边找到相关的节点.

![](images/9-3/AddingToLibrary- 02.png)
> Choose a folder to house all of the custom nodes that you plan on publishing locally. Dynamo will check this folder each time it loads, so make sure the folder is in a permanent place.  Navigate to this folder and choose *"Select Folder".* Your Dynamo node is now published locally, and will remain in your Dynamo Toolbar each time you load the program!
> 选择一个文件夹所有的定制节点,你打算在本地打开。Dynamo将检查这个文件夹加载,所以确保文件夹在一个不会移动的地方,选择“选择文件夹”。*你的Dynamo节点,并一直会在你的工具栏中每次加载程序你指定的文件定制文件.

![](images/9-3/AddingToLibrary- 01.png)
> 1. To check on the custom node folder location, go to *Settings > Manage Node and Package Paths...*
> 1. 检查自定义节点文件夹位置,*设置>管理节点和包路径…*


![](images/9-3/AddingToLibrary- 00.png)
> In this window we see two paths: *AppData\Roaming\Dynamo...* refers to the default location of Dynamo Packages installed online. *Documents\DynamoCustomNodes...* refers to the location of custom nodes we've published locally. *

> 在这个窗口,我们看到两个路径:*AppData\Roaming\Dynamo..*指在线安装发电机包的默认位置。
*文件\ DynamoCustomNodes…*指我们发表在本地定制节点的位置。*
1. You may want to move your local folder path down in the list order above (by selecting the folder path and clicking on the down arrow to the left of the path names).  The top folder is the default path for package installs.  So by keeping the default Dynamo package install path as the default folder, online packages will be separated from your locally published nodes.*
1. 你可能想要移动你的本地文件夹路径在上面的列表顺序(通过选择文件夹路径,单击向下箭头左边的路径名)。文件夹的默认路径是包安装。所以通过保持默认的Dynamo安装路径作为默认文件夹,在线包将被分离。

![](images/9-3/AddingToLibrary- 00A.png)
> We switched the order of the path names in order to have Dynamo's default path as the package install location.
> 我们交换路径名的顺序来作为包的默认路径安装位置。

![](images/9-3/AddingToLibrary- 06.png)
> Navigating to this local folder, we can find the original custom node in the *".dyf"* folder, which is the extension for a Dynamo Custom Node file.  We can edit the file in this folder and the node will update in the UI. We can also add more nodes to the main *DynamoCustomNode* folder and Dynamo will add them to your library at restart!
> 本地文件夹中,我们可以找到原来的定制节点*”。”文件夹,这是Dynamo自定义节点的扩展文件。我们可以编辑文件在这个文件夹和节点,将更新UI。我们也可以添加更多的节点.* DynamoCustomNode *文件夹和Dynamo将在重启后。将它们添加到你的节点库.

![](images/9-3/library.png)
> Dynamo will now load each time with *"PointsToSurface"* in the *"DynamoPrimer"* group of your Dynamo library.

> Dynamo将每次加载* PointsToSurface“* *”DynamoPrimer *到你的节点库.









