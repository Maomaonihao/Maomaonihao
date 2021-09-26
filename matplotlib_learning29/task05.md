# 第五回：样式色彩秀芳华

- 绘图样式：
  - 修改预定义样式
  - 自定义样式
  - rcparams
  - matplotlibrc文件

#### 一、matplotlib的绘图样式（style）

- 1.预定义样式：

    ```python
    axes.titlesize : 24
    axes.labelsize : 20
    lines.linewidth : 3
    lines.markersize : 10
    xtick.labelsize : 16
    ytick.labelsize : 16
    ```

    ```python
    plt.style.use('file/presentation.mplstyle')
    plt.plot([1,2,3,4],[2,3,4,5]);
    ```

    

    ```python
    plt.style.use('default')
    plt.style.use('ggplot')
    
    # 查看所有样式
    print(plt.style.available)
    
    >>>['Solarize_Light2', '_classic_test_patch', 'bmh', 'classic', 'dark_background', 'fast', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn', 'seaborn-bright', 'seaborn-colorblind', 'seaborn-dark', 'seaborn-dark-palette', 'seaborn-darkgrid', 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks', 'seaborn-white', 'seaborn-whitegrid', 'tableau-colorblind10']
    ```

- 用户自定义stylesheet：

    - 在任意路径下创建一个后缀名为mplstyle的样式清单，编辑文件添加以下样式内容:

      ```python
      axes.titlesize : 24
      axes.labelsize : 20
      lines.linewidth : 3
      lines.markersize : 10
      xtick.labelsize : 16
      ytick.labelsize : 16
      ```

      ```python
      plt.style.use('file/presentation.mplstyle')
      plt.plot([1,2,3,4],[2,3,4,5]);
      ```
      
  - matplotlib支持混合样式的引用，只需在引用时输入一个样式列表，若是几个样式中涉及到同一个参数，右边的样式表会覆盖左边的值。
  
    ```python
    plt.style.use(['dark_background', 'file/presentation.mplstyle'])
    plt.plot([1,2,3,4],[2,3,4,5]);
    ```
  
- 设置rcparams:

    - 还可以通过修改默认rc设置的方式改变样式，所有rc设置都保存在一个叫做 matplotlib.rcParams的变量中。

      ```python
      mpl.rcParams['lines.linewidth'] = 2
      mpl.rcParams['lines.linestyle'] = '--'
      plt.plot([1,2,3,4],[2,3,4,5]);
      ```
    
- 修改matplotlibrc文件:

    - 由于matplotlib是使用matplotlibrc文件来控制样式的，也就是上一节提到的rc setting，所以我们还可以通过修改matplotlibrc文件的方式改变样式。

      ```python
      # 查找matplotlibrc文件的路径
      mpl.matplotlib_fname()
      ```

      

#### 二、matplotlib的色彩设置（color）：

- 三个视觉通道：
  - 色相：没有明显的顺序性、一般不用来表达数据量的高低，而是用来表达数据列的类别。
  - 亮度：在视觉上很容易区分出优先级的高低、被用作表达顺序或者表达数据量视觉通道。
  - 饱和度：在视觉上很容易区分出优先级的高低、被用作表达顺序或者表达数据量视觉通道。

**1.设置颜色的几种方式：**

- RGB或RGBA:

  ```python
  plt.style.use('default')
  
  # 颜色用[0,1]之间的浮点数表示，四个分量按顺序分别为(red, green, blue, alpha)，其中alpha透明度可省略
  plt.plot([1,2,3],[4,5,6],color=(0.1, 0.2, 0.5))
  plt.plot([4,5,6],[1,2,3],color=(0.1, 0.2, 0.5, 0.5));
  ```

- HEX RGB 或 RGBA:

  ```python
  # 用十六进制颜色码表示，同样最后两位表示透明度，可省略
  plt.plot([1,2,3],[4,5,6],color='#0f0f0f')
  plt.plot([4,5,6],[1,2,3],color='#0f0f0f80');
  ```

- 灰度色阶：

      ```python
      # 当只有一个位于[0,1]的值时，表示灰度色阶
      plt.plot([1,2,3],[4,5,6],color='0.5');
      ```

- 单字符基本颜色：

  ```python
  # matplotlib有八个基本颜色，可以用单字符串来表示，分别是'b', 'g', 'r', 'c', 'm', 'y', 'k', 'w'，对应的是blue, green, red, cyan, magenta, yellow, black, and white的英文缩写
  plt.plot([1,2,3],[4,5,6],color='m');
  ```

- 颜色名称：

  ```python
  # matplotlib提供了颜色对照表，可供查询颜色对应的名称
  plt.plot([1,2,3],[4,5,6],color='tan');
  ```

- 使用colormap设置一组颜色：

  - 有些图表支持使用colormap的方式配置一组颜色，从而在可视化中通过色彩的变化表达更多信息。

  - 在matplotlib中，colormap共有五种类型:

    - 顺序（Sequential）。通常使用单一色调，逐渐改变亮度和颜色渐渐增加，用于表示有顺序的信息

    - 发散（Diverging）。改变两种不同颜色的亮度和饱和度，这些颜色在中间以不饱和的颜色相遇;当绘制的信息具有关键中间值（例如地形）或数据偏离零时，应使用此值。

    - 循环（Cyclic）。改变两种不同颜色的亮度，在中间和开始/结束时以不饱和的颜色相遇。用于在端点处环绕的值，例如相角，风向或一天中的时间。

    - 定性（Qualitative）。常是杂色，用来表示没有排序或关系的信息。

    - 杂色（Miscellaneous）。一些在特定场景使用的杂色组合，如彩虹，海洋，地形等。

      ```python
      x = np.random.randn(50)
      y = np.random.randn(50)
      plt.scatter(x,y,c=x,cmap='RdPu');
      ```

      

### 参考资料：
[DataWhale开源资料](https://github.com/datawhalechina/fantastic-matplotlib)