# Ground-Penetrating-Radar-Image-Processing
一个探地雷达图像处理项目，已实现B-Scan图像病害提取、病害类型甄别、二层钢筋识别、病害厘米级定位等功能，待实现的功能有声呐图像处理、利用深度学习实现病害分类等。
<br>
## 对空洞与脱空病害的识别、定位、分类
* 概述<br>
 本应用由三种基本的算法支持，即病害提取算法、相位特征提取算法和形状特征提取算法，具体算法总流程如图4所示。其中病害提取算法是另外两种算法的基础，病害提取算法通过提取病害图像在行方差上的分布特征，找出我们感兴趣的有病害区域。进而，相位特征提取算法在直方图均衡、图像二值化等基础上，进行列求导，并提取病害区域的相位特征，根据不同相位特征我们可以对病害进行初步分类，即将含水层与空洞和脱区分开。最后，形状特征提取算法运用F-K偏移算法、图形分割、形状模式识别等操作，在形态学特征上，区分空洞与脱空。<br><br>
      ![算法总流程图](https://github.com/Paul95278/Ground-Penetrating-Radar-Image-Processing/raw/master/img/病害识别算法总流程图.png)
* 病害提取算法
 * 实现功能<br>
本算法以当前高速公路地下混凝土结构病害的GPR信号为研究对象，设计给出一种自动定位GPR信号病害位置的算法；根据GPR信号公路路基图像有无病害的行方差分布的区别，结合阈值法区分出图像有无病害，并提取病害位置，节省了大量时间和人力。此外，行方差和阈值法不受外界固定干扰和混凝土层结构的影响，准确度高。符合当代高速公路地下混凝土结构GPR信号病害自动定位的迫切要求，有很大的经济和现实意义。<br>
 * 结果展示<br>
 ![筛选病害结果展示](https://github.com/Paul95278/Ground-Penetrating-Radar-Image-Processing/raw/master/img/筛选病害结果展示.jpg)
 * 相位特征提取算法
  * 实现步骤<br>
步骤1：根据3.1.1病害提取算法得到的有病害图像行段，对GPR图像像素进行归一化，得到矩阵NI；<br>
步骤2：对矩阵NI进行直方图均衡处理，得到矩阵NI_H；<br>
步骤3：对矩阵NI_H进行三值化，三值化阈值根据类正态分布法设定，得到矩阵NI_HB；<br>
步骤4：对矩阵NI_HB的每列进行求导，然后对求导后的每列分别进行处理，使每列中相位相邻元素之间为异号，最终得到两种相位类型；<br>
步骤5：选取数量较多的相位类型作为GPR图像病害类型。<br>
 * 实现功能<br>
 以当前高速公路地下混凝土结构病害的GPR信号为研究对象，设计给出一种突出GPR信号病害算法；采用了结合归一化、直方图均衡、阈值选取、三值化算法，突出病害位置和特征，有利于进一步提取病害特征。实现了高速公路地下常见病害：脱空、空气、含水层的特征突出，具有一定现实意义，符合探地雷达行业病害识别自动化的追求目标，具有很大的现实意义。
 * 效果展示<br>
 ![原图、直方图均衡、三值化效果对比](https://github.com/Paul95278/Ground-Penetrating-Radar-Image-Processing/raw/master/img/原图、直方图均衡、三值化效果对比.jpg)
 ![相位特征算法处理结果](https://github.com/Paul95278/Ground-Penetrating-Radar-Image-Processing/raw/master/img/相位特征算法处理结果.jpg)
* 形状特征提取算法
 * 实现步骤<br>
 略
 * 实现功能<br>
 略
 * 效果展示<br>
 略
 ## 二层钢筋定位识别
 ![钢筋正对25cm10cm](https://github.com/Paul95278/Ground-Penetrating-Radar-Image-Processing/raw/master/img/钢筋正对25cm10cm.jpg)
 
 ![900M-钢保较小侧](https://github.com/Paul95278/Ground-Penetrating-Radar-Image-Processing/raw/master/img/900M-钢保较小侧.jpg)
 
 ## 项目相关论文
 * [Extracting and Identifying Concrete Structural Defects in GPR Images](http://spie.org/Publications/Proceedings/Paper/10.1117/12.2296452)
 * [Study of GPR Signal Propagation and Imaging of Multilayer Rebar
Mesh Structure](http://spie.org/Publications/Proceedings/Paper/10.1117/12.2296457)
 ## 项目分工
 * `叶奇玲（NUPT）`完成对空洞与脱空病害相关算法的开发
 * `田家乐（NUPT）`完成对钢筋相关算法的开发<br>
   * ``上述大部分研发工作由叶奇玲、田家乐完成``
 * `刘  普（NUPT）`利用Qt+openCV实现并优化上述算法，并封装成可初步使用的软件
