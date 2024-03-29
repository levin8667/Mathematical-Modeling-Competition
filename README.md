2019年中国研究生数学建模竞赛D题

## **汽车行驶工况构建**

**一、问题背景**

**汽车行驶工况**（Driving Cycle）又称车辆测试循环，是描述汽车行驶的速度-时间曲线（如图1、2，一般总时间在1800秒以内，但没有限制标准，图1总时间为1180秒，图2总时间为1800秒），体现汽车道路行驶的运动学特征，是汽车行业的一项重要的、共性基础技术，是车辆能耗/排放测试方法和限值标准的基础，也是汽车各项性能指标标定优化时的主要基准。目前，欧、美、日等汽车发达国家，均采用适应于各自的汽车行驶工况标准进行车辆性能标定优化和能耗/排放认证。

本世纪初，我国直接采用欧洲的NEDC行驶工况（如图1）对汽车产品能耗/排放的认证，有效促进了汽车节能减排和技术的发展。近年来，随着汽车保有量的快速增长，我国道路交通状况发生很大变化，政府、企业和民众日渐发现以NEDC工况为基准所优化标定的汽车，实际油耗与法规认证结果偏差越来越大，影响了政府的公信力（譬如对某型号汽车，该车标注的工信部油耗6.5升/100公里，用户体验实际油耗可能是8.5-10升/100公里）。另外，欧洲在多年的实践中也发现NEDC工况的诸多不足，转而采用世界轻型车测试循环（WLTC，如图2）。但该工况怠速时间比和平均速度这两个最主要的工况特征，与我国实际汽车行驶工况的差异更大。作为车辆开发、评价的最为基础的依据，开展深入研究，制定反映我国实际道路行驶状况的测试工况，显得越来越重要。

另一方面，我国地域辽广，各个城市的发展程度、气候条件及交通状况的不同，使得各个城市的汽车行驶工况特征存在明显的不同。因此，基于城市自身的汽车行驶数据进行城市汽车行驶工况的构建研究也越来越迫切，希望所构建的汽车行驶工况与该市汽车的行驶情况尽量吻合，理想情况下是完全代表该市汽车的行驶情况（也可以理解为对实际行驶情况的浓缩），目前北京、上海、合肥等都已经构建了各城市的汽车行驶工况。

为了更好地理解构建汽车行驶工况曲线的重要性，以某型号汽车油耗为例，简单说明标注的工信部油耗是如何测试出来？标注的工信部油耗并不是该型号汽车在实际道路上的实测油耗，而是基于国家标准（如《GB27840-2011重型商用车辆燃料消耗量测量方法》），在实验室里根据汽车行驶工况曲线，按照一定的标准，经检测、计算得出。由此可见，标注的工信部油耗是否与实际油耗相吻合，与汽车行驶工况曲线有密切关系。

