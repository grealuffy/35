
# 图形学作业2
学号 102101335 姓名 周仲龙

本次作业运行平台是在虚拟机中实现，对main.cpp中的函数进行修改来达到预期效果

## 首先运行函数框架看是否有无问题
* 以下是运行结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/bbba69e772084cfcb1f5432ca55f9ee1.png)
* 由上图可知原函数框架并无问题，随机选取四个点后可绘制相应红色曲线
***
所要补充完整的第一个函数是void bezier(const std::vector<cv::Point2f> &control_points, cv::Mat &window)，该函数实现绘制 Bézier 曲线的功能。它使用一个控制点序列和一个OpenCV::Mat 对象作为输入，没有返回值。它会使 t 在 0 到 1 的范围内进行迭代，并在每次迭代中使 t 增加一个微小值。对于每个需要计算的t，将调用另一个函数 recursive_bezier，然后该函数将返回在 Bézier 曲线上t 处的点。最后，将返回的点绘制在 OpenCV::Mat 对象上。具体函数内容如下：
## 1.递归迭代实现绘制 Bézier 曲线函数bezier

该函数返回一个bool变量，若判断在三角形内就返回true即真，若不在三角形内就返回false即假，反映在图形上即在三角形ABC中，若坐标点P在绕三角形同一方向（如同为顺时针或逆时针）的三个向量AB,BC,CA的同一侧（左侧或右侧），即确定坐标点P在三角形ABC内部，对应的坐标公式如图中函数上半部分所示
![在这里插入图片描述](https://img-blog.csdnimg.cn/026123894b6442298e2c22f076152baf.png)



## 2.De Casteljau 算法返回曲线对应点坐标recursive_bezier
第二个函数cv::Point2f recursive_bezier(const std::vector<cv::Point2f> &control_points, float t)是使用一个控制点序列和一个浮点数 t 作为输入，实现 de Casteljau 算法来返回 Bézier 曲线上对应点的坐标。如下图函数所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/4a911321793040df942a90425db7528b.png)

## 3.最终在虚拟机上bezier函数单独运行结果
* 注释掉main 函数中while 循环内调用 naive_bezier 函数的行，并取消对 bezier 函数的注释。要求你的实现将Bézier 曲线绘制为绿色
![在这里插入图片描述](https://img-blog.csdnimg.cn/80e37eba394c40eab3f17e89241c141b.png)
* 运行结果如下图

![在这里插入图片描述](https://img-blog.csdnimg.cn/040b9da47be8498e97e7813e9b4a1a2d.png)
* 此时曲线颜色为绿色
### 若与native_bezier函数同时运行结果如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/e9d63de1fbac4d74baa7d4670a5e5783.png)
* 此时曲线颜色变为黄色，说明计算结果一致，算法无误

### 不同控制点的绘制结果
* 六个控制点
![在这里插入图片描述](https://img-blog.csdnimg.cn/b35261497f354c5e9231cb9f6a32a808.png)
* 八个控制点

![在这里插入图片描述](https://img-blog.csdnimg.cn/78f81460747f4c73944e087f2f16db07.png)
## 反走样实现
本次作业还要求实现对 Bézier 曲线的反走样。 ( 对于一个曲线上的点，不只把它对应于一个像
素，你需要根据到像素中心的距离来考虑与它相邻的像素的颜色。 )
* 算法实现如bezier函数的下半部分：
![在这里插入图片描述](https://img-blog.csdnimg.cn/026123894b6442298e2c22f076152baf.png)
### 反走样前
* 可以看到线的锯齿情况很严重
![在这里插入图片描述](https://img-blog.csdnimg.cn/1e1eec5e9b7b49c192d009ca4f67ee20.png)
### 反走样后（仅稍微少些锯齿，不完美）
![在这里插入图片描述](https://img-blog.csdnimg.cn/2adfb783ce1c410baaa314610f62c67d.png)

