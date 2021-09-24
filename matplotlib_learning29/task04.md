## 第四回：文字图例尽眉目

#### 一、Figure和Axes上的文本

- matplotlib广泛的文本支持：
  - 数学表达式
  - 栅格
  - 矢量输出的TrueType
  - 具有任意旋转的换行分割文本
  - Unicode

- pyplot API和objected-oriented API分别创建文本的方式：

  | pyplot API | OO API     | description                |
  | ---------- | ---------- | -------------------------- |
  | text       | text       | 在Axes的任意位置添加text   |
  | title      | set_title  | 在Axes添加title            |
  | figtext    | text       | 在Figure的任意位置添加text |
  | suptitle   | suptitle   | 在Figure添加title          |
  | xlabel     | set_xlabel | 在Axes的x-axis添加label    |
  | ylabel     | set_ylabel | 在Axes的y-axis添加label    |

- 字体的属性设置：

  - 全局字体设置：

    - 查看matplotlib所有可用的字体：

      ```python
      from matplotlib import font_manager
      font_family = font_manager.fontManager.ttflist
      font_name_list = [i.name for i in font_family]
      for font in font_name_list[:10]:
          print(f'{font}\n')
      ```

      ```python
      #该block讲述如何在matplotlib里面，修改字体默认属性，完成全局字体的更改。
      import matplotlib.pyplot as plt
      plt.rcParams['font.sans-serif'] = ['SimSun']    # 指定默认字体为新宋体。
      plt.rcParams['axes.unicode_minus'] = False      # 解决保存图像时 负号'-' 显示为方块和报错的问题。
      ```

  - 自定义局部字体设置：

    ```python
    #局部字体的修改方法1
    import matplotlib.pyplot as plt
    import matplotlib.font_manager as fontmg
    
    x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    plt.plot(x, label='小示例图标签')
    
    # 直接用字体的名字。
    plt.xlabel('x 轴名称参数', fontproperties='Microsoft YaHei', fontsize=16)         # 设置x轴名称，采用微软雅黑字体
    plt.ylabel('y 轴名称参数', fontproperties='Microsoft YaHei', fontsize=14)         # 设置Y轴名称
    plt.title('坐标系的标题',  fontproperties='Microsoft YaHei', fontsize=20)         # 设置坐标系标题的字体
    plt.legend(loc='lower right', prop={"family": 'Microsoft YaHei'}, fontsize=10);    # 小示例图的字体设置
    ```

    ```python
    #局部字体的修改方法2
    import matplotlib.pyplot as plt
    import matplotlib.font_manager as fontmg
    
    x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    plt.plot(x, label='小示例图标签')
    #fname为你系统中的字体库路径
    my_font1 = fontmg.FontProperties(fname=r'C:\Windows\Fonts\simhei.ttf')      # 读取系统中的 黑体 字体。
    my_font2 = fontmg.FontProperties(fname=r'C:\Windows\Fonts\simkai.ttf')      # 读取系统中的 楷体 字体。
    # fontproperties 设置中文显示，fontsize 设置字体大小
    plt.xlabel('x 轴名称参数', fontproperties=my_font1, fontsize=16)       # 设置x轴名称
    plt.ylabel('y 轴名称参数', fontproperties=my_font1, fontsize=14)       # 设置Y轴名称
    plt.title('坐标系的标题',  fontproperties=my_font2, fontsize=20)       # 标题的字体设置
    plt.legend(loc='lower right', prop=my_font1, fontsize=10);              # 小示例图的字体设置
    ```

  - 数学表达式：（MathText）

    ```python
    import numpy as np
    import matplotlib.pyplot as plt
    t = np.arange(0.0, 2.0, 0.01)
    s = np.sin(2*np.pi*t)
    
    plt.plot(t, s)
    plt.title(r'$\alpha_i > \beta_i$', fontsize=20)
    plt.text(1, -0.6, r'$\sum_{i=0}^\infty x_i$', fontsize=20)
    plt.text(0.6, 0.6, r'$\mathcal{A}\mathrm{sin}(2 \omega t)$',
             fontsize=20)
    plt.xlabel('time (s)')
    plt.ylabel('volts (mV)')
    plt.show()
    ```

    

#### 二、Tick上的文本：

- 设置tick（刻度）和ticklabel（刻度标签）也是可视化中经常需要操作的步骤
- matplotlib既提供了自动生成刻度和刻度标签的模式（默认状态），同时也提供了许多让使用者灵活设置的方式。

