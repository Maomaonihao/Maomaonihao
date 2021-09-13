## Task01：Matplotlib初相识（2天）

- **Python 可视化包总结：**

  - Matplotlib(比较低级的库)
  - Seaborn、Pandas建立在Matplotlib之上（Seaborn 或 Pandas 中的 df.plot() 时，用的其实是别人用 Matplotlib 写的代码）
  - ggplot
  - Bokeh
  - plotly(非常强大，但用它设置和创建图形都要花费大量时间，而且都不直观)
  - pygal
  - pyecharts

  

- **Matplotlib功能：**

  - 可绘制静态、同态、交互的图表
  - 可用于Python脚本，Python和IPython Shell、Jupyter notebook，Web应用程序服务器和各种图形用户界面工具包等



- **matplotlib图像组成：**四个层级（容器）

  - Figure: 顶级层，可容纳所有绘图元素
  - Axes: 用来构造子图（一个figure可有一个或多个子图组成）

  - Axis: Axes下属层级（处理和坐标轴，网格有关的元素）
  - Tick: Axis的下属层级（处理和刻度有关的元素）

  

- **两种绘图接口：**

  - 显示创建figure和axes(OO（object-oriented style）模式)

    ```python
    # 案例
    x =  linspace(0, 2, 100)
    
    fig, ax = plt.subplots()
    ax.plot(x, x, label='linear')
    ax.plot(x, x**2, label='quadratic')
    ax.plot(x, x**3, label='cubic')
    ax.set_xlabel('x label')
    ax.set_ylabel('y label')
    ax.set_title('Simple Plot')
    ax.legend()
    plot.show()
    ```

  - 依赖pyplot自动创建figure和axes，并绘图

    ```python
    x = np.linspace(0, 2, 100)
    
    plt.plot(x, x, label='linear')
    plt.plot(x, x**2, label='quadratic')
    plt.plot(x, x**3, label='cubic')
    plt.xlabel('x label')
    plt.ylabel('y label')
    plt.title('Simple Plot')
    plt.lengend()
    plt.show()
    ```



- **Trick:**
  - jupyter notebook使用matplotlib出现的问题；
    - 默认打印最后一个对象（eg:<matplotlib.lines.Line2D at 0x23155916dc0>）
  - 解决方法：
    - 在代码最后加一个分号（;）
    - 在最后加plt.show()
    - 绘图时，将对象显示赋给一个变量（eg :plt.plot([1, 2, 3, 4]) 改成line =plt.plot([1, 2, 3, 4])）



- 参考资料

  [DataWhale开源资料](https://github.com/datawhalechina/fantastic-matplotlib)

s
