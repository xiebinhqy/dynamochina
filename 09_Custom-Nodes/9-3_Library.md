<style>
img{display:block;margin-left: auto;   margin-right: auto }
</style>

# 增加你的节点库

在Dynamo中应用到一个特定的过程，我们喜欢这样的节点，我们想让它们在我们在Dynamo节点库中引用其他的图形，要做到这一点，我们就要将节点发布到本地节点，这样的一个过程就是发布一个节点包，比如,LunchBoxs、unfold、等等.我们讲在下一章更详细的讲解.

### 在本地发布定制节点

上传定制节点，我们在前一章节中创建的，在本地通过发布一个节点，该节点将访问你的Dynamo节点库，出线新的一个节点.没有发布一个节点，Dynamo图引用一个定制节点还必须要定制节点的文件夹（或自定义节点必须导入到Dynamo使用的文件路径）*文件>导入库*

>下载示例文件,伴随这个练习(右点击“链接另存为…”)。示例文件的完整列表可以在附录中找到。
[PointsToSurface.dyf](datasets/9-3/PointsToSurface.dyf)

![](images/9-3/AddingToLibrary- 05.png)
> 打开PointsToSurface定制节点,我们看到上图的Dynamo定制节点编辑器，你也可以通过双击打开一个自定义节点的Dynamo图编辑器.

![](images/9-3/AddingToLibrary- 04.png)
> 1. 在本地发布自定义节点,只需右键单击画布并选择* *“发布这个定制节点…”

![](images/9-3/AddingToLibrary- 03.png)
> 类似于上图填写相关信息并选择*“发布本地”.*.注意,文字定义了Dynamo的主要元素可以从菜单里边找到相关的节点.

![](images/9-3/AddingToLibrary- 02.png)
> 选择一个文件夹所有的定制节点,你打算在本地打开。Dynamo将检查这个文件夹加载,所以确保文件夹在一个不会移动的地方,选择“选择文件夹”。*你的Dynamo节点,并一直会在你的工具栏中每次加载程序你指定的文件定制文件.

![](images/9-3/AddingToLibrary- 01.png)
> 1. 检查自定义节点文件夹位置,*设置>管理节点和包路径…*


![](images/9-3/AddingToLibrary- 00.png)
> 在这个窗口,我们看到两个路径:*AppData\Roaming\Dynamo..*指在线安装发电机包的默认位置。
*文件\ DynamoCustomNodes…*指我们发表在本地定制节点的位置。*


1. 你可能想要移动你的本地文件夹路径在上面的列表顺序(通过选择文件夹路径,单击向下箭头左边的路径名)。文件夹的默认路径是包安装。所以通过保持默认的Dynamo安装路径作为默认文件夹,在线包将被分离。

![](images/9-3/AddingToLibrary- 00A.png)
> 我们交换路径名的顺序来作为包的默认路径安装位置。

![](images/9-3/AddingToLibrary- 06.png)
> 本地文件夹中,我们可以找到原来的定制节点*”。”文件夹,这是Dynamo自定义节点的扩展文件。我们可以编辑文件在这个文件夹和节点,将更新UI。我们也可以添加更多的节点.* DynamoCustomNode *文件夹和Dynamo将在重启后。将它们添加到你的节点库.

![](images/9-3/library.png)
> Dynamo将每次加载* PointsToSurface“* *”DynamoPrimer *到你的节点库.









