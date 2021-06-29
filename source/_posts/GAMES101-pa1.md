---
title: 旋转与投影
comment: false
tags:
  - Computer Graphics
  - Math
  - Linear Algebra
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: 1ecca1be
mathjax: true
date: 2021-05-11 19:24:39
type:
banner_img:
index_img:
translate_title:
top:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/E0zNdAgXMAIBu_T.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/m4ndrill/status/1390712946343522305">Twitter@m4ndrill</a>
   </i>
  </font>
</div>



### 引言

GAMES101现代图形学入门是由闫令琪老师教授。本次作业主要是旋转与投影，深入理解投影变换。

<!--more-->

> 大家好，GAMES101课程的作业1现在发布。
>
> 我们在games，smartchair放了两份完全相同的备份，请大家根据网络环境自行选择下载途径。
>
> [games的作业1链接](http://games-cn.org/wp-content/uploads/2020/02/Assignment1.zip)
>
> [smartchair的作业1链接](http://www.smartchair.org/f_/GAMES2020Course-YLQ/75aa1/F2/Hw1.zip)





### 总览

到目前为止，我们已经学习了如何使用矩阵变换来排列二维或三维空间中的对象。所以现在是时候通过实现一些简单的变换矩阵来获得一些实际经验了。在接下来的三次作业中，我们将要求你去模拟一个基于 CPU 的光栅化渲染器的简化版本。

本次作业的任务是填写一个旋转矩阵和一个透视投影矩阵。给定三维下三个点$v0(2.0,0.0,−2.0),v1(0.0,2.0,−2.0),v2(−2.0,0.0,−2.0)$, 你需要将这三个点的坐标变换为屏幕坐标并在屏幕上绘制出对应的线框三角形 (在代码框架中，我们已经提供了 `draw_triangle` 函数，所以你只需要去构建变换矩阵即可)。简而言之， 我们需要进行模型、视图、投影、视口等变换来将三角形显示在屏幕上。在提供的代码框架中，我们留下了模型变换和投影变换的部分给你去完成。

如果你对上述概念有任何不清楚或疑问，请复习课堂笔记或询问助教。

以下是你需要在 `main.cpp` 中修改的函数(请不要修改任何的函数名和其他已经填写好的函数，并保证提交的代码是已经完成且能运行的):

+ `get_model_matrix(float rotation_angle)`: 逐个元素地构建模型变换矩阵并返回该矩阵。在此函数中，你只需要实现三维中绕 z 轴旋转的变换矩阵， 而不用处理平移与缩放
+ `get_projection_matrix(float eye_fov, float aspect_ratio, float zNear, float zFar)`: 使用给定的参数逐个元素地构建透视投影矩阵并返回该矩阵
+ `[Optional] main()`: 自行补充你所需的其他操作

当你在上述函数中正确地构建了模型与投影矩阵，光栅化器会创建一个窗口显示出线框三角形。由于光栅化器是逐帧渲染与绘制的，所以你可以使用 **A** 和 **D** 键去将该三角形绕 z 轴旋转 (此处有一项提高作业，将三角形绕任意过原点的轴旋转)。当你按下 **Esc** 键时，窗口会关闭且程序终止。

另外，你也可以从命令行中运行该程序。你可以使用以下命令来运行和传递旋转角给程序，在这样的运行方式下，是不会生成任何的窗口，输出的结果图像会被存储在给定的文件中 (若未指定文件名，则默认存储在 `output.png` 中)。图像的存储位置在可执行文件旁，所以如果你的可执行文件是在 `build` 文件夹中， 那么图像也会在该文件夹内。

命令行的使用命令如下:

```shell
./Rasterizer //循环运行程序，创建一个窗口显示，且你可以使用A键和D键旋转三角形
./Rasterizer−r20 //运行程序并将三角形旋转20度,然后将结果存在output.png中
./Rasterizer−r20image.png //运行程序并将三角形旋转20度，然后将结果存在image.png中
```



### 代码框架

在本次作业中，因为你并不需要去使用三角形类，所以你需要理解与修改的文件为`:rasterizer.hpp` 和 `main.cpp`。其中 `rasterizer.hpp` 文件作用是生成渲染器界面与绘制。

光栅化器类在该程序系统中起着重要的作用，其成员变量与函数如下：



#### 成员变量

- `Matrix4f model, view, projection`: 三个变换矩阵。

- `vector<Vector3f> frame_buf`: 帧缓冲对象，用于存储需要在屏幕上绘制的

  颜色数据。



#### 成员函数

+ `set_model(constEigen::Matrix4f&m)`: 将内部的模型矩阵作为参数传 递给光栅化器。

+ `set_view(const Eigen::Matrix4f& v)`: 将视图变换矩阵设为内部视图矩 阵。

+ `set_projection(const Eigen::Matrix4f& p)`: 将内部的投影矩阵设为给 定矩阵 p，并传递给光栅化器

+ `set_pixel(Vector2f point, Vector3f color)`: 将屏幕像素点 (x, y) 设 为 (r, g, b) 的颜色，并写入相应的帧缓冲区位置。

在 `main.cpp` 中，我们模拟了图形管线。我们首先定义了光栅化器类的实例，然后设置了其必要的变量。然后我们得到一个带有三个顶点的硬编码三角形 (请不要修改它)。在主函数上，我们定义了三个分别计算模型、视图和投影矩阵的函数，每一个函数都会返回相应的矩阵。接着，这三个函数的返回值会被 `set_model()`, `set_view()` 和 `set_projection()` 三个函数传入光栅化器中。最后，光栅化器在屏幕上显示出变换的结果。

在用模型、视图、投影矩阵对给定几何体进行变换后，我们得到三个顶点的正则化空间坐标 (canonical space coordinate)。正则化空间坐标是由三个取值范围在 [-1,1] 之间的 x, y, z 坐标构成。我们下一步需要做的就是视口变换，将坐标映射到我们的屏幕中 `(window_width * window_height)`，这些在光栅化器中都已完成，所以不需要担心。但是，你需要去理解这步操作是如何运作的，这一点十分重要。



### 编译

如果使用自己的系统，本次程序作业中使用到的库为 Eigen 与 OpenCV，请确保这两个库的配置正确。

如果使用虚拟机并用 CMake 进行编译，请在终端(命令行)下输入以下内容:

```shell
mkdirbuild // 创建build文件夹以保留的工程文件
cdbuild // 进入build文件夹
cmake .. // 通过提供CMakeLists.txt文件的路径作为参数来运行CMake
make−j4 // 通过make编译代码，−j4表示通过4个内核进行并行化编译
./Rasterizer // 运行代码
```



如果没有对虚拟机的核心数进行过设置，可以在 **Virtual Box** 里点击“设置”，在弹出的窗口中选择“系统—处理器”，然后就可以设置虚拟机的核心数了。 具体操作可见下图:

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511202848006.png)







### 评分与提交

#### 评分

每次作业的评分，分为基础与提高两部分，即在作业批改时会给大家反馈两 个成绩。由于作业不是强制要求必须提交，所以在完成全部作业后，我们会统计 所有的基础分数。若基础分数及格则视为通过课程，反之视为不通过。

- [5 分] 正确构建模型矩阵。
- [5 分] 正确构建透视投影矩阵。
- [10 分] 你的代码可以在现有框架下正确运行，并能看到变换后的三角形。
- [10 分] 当按 A 键与 D 键时，三角形能正确旋转。或者正确使用命令行得到旋转结果图像。
- [提高项 5 分] 在 `main.cpp` 中构造一个函数，该函数的作用是得到绕任意过原点的轴的旋转变换矩阵。
   `Eigen::Matrix4f get_rotation(Vector3f axis, float angle)`



#### 提交

当你完成作业后，请清理你的项目，记得在你的文件夹中包含 CMakeLists.txt 和所有的程序文件 (无论是否修改)。同时，请添加一个 README.md 文件写下 是否完成提高题。最后，将上述内容打包，并用“姓名_Homework1.zip”的命名 方式提交到 SmartChair 平台。

平台链接:http://smartchair.org/GAMES2020Course-YLQ



### 实现

#### 代码框架

```c++
#include "Triangle.hpp"
#include "rasterizer.hpp"
#include <eigen3/Eigen/Eigen>
#include <iostream>
#include <opencv2/opencv.hpp>

constexpr double MY_PI = 3.1415926;

Eigen::Matrix4f get_view_matrix(Eigen::Vector3f eye_pos)
{
    Eigen::Matrix4f view = Eigen::Matrix4f::Identity();

    Eigen::Matrix4f translate;
    translate << 1, 0, 0, -eye_pos[0], 0, 1, 0, -eye_pos[1], 0, 0, 1,
        -eye_pos[2], 0, 0, 0, 1;

    view = translate * view;

    return view;
}

Eigen::Matrix4f get_model_matrix(float rotation_angle)
{
    Eigen::Matrix4f model = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the model matrix for rotating the triangle around the Z axis.
    // Then return it.

    return model;
}

Eigen::Matrix4f get_projection_matrix(float eye_fov, float aspect_ratio,
                                      float zNear, float zFar)
{
    // Students will implement this function

    Eigen::Matrix4f projection = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the projection matrix for the given parameters.
    // Then return it.

    return projection;
}

int main(int argc, const char** argv)
{
    float angle = 0;
    bool command_line = false;
    std::string filename = "output.png";

    if (argc >= 3) {
        command_line = true;
        angle = std::stof(argv[2]); // -r by default
        if (argc == 4) {
            filename = std::string(argv[3]);
        }
    }

    rst::rasterizer r(700, 700);

    Eigen::Vector3f eye_pos = {0, 0, 5};

    std::vector<Eigen::Vector3f> pos{{2, 0, -2}, {0, 2, -2}, {-2, 0, -2}};

    std::vector<Eigen::Vector3i> ind{{0, 1, 2}};

    auto pos_id = r.load_positions(pos);
    auto ind_id = r.load_indices(ind);

    int key = 0;
    int frame_count = 0;

    if (command_line) {
        r.clear(rst::Buffers::Color | rst::Buffers::Depth);

        r.set_model(get_model_matrix(angle));
        r.set_view(get_view_matrix(eye_pos));
        r.set_projection(get_projection_matrix(45, 1, 0.1, 50));

        r.draw(pos_id, ind_id, rst::Primitive::Triangle);
        cv::Mat image(700, 700, CV_32FC3, r.frame_buffer().data());
        image.convertTo(image, CV_8UC3, 1.0f);

        cv::imwrite(filename, image);

        return 0;
    }

    while (key != 27) {
        r.clear(rst::Buffers::Color | rst::Buffers::Depth);

        r.set_model(get_model_matrix(angle));
        r.set_view(get_view_matrix(eye_pos));
        r.set_projection(get_projection_matrix(45, 1, 0.1, 50));

        r.draw(pos_id, ind_id, rst::Primitive::Triangle);

        cv::Mat image(700, 700, CV_32FC3, r.frame_buffer().data());
        image.convertTo(image, CV_8UC3, 1.0f);
        cv::imshow("image", image);
        key = cv::waitKey(10);

        std::cout << "frame count: " << frame_count++ << '\n';

        if (key == 'a') {
            angle += 10;
        }
        else if (key == 'd') {
            angle -= 10;
        }
    }

    return 0;
}
```





#### model变换

##### 绕z轴旋转

我们首先实现模型变换函数，`rotation_angle`需转换为弧度制，z轴旋转课上已经给出：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329205934890.png)



