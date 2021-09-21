# Task03 布局格式定方圆

- **导包：**

  ```python
  import numpy as np
  import pandas as pd
  import matplotlib.pyplot as plt
  plt.rcParams['font.sans-serif'] = ['SimHei']  # 用来正常显示中文标签
  plt.rcParams['axes.unicode_minus'] = False  # 用来正常显示负号
  ```

- **子图：**

  - plt.subplots绘制均匀状态下的子图

    - 返回元素分别为画布（fig）和子图（axs）构成的列表

    - figsize:指定整个画布的大小

    - sharex/sharey: 是否共享横轴和纵轴刻度

    - tight_layout: 调整子图的相对大小，使子图不会重叠

      ```python
      fig, axs = plt.subplots(2, 5, figsize=(10, 4), sharex=True, sharey=True)
      fig.suptitle('样例1', size=20)
      for i in range(2):
          for j in range(5):
              axs[i][j].scatter(np.random.randn(10), np.random.randn(10))
              axs[i][j].set_title('第%d行，第%d列'%(i+1,j+1))
              axs[i][j].set_xlim(-5,5)
              axs[i][j].set_ylim(-5,5)
              if i==1: axs[i][j].set_xlabel('横坐标')
              if j==0: axs[i][j].set_ylabel('纵坐标')
      fig.tight_layout()
      ```

      ```python
      # 极坐标
      N = 150
      r = 2 * np.random.rand(N)
      theta = 2 * np.pi * np.random.rand(N)
      area = 200 * r**2
      colors = theta
      
      
      plt.subplot(projection='polar')
      plt.scatter(theta, r, c=colors, s=area, cmap='hsv', alpha=0.75);
      ```

  - 使用GridSpec绘制非均匀子图：

    - 第一种非均匀： 图的比例大小不同但没有跨行或跨列

    - 第二种非均匀： 图为跨行或跨列状态

    - add_gridspec: 指定width_ratios(相对宽度比例)、 height_ratios(相对高度比例)

      ```python
      # spec[i, j]
      fig = plt.figure(figsize=(10, 4))
      spec = fig.add_gridspec(nrows=2, ncols=5, width_ratios=[1,2,3,4,5], height_ratios=[1,3])
      fig.suptitle('样例2', size=20)
      for i in range(2):
          for j in range(5):
              ax = fig.add_subplot(spec[i, j])
              ax.scatter(np.random.randn(10), np.random.randn(10))
              ax.set_title('第%d行，第%d列'%(i+1,j+1))
              if i==1: ax.set_xlabel('横坐标')
              if j==0: ax.set_ylabel('纵坐标')
      fig.tight_layout()
      ```

      ```python
      # 通过切片实现子图的合并，大道跨图的功能
      fig = plt.figure(figsize=(10, 4))
      spec = fig.add_gridspec(nrows=2, ncols=6, width_ratios=[2,2.5,3,1,1.5,2], height_ratios=[1,2])
      fig.suptitle('样例3', size=20)
      # sub1
      ax = fig.add_subplot(spec[0, :3])
      ax.scatter(np.random.randn(10), np.random.randn(10))
      # sub2
      ax = fig.add_subplot(spec[0, 3:5])
      ax.scatter(np.random.randn(10), np.random.randn(10))
      # sub3
      ax = fig.add_subplot(spec[:, 5])
      ax.scatter(np.random.randn(10), np.random.randn(10))
      # sub4
      ax = fig.add_subplot(spec[1, 0])
      ax.scatter(np.random.randn(10), np.random.randn(10))
      # sub5
      ax = fig.add_subplot(spec[1, 1:5])
      ax.scatter(np.random.randn(10), np.random.randn(10))
      fig.tight_layout()
      ```

- **子图上的方法：**

  - 在 `ax` 对象上定义了和 `plt` 类似的图形绘制函数，常用的有： `plot, hist, scatter, bar, barh, pie`

  - 常用直线的画法为： `axhline, axvline, axline` （水平、垂直、任意方向）

    - axline好像被弃用？

  - 使用 `set_xscale, set_title, set_xlabel` 分别可以设置坐标轴的规度（指对数坐标等）、标题、轴名

  - 与一般的 `plt` 方法类似， `legend, annotate, arrow, text` 对象也可以进行相应的绘制

    - legend中的loc参数如下：

    | string       | code |
    | :----------- | :--: |
    | best         |  0   |
    | upper right  |  1   |
    | upper left   |  2   |
    | lower left   |  3   |
    | lower right  |  4   |
    | right        |  5   |
    | cneter left  |  6   |
    | center right |  7   |
    | lower center |  8   |
    | upper center |  9   |
    | center       |  10  |

      

### 参考资料：
[DataWhale开源资料](https://github.com/datawhalechina/fantastic-matplotlib)
