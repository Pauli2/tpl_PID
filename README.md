# tpl_PID
Particle identification in liquid scintillation detectors
# 粒子物理大作业



## 作业背景

粒子物理大作业是基于中微子排位赛2020（Ghost-Hunter2020）结合而来的一个作业。主要分为两个阶段：

第一个阶段为根据物理背景，模拟生成alpha粒子和beta粒子进入液体闪烁体探测器时，光电倍增管最后得到的输出出信号，即探测器系统对于粒子的信号相应。

第二阶段为将现有光电倍增管输出波形信号，对alpha粒子和beta粒子进行鉴别，分析事例信号为两种粒子的概率大小。

本次大作业的第二部分以清华-锦屏中微子实验为物理背景。对中微子实验中的光电倍增管（PMT）波形（HDF5格式存储）进行数据分析，对液体闪烁体探测器中的alpha粒子和beta粒子进行鉴别，得到相应的粒子类型，并将入射粒子的类型作为输出结果进行提交。

本次作业将对提交的粒子类型结果的准确率进行评估判定，给出最后的得分。



## 物理背景

所需要用到的物理背景知识详见：背景知识.pdf

##### 

## 第一阶段作业

第一阶段的作业主要进行的是模拟探测器对alpha粒子和beta粒子的响应。可以大概分为以下三个步骤：

第一步：根据入射粒子的类型和能量，得到发射光子的数量。这一步需要输出最终发射的光子数量。

第二步：模拟光子到达光电倍增管的过程。这个过程我们对整个过程进行一些必要的简化，我们将入射的粒子作为点源发射，简单的认为粒子在轨迹的末端直接停止，发射光子，这里的发射位置简化为在探测器的球心。同样，简化后我们认为光子的发射是各向同性的。

在光子传输到达光电倍增管的过程，我们认为该过程是需要进行一定的衰减的，衰减的过程简单的认为符合指数衰减规律，即光子到达光电倍增管的亮度认为与发射点到PMT间的距离满足指数规律。该部分需要输出光子到达PMT的时间和光强。

第三步：模拟光子经过光电倍增管放大，得到输出的波形。该部分需要输出得到的波形图像。

该阶段的作业需要提交3个编程文件，经过助教测试后得到相应的分数。

给定的初始参量如下：

液体闪烁体探测器直径：1m

alpha粒子动能：10MeV

beta粒子动能：1MeV

探测器液闪平均电离能：0.2MeV/mm



## 第二阶段作业

第二阶段的作业主要是粒子鉴别，这一部分的作业主要基于锦屏的实际数据进行。我们的数据存储为HDF5格式，具体的读写操作见文档：如何读取数据.pdf，如何提交结果.pdf

我们提供了每个探测事例光电倍增管的波形，需要同学们根据每一个事例的波形特征，判断该事例的粒子类别。

在这一步，我们不限制使用的方法和编程语言，最后粒子鉴别标记结果提交后，会由我们的算法给出标记的准确率，给出评分排名（在大作业截止前可以多次提交）。