```c++
Eigen::Matrix4f get_model_matrix(float rotation_angle)
{
    Eigen::Matrix4f model = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the model matrix for rotating the triangle around the Z axis.
    // Then return it.

    float angle = rotation_angle / 180.0 * MY_PI;

    Eigen::Matrix4f rotation = Eigen::Matrix4f::Identity();
    rotation << std::cos(angle), -std::sin(angle), 0, 0,
                std::sin(angle), std::cos(angle), 0, 0,
                0, 0, 1, 0,
                0, 0, 0, 1;
    
    model = model * rotation;

    return model;
}
```





##### 绕任意轴旋转

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210617200911722.png)



```c++
Eigen::Matrix4f get_model_matrix(Vector3f axis,float rotation_angle)
{
    Eigen::Matrix4f model = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the model matrix for rotating the triangle around the any axis.
    // Then return it.

    float angle = rotation_angle / 180.0 * MY_PI;

    Eigen::Matrix3f tr;
    Eigen::Matrix3f mul;
    Eigen::Matrix3f tmp = Eigen::Matrix3f::Identity();

    mul << 0, -axis[2], axis[1],
           axis[2], 0, -axis[0],
           -axis[0], axis[0], 0;

    tr = std::cos(angle) * tmp + (1 - std::cos(angle)) * axis * axis.adjoint() + std::sin(angle) * mul;

    model << tr(0,0), tr(0,1), tr(0,2),0,
             tr(1,0), tr(1,1), tr(1,2),0,
             tr(2,0), tr(2,1), tr(2,2),0,
             0, 0, 0, 1;

    return model;
}
```