![图1.png](https://i.loli.net/2020/02/06/shTkBKv5RHbe8Wc.png)

  <center>图1 欧洲NEDC工况</center> 

![图2.png](https://i.loli.net/2020/02/06/cB6AdJDO9gYZ3VI.png)

  <center>图2 世界WLTC工况</center> 

**二、目标的提出**

在上述背景下，请根据附件（3个数据文件，每个数据文件为同一辆车在不同时间段内所采集的数据）所提供的某城市轻型汽车实际道路行驶采集的数据（采样频率1Hz），构建一条能体现参与数据采集汽车行驶特征的**汽车行驶工况**曲线（1200-1300秒），该曲线所体现的汽车运动特征（如平均速度、平均加速度等）能代表所采集数据源的相应特征，两者间的误差越小，说明所构建的汽车行驶工况的代表性越好。

 

**三、解决的问题**

**1.数据预处理**

由汽车行驶数据的采集设备直接记录的原始采集数据往往会包含一些不良数据值，不良数据主要包括几个类型：

(1) 由于高层建筑覆盖或过隧道等，GPS信号丢失，造成所提供数据中的时间不连续；

(2) 汽车加、减速度异常的数据（普通轿车一般情况下：0至100km/h的加速时间大于7秒，紧急刹车最大减速度在7.5~8 m/s2）；

(3) 长期停车（如停车不熄火等候人、停车熄火了但采集设备仍在运行等）所采集的异常数据。

(4) 长时间堵车、断断续续低速行驶情况（最高车速小于10km/h）,通常可按怠速情况处理。

(5) 一般认为怠速时间超过180秒为异常情况，怠速最长时间可按180秒处理。

请设计合理的方法将上述不良数据进行预处理，并给出各文件数据经处理后的记录数。



**2.运动学片段的提取**

运动学片段是指汽车从怠速状态开始至下一个怠速状态开始之间的车速区间，如图3所示（基于运动学片段构建汽车行驶工况曲线是日前最常用的方法之一，但并不是必须的步骤，有些构建汽车行驶工况曲线的方法并不需要进行运动学片段划分和提取）。请设计合理的方法，将上述经处理后的数据划分为多个运动学片段，并给出各数据文件最终得到的运动学片段数量。

![%E5%9B%BE3.png](https://cl.ly/097aa855aa62/download/%E5%9B%BE3.png)

 <center>图3 运动学片段的定义</center> 

**3.汽车行驶工况的构建**

请根据上述经处理后的数据，构建一条能体现参与数据采集汽车行驶特征的汽车行驶工况曲线（1200-1300秒），该曲线的汽车运动特征能代表所采集数据源（经处理后的数据）的相应特征，两者间的误差越小，说明所构建的汽车行驶工况的代表性越好。要求：

（1）科学、有效的构建方法（数学模型或算法，特别鼓励创新方法，如果采用已有的方法，必须注明来源）；

（2）合理的汽车运动特征评估体系（至少包含但不限于以下指标：平均速度（km/h）、平均行驶速度（km/h）、平均加速度（m/  ）、平均减速度（m/  ）、怠速时间比（%）、加速时间比（%）、减速时间比（%）、速度标准差（km/h）、加速度标准差（m/  ）等）；

（3）按照你们所构建的汽车行驶工况及汽车运动特征评估体系，分别计算出汽车行驶工况与该城市所采集数据源（经处理后的数据）的各指标（运动特征）值，并说明你们所构建的汽车行驶工况的合理性。



**四、名词解释与参考文献**

**1.** **部分名词解释**

**怠速：**汽车停止运动，但发动机保持最低转速运转的连续过程。

**加速：**汽车加速度大于0.1m/s2的连续过程。

**减速：**汽车加速度小于-0.1m/s2的连续过程。

**巡航/匀速：**汽车加速度的绝对值小于0.1m/s2非怠速的连续过程。

**平均速度：**一段时间周期内，汽车速度的算术平均值。

**平均行驶速度：**汽车在行驶状态下汽车速度的算术平均值，即不包含汽车怠速状态。

**怠速时间比：**一段时间周期内，怠速状态的累计时间长度占该时间周期总时间长度的百分比。

**平均加速度：**汽车在加速状态下各单位时间（秒）加速度的算术平均值。

**平均减速度：**汽车在减速状态下各单位时间（秒）减速度的算术平均值。

**加速时间比：**一段时间周期内，处在加速状态的累计时间长度占该时间周期总时间长度的百分比。

**减速时间比：**一段时间周期内，处在减速状态的累计时间长度占该时间周期总时间长度的百分比。

**速度标准差：**一段时间周期内，汽车速度的标准差，即包括怠速状态。

**加速度标准差：**一段时间周期内，处在加速状态的汽车加速度的标准差。

 

**2.** **参考文献**

【1】   Lin J, Niemeier D A. Exploratory analysis comparing a stochastic driving cycle to California's regulatory cycle[J]. Atmospheric Environment, 2002, 36(38):5759-5770. 

【2】   Karande, S., Olson, M., and Saha, B. Development of Representative Vehicle Drive Cycles for Hybrid Applications[J]. SAE Technical Paper 2014-01-1900, 2014, doi:10.4271/2014-01-1900.

【3】   姜平，石琴，陈无畏，黄志鹏. 基于小波分析的城市道路行驶工况构建的研究[J]. 汽车工程, 2011(1):70-73.

【4】   Knez M, Muneer T, Jereb B, et al. The estimation of a driving cycle for Celje and a comparison to other European cities[J]. Sustainable Cities and Society, 2014, 11:56-60.

【5】   Ho, Sze-Hwee, Wong, Yiik-Diew, Chang, Victor Wei-Chung. Developing Singapore Driving Cycle for passenger cars to estimate fuel consumption and vehicular emissions [J]. Atmospheric Environment,2014,97:353-362. 