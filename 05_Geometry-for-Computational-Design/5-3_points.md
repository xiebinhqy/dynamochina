##Dynamo 中的点

点是所有创建几何的基础，我们至需要两个点来创建一个曲线，需要三个点来创建多边形或网状的异形.他的位置、定义、顺序和点之间的关系能够定义出更高的异形曲面或曲体.

![Point to Curve](images/5-3/PointsAsBuildingBlocks-1.png)
> 1. 圆使用的功能 ```x=r*cos(t)``` and ```y=r*sin(t)```
> 2. 正弦曲线使用功能 ```x=(t)``` and ```y=r*sin(t)```

### 点的定义

一个点被定义为一个或多个值时，被称为坐标，需要定义多少坐标值点取决于他所在坐标的数值，最常见的点在Dynamo中三维世界坐标系统和有三个坐标值（x,y,z）.

![Point](images/5-3/Point.png)

### 点的坐标

点可以存在于一二维坐标系统，不同的字母符号取决于不同的空间，我们正在使用在同一表面上不同统一坐标系（x,y）或（u,v）之间的关系.

![Point as Coordinates](images/5-3/Coordinates.png)
> 1. 一个点在几何坐标系统: [X,Y,Z]
> 2. 一个点在一条曲线参数坐标系统: [t]
> 3. 一个点在一个表面参数坐标系统: [U,V]


参数曲线和表面都是连续和不规则的几何形状，自定义形状参数空间停留在一个三维世界坐标系统，我们可以将参数坐标转化为一个“世界”坐标，表面上的点[0.2,0.5]转化为世界坐标的点[1.8,2.0,4.1].

![Points in Dynamo](images/5-3/Dynamo-Points.png)
> 1. 在假定世界坐标中的X,Y,Z
> 2. 点相对于给定的坐标系(圆柱)
> 3. 点作为UV坐标在一个表面上


>下载示例文件,伴随这幅图像(右点击“链接另存为…”):[Geometry for Computational Design - Points.dyn](datasets/5-3/Geometry for Computational Design - Points.dyn).示例文件的完整列表可以在附录中找到.