#### view变换

##### Ortho

我们先写出正交投影变换的矩阵，之前理论课讲到先做平移变换移至原点，再缩放变换将范围缩小到$[-1,1]$的范围。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330100705375.png)



据此我们可以很容易写出两个平移缩放矩阵：

$M_{ortho} = M_{trans}M_{scale} = \begin{bmatrix}\frac{2}{r-l} & 0 & 0 & 0 \\\\ 0 & \frac{2}{t-b} & 0 & 0 \\\\ 0 & 0 & \frac{2}{n-f} & 0 \\\\ 0 & 0 & 0 & 1\end{bmatrix}\begin{bmatrix}1 & 0 & 0 & -\frac{r+l}{2} \\\\ 0 & 1 & 0 & -\frac{t+b}{2} \\\\ 0 & 0 & 1 & -\frac{n+f}{2} \\\\ 0 & 0 & 0 & 1\end{bmatrix}$



回到代码，这里的函数给了四个参数，分别是：

+ `eye_fov`：垂直可视角度
+ `aspect_ratio`：宽高比
+ `zNear`、`zFar`：图中的`n`和`z`

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330102812268.png)



```c++
Eigen::Matrix4f get_projection_matrix(float eye_fov, float aspect_ratio,
                                      float zNear, float zFar)
{
    // Students will implement this function

    Eigen::Matrix4f projection = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the projection matrix for the given parameters.
    // Then return it.

    return projection;
}
```