**1.简单模式：**

- 可以使用axis的`set_ticks`方法手动设置标签位置，使用axis的`set_ticklabels`方法手动设置标签格式

```python
import matplotlib.pyplot as plt
import numpy as np
import matplotlib
x1 = np.linspace(0.0, 5.0, 100)
y1 = np.cos(2 * np.pi * x1) * np.exp(-x1)
```

```python
# 使用axis的set_ticks方法手动设置标签位置的例子，该案例中由于tick设置过大，所以会影响绘图美观，不建议用此方式进行设置tick
fig, axs = plt.subplots(2, 1, figsize=(5, 3), tight_layout=True)
axs[0].plot(x1, y1)
axs[1].plot(x1, y1)
axs[1].xaxis.set_ticks(np.arange(0., 10.1, 2.))
plt.show()
```

```python
# 使用axis的set_ticklabels方法手动设置标签格式的例子
fig, axs = plt.subplots(2, 1, figsize=(5, 3), tight_layout=True)
axs[0].plot(x1, y1)
axs[1].plot(x1, y1)
ticks = np.arange(0., 8.1, 2.)
tickla = [f'{tick:1.2f}' for tick in ticks]
axs[1].xaxis.set_ticks(ticks)
axs[1].xaxis.set_ticklabels(tickla)
plt.show()
```

```python
#一般绘图时会自动创建刻度，而如果通过上面的例子使用set_ticks创建刻度可能会导致tick的范围与所绘制图形的范围不一致的问题。
#所以在下面的案例中，axs[1]中set_xtick的设置要与数据范围所对应，然后再通过set_xticklabels设置刻度所对应的标签
import numpy as np
import matplotlib.pyplot as plt
fig, axs = plt.subplots(2, 1, figsize=(6, 4), tight_layout=True)
x1 = np.linspace(0.0, 6.0, 100)
y1 = np.cos(2 * np.pi * x1) * np.exp(-x1)
axs[0].plot(x1, y1)
axs[0].set_xticks([0,1,2,3,4,5,6])

axs[1].plot(x1, y1)
axs[1].set_xticks([0,1,2,3,4,5,6])#要将x轴的刻度放在数据范围中的哪些位置
axs[1].set_xticklabels(['zero','one', 'two', 'three', 'four', 'five','six'],#设置刻度对应的标签
                   rotation=30, fontsize='small')#rotation选项设定x刻度标签倾斜30度。
axs[1].xaxis.set_ticks_position('bottom')#set_ticks_position()方法是用来设置刻度所在的位置，常用的参数有bottom、top、both、none
print(axs[1].xaxis.get_ticklines())
plt.show()
```



#### 三、legend(图例)

- 图例有一个或多个legend entries（图例条目）组成

- 一个entry由一个key和一个label组成

- **legend key（图例键）：** 每个 legend label左面的colored/patterned marker（彩色/图案标记）

- **legend label（图例标签）：** 描述由key来表示的handle的文本

- **legend handle（图例句柄）：** 用于在图例中生成适当图例条目的原始对象

- 常用的几个参数：

  - (1)设置图列位置： plt.legend(loc='upper center') 等同于plt.legend(loc=9)

    | loc by number | loc by text    |
    | ------------- | -------------- |
    | 0             | 'best'         |
    | 1             | 'upper right'  |
    | 2             | 'upper left'   |
    | 3             | 'lower left'   |
    | 4             | 'lower right'  |
    | 5             | 'right'        |
    | 6             | 'center left'  |
    | 7             | 'center right' |
    | 8             | 'lower center' |
    | 9             | 'upper center' |
    | 10            | 'center'       |

  - (2)设置图例字体大小:  fontsize : int or float or {‘xx-small’, ‘x-small’, ‘small’, ‘medium’, ‘large’, ‘x-large’, ‘xx-large’}

  - (3)设置图例边框及背景:

     ```python
     plt.legend(loc='best',frameon=False) #去掉图例边框
     plt.legend(loc='best',edgecolor='blue') #设置图例边框颜色
     plt.legend(loc='best',facecolor='blue') #设置图例背景颜色,若无边框,参数
     ```

  - (4)设置图例标题:

    ```python
    legend = plt.legend(["CH", "US"], title='China VS Us')
    ```

  - (5)设置图例名字及对应关系:
  
    ```python
    legend = plt.legend([p1, p2], ["CH", "US"])
  
    

### 参考资料：
[DataWhale开源资料](https://github.com/datawhalechina/fantastic-matplotlib)

