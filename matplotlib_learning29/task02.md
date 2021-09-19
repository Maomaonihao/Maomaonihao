## Task02 艺术画笔见乾坤

- **matplotlib的三个层次的API:**

  - 绘图区:  画纸（matplotlib.backend_bases.FigureCanvas）
  - 渲染区：画笔（matplotlib.backend_bases.Renderer）
  - 图标组件：画家，控制画笔在画纸上作图（matplotlib.artist.Artist）

- **Artist分类**：

  - primitives：基本要素，包含在画图时用到的标准图形对象（eg:**曲线Line2D，文字text，矩形Rectangle，图像image**）

  - containers: 容器（装基本要素）（eg:**图形figure、坐标系Axes和坐标轴Axis**）

- **matpltolib标准用法：**
  - 创建一个`Figure`实例
  - 使用`Figure`实例创建一个或者多个`Axes`或`Subplot`实例
  - 使用`Axes`实例的辅助方法来创建`primitive
    - Axes是一种容器，matplotlib API中最重要的类

- **基本元素绘制：**

  - 绘制2DLines: 

    -   绘制直线line：
      - **pyplot方法绘制**
      - **Line2D对象绘制**
    -  **绘制误差折线图**
      - errorbar
  -  patches(二维图形类):
  
    - 基类是matplotlib.artist.Artist
    -  Rectangle-矩形:
      - 最常见的矩形图是**`hist直方图`和`bar条形图`**
    - Polygon-多边形:
      - 基类是matplotlib.patches.Patch
    - Wedge-契形:
      - 基类是matplotlib.patches.Patch
  - collections:
    - collections类是用来绘制一组对象的集合，collections有许多不同的子类:
      - RegularPolyCollection, CircleCollection, Pathcollection, 分别对应不同的集合子类型
      - 比较常用的就是散点图，属于PathCollection子类
  - images:
    - 最常用的imshow可以根据数组绘制成图像
    - 使用imshow画图时首先需要传入一个数组，数组对应的是空间内的像素位置和像素点的值，interpolation参数可以设置不同的差值方法

- **对象容器：**  

  - Figure容器：
    - `matplotlib.figure.Figure`是`Artist`最顶层的`container`-对象容器，它包含了图表中的所有元素。一张图表的背景就是在`Figure.patch`的一个矩形`Rectangle`。
    - 向图表添加`Figure.add_subplot()`或者`Figure.add_axes()`元素时，这些都会被添加到`Figure.axes`列表中。
    - 由于`Figure`维持了`current axes`，因此你不应该手动的从`Figure.axes`列表中添加删除元素
    - 而是要通过`Figure.add_subplot()`、`Figure.add_axes()`来添加元素，通过`Figure.delaxes()`来删除元素。
    - 可以迭代或者访问`Figure.axes`中的`Axes`，然后修改这个`Axes`的属性。
    - Figure有它自己的`text、line、patch、image`，直接通过`add primitive`语句直接添加
    - 注意`Figure`默认的坐标系是以像素为单位，你可能需要转换成figure坐标系
    - **Figure容器的常见属性：**
      `Figure.patch`属性：Figure的背景矩形
      `Figure.axes`属性：一个Axes实例的列表（包括Subplot)
      `Figure.images`属性：一个FigureImages patch列表
      `Figure.lines`属性：一个Line2D实例的列表（很少使用）
      `Figure.legends`属性：一个Figure Legend实例列表（不同于Axes.legends)
      `Figure.texts`属性：一个Figure Text实例列表
  - Axes容器：
    - `matplotlib.axes.Axes`是matplotlib的核心
    - 大量的用于绘图的`Artist`存放在它内部，并且它有许多辅助方法来创建和添加`Artist`给它自己，而且它也有许多赋值方法来访问和修改这些`Artist`。
    - `Axes`包含了一个patch属性，对于笛卡尔坐标系而言，它是一个`Rectangle`；对于极坐标而言，它是一个`Circle`。这个patch属性决定了绘图区域的形状、背景和边框。
    - `Axes`有许多方法用于绘图，如`.plot()、.text()、.hist()、.imshow()`等方法用于创建大多数常见的`primitive`(如`Line2D，Rectangle，Text，Image`等等）
    - Axes还包含两个最重要的Artist container：
      - `ax.xaxis`：XAxis对象的实例，用于处理x轴tick以及label的绘制
        `ax.yaxis`：YAxis对象的实例，用于处理y轴tick以及label的绘制
    - **Axes容器**的常见属性有：
      - `artists`: Artist实例列表 `patch`: Axes所在的矩形实例 `collections`: Collection实例 `images`: Axes图像 `legends`: Legend 实例 
      - `lines`: Line2D 实例 `patches`: Patch 实例 `texts`: Text 实例 `xaxis`: matplotlib.axis.XAxis 实例 `yaxis`: matplotlib.axis.YAxis 实例
  - Axis容器：
    - `matplotlib.axis.Axis`实例处理`tick line`、`grid line`、`tick label`以及`axis label`的绘制，包括坐标轴上的刻度线、刻度`label`、坐标网格、坐标轴标题。
  - Tick容器：
    - `matplotlib.axis.Tick`是从`Figure`到`Axes`到`Axis`到`Tick`中最末端的容器对象。
    - `Tick`包含了`tick`、`grid line`实例以及对应的`label`。
    - 常见的`tick`属性有：
      - Tick.tick1line：Line2D实例
      - Tick.tick2line：Line2D实例
      - Tick.gridline：Line2D实例
      - Tick.label1：Text实例
      - Tick.label2：Text实例

  

  ### 作业:

  #### 一、思考题：

  - primitives 和 container的区别和联系是什么？
    - 区别：
      1. primitives只能控制自身元素的属性，通过设置属性，展示不同图形的效果
      2. container不能控制基本元素，仅能使用添加/删除元素的方法
    - 联系：
      1. container包含primitives，包括Line2D曲线、Text文字、Patches、collections、image图像等
      2. container和primitives都可以设置属性，用于绘制图形
      3. container和primitives的基类都是`matplotlib.artist.Artist`
      4. Axes container可使用多种方法创建primitives基本元素

  - 四个容器的联系和区别是什么？他们分别控制一张图表的哪些要素？

  联系：

  1. 基类都是`matplotlib.artist.Artist`
  2. 包含关系：Figure容器⊇ Axes容器 ⊇ Axis容器⊇ Tick容器
  3. Figure容器和Axes容器都有`patch`、`images`、`lines`、`legends`和`texts`属性

  区别和控制对象：

  1. Figure容器：控制Axes和subplot对象，包括背景、Axes实例列表、Figure Images patch列表、Line2D实例列表、Figure Legend实例列表和Figure Text实例列表
  2. Axes容器：存放用于绘图的Artist对象，控制patch元素，包括绘图区域的形状、背景和边框
  3. Axis容器：处理`tick line`、`grid line`、`tick label`以及`axis label`的绘制，控制坐标轴上的刻度线、刻度`label`、坐标网格、坐标轴标题
  4. Tick容器：控制`tick`、`grid line`实例以及对应的`label`对象




### 参考资料：

[DataWhale开源资料](https://github.com/datawhalechina/fantastic-matplotlib)

[大佬笔记]([Task02 艺术画笔见乾坤 (relph1119.github.io)](https://relph1119.github.io/my-team-learning/#/matplotlib_learning29/task02))

