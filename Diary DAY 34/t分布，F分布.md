t分布，F分布，卡方分布都是基于正态分布衍生出来的

u检验（总体均值，总体方差已知的情况下使用）

例子：(U检验)

一台机器生成某种金属球，直径服从正态分布N(10，0.04)。抽取100个样本后，发现样本的均值为9.8cm，请问该机器生产的产品直径的均值是否为10cm。在0.05的显著性水平下

1、H0：![u_{0}=10cm](https://private.codecogs.com/gif.latex?u_%7B0%7D%3D10cm)   H1:![u_{0}\neq 10cm](https://private.codecogs.com/gif.latex?u_%7B0%7D%5Cneq%2010cm)

2、取![\alpha=0.05](https://private.codecogs.com/gif.latex?%5Calpha%3D0.05)

3、样本量为100，所以这里选择u检验（为什么会选择u检验，而不选择t？）

在总体方差已经知道的情况下，不管样本数量多少都可以选择u检验。而如果总体方差未知，且样本数量小于40，则应该选择t检验。那么如果总体方差未知，但是样本数量超过40了，则u检验和t检验都可以使用，因为样本量大的情况下，t分布趋向于正态分布

+++

假设检验的步骤

       1 提出假设，包括无效假设H0和备择假设H1。
    
       2 预设检验水准，一般设为0.05，概率小于0.05为小概率事件
    
       3 选定检验方法，检验方法的选定要依据抽样的样本数量等因素进行确定
    
       4 依据检验方法，确定在H0假设下的发生概率，如果小于0.05，则证明，H0假设为小概率事件，就可以拒绝H0

+++

4、计算

![u=\frac{9.8-10}{0.2/\sqrt{100}}=-10](https://private.codecogs.com/gif.latex?u%3D%5Cfrac%7B9.8-10%7D%7B0.2/%5Csqrt%7B100%7D%7D%3D-10)

可以发现这里是双边检验，所以查![u_{0.025}](https://private.codecogs.com/gif.latex?u_%7B0.025%7D)=1.96。所以拒绝H0

**双边检验**：在假设检验中，利用检验统计量的密度曲线和x轴边界区域两侧的尾部面积来构造临界区域。

在选择的显著性水平A下，将A确定的放弃区域平分为两部分，放置在正态曲线的两侧（如图所示），即每边占**A／2**的面积。需要进行双边检验。

[![img](https://iknow-pic.cdn.bcebos.com/8ad4b31c8701a18b761134328e2f07082938fed1?x-bce-process%3Dimage%2Fresize%2Cm_lfit%2Cw_600%2Ch_800%2Climit_1%2Fquality%2Cq_85%2Fformat%2Cf_jpg)](https://iknow-pic.cdn.bcebos.com/8ad4b31c8701a18b761134328e2f07082938fed1)

+++

t检验（总体均值已经知道，但总体方差未知，只知道样本的方差）

  （一）、单总体t检验

 一台机器生成某种金属球，直径服从正态分布。抽取16个样本后，发现样本的均值为9.8cm，方差为0.04，请问该机器生产的产品直径的均值是否为10cm。在0.05的显著性水平下

1、H0：![u_{0}=10cm](https://private.codecogs.com/gif.latex?u_%7B0%7D%3D10cm)   H1:![u_{0}\neq 10cm](https://private.codecogs.com/gif.latex?u_%7B0%7D%5Cneq%2010cm)

2、取![\alpha=0.05](https://private.codecogs.com/gif.latex?%5Calpha%3D0.05)

3、总体方差未知，样本量为16，所以这里选择t检验（如果样本数量较大，比如超过40，亦可以选择u检验）

4、计算![t=\frac{9.8-10}{0.2/\sqrt{16}}=-4](https://private.codecogs.com/gif.latex?t%3D%5Cfrac%7B9.8-10%7D%7B0.2/%5Csqrt%7B16%7D%7D%3D-4)



查![t_{0.025}(15)=2.49](https://private.codecogs.com/gif.latex?t_%7B0.025%7D%2815%29%3D2.49)，所以拒绝H0

 （二）、两总体t检验（这两个总体的方差齐，且服从正态分布）

两台机器A,B生产某种金属球，从A生产的产品中取16件，发现其均值为9.8cm，方差为0.04，从B生产的产品中取9件，发现其均值为9.7cm，方差为0.015，是否可以认定A,B产品的直径有显著性差异，在0.05的显著性水平下。

1、H0：![\mu _{A} =\mu_{B}](https://private.codecogs.com/gif.latex?%5Cmu%20_%7BA%7D%20%3D%5Cmu_%7BB%7D)   H1:![\mu _{A} \neq \mu_{B}](https://private.codecogs.com/gif.latex?%5Cmu%20_%7BA%7D%20%5Cneq%20%5Cmu_%7BB%7D)

2、取![\alpha=0.05](https://private.codecogs.com/gif.latex?%5Calpha%3D0.05)

3、判断两个总体的均值是否有显著性差异，要用t检验

4、计算![t=\frac{9.8-9.7}{\sqrt{\frac{0.04}{16}+\frac{0.015}{9}}}=1.5506](https://private.codecogs.com/gif.latex?t%3D%5Cfrac%7B9.8-9.7%7D%7B%5Csqrt%7B%5Cfrac%7B0.04%7D%7B16%7D&plus;%5Cfrac%7B0.015%7D%7B9%7D%7D%7D%3D1.5506)

![t_{0.025}(16+9-2)=2.3978](https://private.codecogs.com/gif.latex?t_%7B0.025%7D%2816&plus;9-2%29%3D2.3978)

，所以接受H0。

+++



![image-20220120133632918](C:\Users\73887\AppData\Roaming\Typora\typora-user-images\image-20220120133632918.png)