那么我们可以据此求出`t`、`b`、`l`、`r`，进而求出正交投影矩阵：

```c++
      // Matrix ortho

      float angle = eye_fov / 180.0 * MY_PI;

      float top = zNear * std::tan(angle / 2);
      float bot = -top;
      float left = top * aspect_ratio;
      float right = -left;


      Eigen::Matrix4f ortho = Eigen::Matrix4f::Identity();
      Eigen::Matrix4f trans(4,4);
      Eigen::Matrix4f scale(4,4);

      trans << 2 / (right - left), 0, 0, 0,
               0, 2 / (top - bot), 0, 0,
               0, 0, 2 / (zNear -zFar), 0,
               0, 0, 0, 1;

      scale << 1, 0, 0, -(right + left) / 2,
               0, 1, 0, -(top + bot) / 2,
               0, 0, 1, -(zNear + zFar) / 2,
               0, 0, 0, 1;

      ortho = trans * scale;
```







##### Persp to Ortho

求出投影矩阵之后我们来写正交到透视的变换矩阵$M_{persp2ortho}$，理论课我们把未知的参数`A`、`B`都求了出来，可以看到只需要`zNear`和`zFar`，最终矩阵可以写成：

$M_{persp2ortho}=\begin{bmatrix}n & 0 & 0 & 0 \\\\ 0 & n & 0 & 0 \\\\ 0 & 0 & A & B \\\\ 0 & 0 & 1 & 0\end{bmatrix}$ 其中$A=n+f$、$B=-nf$

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210617143035536.png)

最后只需$M_{persp} = M_{ortho}M_{persp2ortho}$即可：

```c++
    // Matrix persp2ortho

    float A = zNear + zFar;
    float B = -zNear * zFar;

    Eigen::Matrix4f persp2ortho = Eigen::Matrix4f::Identity();

    persp2ortho << zNear, 0, 0, 0,
                   0, zNear, 0, 0,
                   0, 0, A, B,
                   0, 0, 1, 0;


    // Matrix presp
    projection = ortho * persp2ortho;
```





最终整个视口函数如下：

```c++
Eigen::Matrix4f get_projection_matrix(float eye_fov, float aspect_ratio,
                                      float zNear, float zFar)
{
    // Students will implement this function

    Eigen::Matrix4f projection = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the projection matrix for the given parameters.
    // Then return it.

    // Matrix ortho

    float angle = eye_fov / 180.0 * MY_PI;

    float top = zNear * std::tan(angle / 2);
    float bot = -top;
    float left = top * aspect_ratio;
    float right = -left;


    Eigen::Matrix4f ortho = Eigen::Matrix4f::Identity();
    Eigen::Matrix4f trans(4,4);
    Eigen::Matrix4f scale(4,4);

    trans << 2 / (right - left), 0, 0, 0,
             0, 2 / (top - bot), 0, 0,
             0, 0, 2 / (zNear -zFar), 0,
             0, 0, 0, 1;

    scale << 1, 0, 0, -(right + left) / 2,
             0, 1, 0, -(top + bot) / 2,
             0, 0, 1, -(zNear + zFar) / 2,
             0, 0, 0, 1;

    ortho = trans * scale;

    // Matrix persp2ortho

    float A = zNear + zFar;
    float B = -zNear * zFar;

    Eigen::Matrix4f persp2ortho = Eigen::Matrix4f::Identity();

    persp2ortho << zNear, 0, 0, 0,
                   0, zNear, 0, 0,
                   0, 0, A, B,
                   0, 0, 1, 0;


    // Matrix presp
    projection = ortho * persp2ortho;

    return projection;
}
```





### 参考文章

+ [GAMES101 作业1 基础版 答案](https://www.cnblogs.com/eat-too-much/p/12465518.html)
+ [GAMES101-作业1详解](https://zhuanlan.zhihu.com/p/361156478)

