
# 一.uv贴图


在3D计算机图形学中，UV映射是一种将2D纹理映射到3D模型表面的方法。在这里，“U”和“V”代表了2D纹理空间的坐标，这与2D笛卡尔坐标系统中的“X”和“Y”是类似的。在3D模型的每个顶点上，都会有一组对应的UV坐标，它们定义了3D模型在这个顶点上的表面应当对应纹理图像的哪个部分。


UV坐标通常被储存在模型的顶点属性中，并与其他属性（如顶点位置、法线向量等）一起被传递到渲染管线中。在渲染过程中，像素着色器会使用这些UV坐标来从纹理中采样颜色，然后用这些颜色来着色模型的表面。


UV坐标的取值范围通常是\[0, 1]，其中(0,0\)对应纹理的左下角，(1,1\)对应纹理的右上角。然而，也可以使用超出这个范围的值，这通常会导致纹理的重复或镜像，具体的效果取决于纹理的环绕模式（wrap mode）。


UV映射的主要挑战之一是如何有效地将2D纹理映射到复杂的3D形状上，以避免拉伸、压缩或其他形式的失真。这通常需要专门的UV展开或UV拆分工具，以及一些手动的调整工作。


总的来说，UV属性在3D场景中是非常重要的，它们定义了如何将纹理映射到3D模型的表面，从而极大地影响了模型的最终视觉效果。


## 解释


uv可以理解为一个坐标系，主要作用于给物体进行贴图的


为什么这一个贴图贴上去，就刚刚好图片在物体正中间不偏不倚


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357025.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357025.png)


这个鸭子使用很多个平面三角形组成，那么为什么用了这么一张图片他知道眼睛这里用黑色，嘴巴那里用稍微黑一点的


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357994.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357994.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357008.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357008.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357063.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357063.png)


举例


创建一个平面几何体，给上贴图


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357067.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357067.png)


但是这个几何体使用创建顶点的方式实现的


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357077.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357077.png)


再创建一个几何体，不创建uv，直接给贴图


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357533.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357533.png)


左边就是有uv的，右边没有uv不知道怎么贴图就是白色


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357744.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357744.png)


之前用顶点，三个点是一个点的位置


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357874.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357874.png)


这里创建uv坐标，并且设置属性的时候声明两个点是一个坐标的位置


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357889.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281357889.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358089.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358089.png)


还可以把第四个点拉到下面来


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358376.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358376.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358927.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358927.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358056.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358056.png)


眼睛顶点


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358183.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358183.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358208.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358208.png)


# 二.法向量


## 1\.解释


法向量就是投射于物体的一条直线，可以形成反射效果


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358541.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358541.png)


如果是快速创建的一个物体他会自动有法向量，但是通过顶点创建就没有，所以在环境贴图里面就不能反射


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358186.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358186.png)


开启法向量


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358235.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358235.png)


同时环境贴图要设置每一个可以作用的材质


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358286.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358286.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358757.gif)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358757.gif)


**除了自动计算法向量也可以自己设置顶点**


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358224.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358224.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358307.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358307.png)


辅助线开启


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358634.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358634.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358856.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358856.png)


在3D计算机图形学中，"法向量"（或简称为"法线"）是一个向量，表示3D模型表面在某一点的方向。在每个顶点上，都会有一个关联的法向量，这个向量通常被归一化，也就是说它的长度为1。


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358242.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358242.png)


顶点的法向属性在很多计算图形的领域都有应用，但最常见的用途是在光照计算中。当光源照亮一个3D模型的时候，每个表面的亮度取决于光线与表面的相对角度。这个角度可以通过比较光线方向和表面法向量来计算。这样，即使表面的几何形状非常复杂，也可以通过使用每个顶点的法向量来进行准确的光照计算。


法向量通常在模型的创建过程中被计算出来，然后存储在每个顶点的属性中。对于有些表面，如平面或者球体，法向量可以通过简单的数学公式来计算。但对于更复杂的几何形状，可能需要通过比如"法线映射"（normal mapping）等更复杂的技术来生成。


