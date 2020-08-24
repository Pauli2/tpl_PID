# tpl_PID
Particle identification in liquid scintillation detectors
# 粒子物理大作业



提示：如果你无法渲染其中的公式，请阅读 `README.pdf`，两者内容相同。

## 大作业介绍

中微子是组成自然界的基本粒子之一，质量几乎为 0 ，以接近光速运动，每一秒钟就有数万亿中微子穿过每个人的身体。中微子只参与弱相互作用，与物质的相互作用十分微弱，很难探测，因此被称为幽灵粒子(Ghost Particle)。现在的探测方法，是借助中微子与物质偶然相互作用产生带电粒子，在探测器上沉积能量发出光子，进而通过光电倍增管(Photomultiplier，简称 PMT)接收光信号，产生电压波形。

在探测中微子信号的同时，探测器也会探测到一些典型带电粒子，例如alpha粒子和beta粒子等。在众多的粒子信号中，我们需要将不同的探测事例进行分析比对后，分别标记，本次的大作业，即是完成对alpha粒子和beta粒子的鉴别标记。

粒子物理大作业主要分为两个阶段：

第一个阶段为根据物理背景，模拟生成alpha粒子和beta粒子进入液体闪烁体探测器时，光电倍增管最后得到的输出出信号，即探测器系统对于粒子的信号相应。

第二阶段为将现有光电倍增管输出波形信号，对alpha粒子和beta粒子进行鉴别，分析事例信号为两种粒子的概率大小。

本次大作业的第二部分以清华-锦屏中微子实验为物理背景。对中微子实验中的光电倍增管（PMT）波形（HDF5格式存储）进行数据分析，对液体闪烁体探测器中的alpha粒子和beta粒子进行鉴别，得到相应的粒子类型，并将入射粒子的类型作为输出结果进行提交。



## 物理背景

所需要用到的物理背景知识详见：背景知识.pdf



## 数据说明

所有的输入数据存放在data文件夹下，因此请不要随意改动这个文件夹下的内容。

data.txt文件中存储了用于第一步任务中需要用到的探测器参数和粒子的基本信息，具体内容如下：

| Table    | value     | units              |
| -------- | --------- | ------------------ |
| E_alpha  | 10        | MeV                |
| E_beta   | 1         | MeV                |
| Z        | 246       | 相对原子质量       |
| I        | 0.0022    | MeV                |
| c        | 3.0*10^8  | m/s                |
| v_alpha  | 2.19*10^7 | m/s                |
| v_beta   | 2.82*10^8 | m/s                |
| k        | 4300      | /MeV               |
| n_alpha1 | 0.8       | 慢成分比例         |
| n_alpha2 | 0.2       | 快成分比例         |
| t_alpha1 | 25        | ns，慢成分衰减常数 |
| t_alpha2 | 5         | ns，快成分衰减常数 |
| t_beta   | 5         | ns                 |
| d        | 1         | m，探测器直径      |
| n        | 1.5       | 折射率             |
| N        | 1*10^21   | 每立方米，分子数密度|





## 作业要求（功能部分）

### Makefile

本次作业提供了 Makefile，最终助教也将使用 Makefile 进行测试。需要注意，你在编写所有程序文件时，都应该使用 make 给程序传入的参数（来自 `data.csv`；否则，你可能无法通过测试。

在本目录中运行 `make -n` 即可看到实际运行的命令，这或许能帮助你开发。

### 基本要求

第一阶段的作业主要进行的是模拟探测器对alpha粒子和beta粒子的响应。可以大概分为以下三个步骤，完成每一个任务即可拿到相应的分数：

| 任务（程序名） | 分数 |
| -------------- | ---- |
| first.py       | 10   |
| second.py      | 10   |
| third.py       | 10   |



第一步：根据入射粒子的类型和能量，计算带电粒子的电离能量损失（bethe公式描述），以及发射光子的数量。这里我们做一个简化，认为带电粒子在运动过程中只在探测器球心处发生一次能量沉积（沉积长度delta x=1nm），且作为点源发射各向同性的光子。这里需要区分发射光子的快慢成分（完成first.py）。经过该步骤应该得到一个如下的表格形式：

|           | 快成分光子数 | 慢成分光子数 |
| --------- | ------------ | ------------ |
| alpha粒子 |              |              |
| beta粒子  |              | 不考虑       |



第二步：模拟光子到达光电倍增管的过程（完成second.py）。发射光子，这里的发射位置简化为在探测器的球心。同样，简化后我们认为光子的发射是各向同性的。

在光子传输到达光电倍增管的过程，我们认为该过程是需要进行一定的衰减的，衰减的过程简单的认为符合平方反比规律，即光子到达光电倍增管的亮度认为与发射点到PMT间的距离满足平方反比规律。该部分需要输出光子到达PMT的时间和光强。你需要输出一个如下的表格：

|           | 到达时间（ns） | 光强（光子数） |
| --------- | -------------- | -------------- |
| alpha粒子 |                |                |
| beta粒子  |                |                |



第三步：模拟光子经过光电倍增管放大，得到输出的波形（完成thrid.py）。该部分需要输出得到的波形图像。

该阶段的作业需要提交3个编程文件，经过助教测试后得到相应的分数。





## 第二阶段作业

第二阶段的作业主要是粒子鉴别，这一部分的作业主要基于锦屏的实际数据进行。我们的数据存储为HDF5格式，具体的读写操作见文档：如何读取数据.pdf，如何提交结果.pdf

我们提供了每个探测事例光电倍增管的波形，需要同学们根据每一个事例的波形特征，判断该事例的粒子类别。

在这一步，我们不限制使用的方法和编程语言，最后粒子鉴别标记结果提交后，会由我们的算法给出标记的准确率，给出评分排名（在大作业截止前可以多次提交）。



___

---