除了用于光照计算外，法向量也可以用于一些其他的图形效果，如环境光遮蔽（ambient occlusion）、凹凸映射（bump mapping）、反射和折射等。总的来说，法向属性在3D场景中是非常重要的，它们对于渲染真实感的图像有着关键的作用。


## 2\.顶点转换


也就是之前用的position、rotate、scale等不仅可以直接用方法，还可以用顶点的方式


初始顶点的位置


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358393.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358393.png)


想让他移动x轴为4


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358497.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358497.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358895.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358895.png)


## 3\.包围盒


什么是包围盒，比如这一个鸭子，有一个立方体框柱就是他的包围盒


好处在于如果想去计算鸭子的大小，那么会去计算很多个顶点很麻烦，但是如果他有一个包围盒计算包围盒的大小也就上下左右几个顶点就可以了


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358176.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358176.png)


实现


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358569.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358569.png)


直接加载模型


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358722.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358722.png)


可以查看这个物体的名字和id


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358059.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358059.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358704.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358704.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358745.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358745.png)


在导入模型的回调里面


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358180.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358180.png):[豆荚加速器官网](https://baitenghuo.com)


但是此时的包围盒会很大，因为他的缩放给的值很大


### 3\.1 世界矩阵


这个时候就要用到世界矩阵，让他的变换和本地的一样比例


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358662.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358662.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358740.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358740.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358905.gif)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358905.gif)


## 4\.几何体居中和获取几何体中心


有了包围盒，可以快速让一个模型居中


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358480.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358480.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358986.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358986.png)


## 5\.获取多个物体包围盒


加入有多个物体，想让他们在一起形成一个大的包围盒去操作


得益于包围盒有这么一个方法


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358281.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358281.png)


三个小球


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358712.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358712.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358934.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358934.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358038.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358038.png)


也可以快速直接计算


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358290.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358290.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358416.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358416.png)


## 6\.边缘几何体和线框几何体


边缘几何体就是边缘是经过计算得到，不再是每个平面都是用三角形组成，而线段几何体就是之前的wireframe，将所有面用三角线组成


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358138.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358138.png)


拿到物体的几何体，创建边缘几何体，要用到线段材质


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358259.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358259.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358612.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358612.png)


此时方向不一致，那是因为这是直接拿到物体的顶点来创建的，得到的最原始的位置旋转等，如果想要跟这个模型一模一样，那么需要复制到这个物体的矩阵


开启建筑物的矩阵，然后让边缘几何体赋值建筑物的矩阵，并且需要更新，decompose就是结构当前的信息分别给到边缘几何体的位置、旋转和缩放


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358154.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358154.png)


完全重合


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358436.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358436.png)


线段几何体


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358666.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358666.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358685.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358685.png)


如果一个模型过大，里面很多物体都想变为边缘几何体，就可以通过遍历，traverse专门获取里面的3D物体


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358899.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358899.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358083.png)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358083.png)


[![](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358761.gif)](https://heymar.oss-cn-chengdu.aliyuncs.com/undefined202411281358761.gif)


  * [一.uv贴图](#%E4%B8%80uv%E8%B4%B4%E5%9B%BE)
* [解释](#%E8%A7%A3%E9%87%8A)
* [二.法向量](#%E4%BA%8C%E6%B3%95%E5%90%91%E9%87%8F)
* [1\.解释](#tid-W72Hn7)
* [2\.顶点转换](#tid-T8dncD)
* [3\.包围盒](#tid-rN7exe)
* [3\.1 世界矩阵](#tid-hsDZ5d)
* [4\.几何体居中和获取几何体中心](#tid-wc4DcT)
* [5\.获取多个物体包围盒](#tid-bEYAff)
* [6\.边缘几何体和线框几何体](#tid-dEsmtM)

   \_\_EOF\_\_

   ![](https://github.com/heymar)Heymar  - **本文链接：** [https://github.com/heymar/p/18574171](https://github.com)
 - **关于博主：** 评论和私信会在第一时间回复。或者[直接私信](https://github.com)我。
 - **版权声明：** 本博客所有文章除特别声明外，均采用 [BY\-NC\-SA](https://github.com "BY-NC-SA") 许可协议。转载请注明出处！
 - **声援博主：** 如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。
     
