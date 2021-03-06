## 1.2 生理模型

计算神经科学所希望建模的是真实生物的神经系统，因此，要了解神经元模型，可以先从和生理实际联系最紧密的模型入手。下面，本节将介绍受生理实验启发的最经典的模型：Hodgkin-Huxley模型。

### 1.2.1 Hodgkin-Huxley模型

Hodgkin和Huxley（1952）在枪乌贼的巨轴突上用膜片钳技术记录了动作电位的产生，并提出了经典的神经元模型**Hodgkin-Huxley模型**（**HH模型**）。

上一节我们已经介绍了神经元膜的一般结构，为了建模这样的结构，HH模型中将生物上的细胞膜转化为等效电路，如图1-4所示。

<center><img src="../../figs/neus/1-2.png">	</center>

<center><b>图1-4 神经元细胞膜的等效电路图（<cite>Gerstner et al., 2014 <sup><a href="#fn_1">1</a></sup></cite>） </b></center>

上图是将图1-1中真实神经元膜转换为电子元件所得到的等效电路图，图中电容$$C$$表示低电导的疏水性磷脂双层膜，电流$$I$$表示外界输入。

右侧三个并联的电阻中，Na+和K+通道被单独建模为两个可变电阻$$R_{Na}$$和$$R_K$$（这是由于Na+和K+在动作电位的形成中特别重要），电阻$$R$$则代表膜上除了Na+通道和K+通道之外所有未指明的离子通道，有时也表示为下标$$_L$$或者$$_{leak}$$。电源 $$E_{Na}$$, $$E_K$$ 和$$E_L$$对应着由相应离子在膜两侧的浓度差所引起的电位差。

考虑基尔霍夫第一定律，即对于电路中的任一点，流入该点的总电流和流出该点的总电流相等，图1-4可被建模为如下所示的微分方程：
$$
C \frac{dV}{dt} = -(\bar{g}_{Na} m^3 h (V - E_{Na}) + \bar{g}_K n^4(V - E_K) + g_{leak}(V - E_{leak})) + I(t)
$$

$$
\frac{dx}{dt} = \alpha_x(1-x) - \beta_x , x \in \{ Na, K, leak \}
$$

这就是著名的Hodgkin-Huxley模型。注意在如上的$$\frac{dV}{dt}$$方程中，右侧的前三项分别代表穿过钠离子通道，钾离子通道和其他非特定离子通道的电流，同时$$I(t)$$表示外部输入。在方程左侧，$$C\frac{dV}{dt} = \frac{dQ}{dt} = I$$是穿过电容的电流。

在计算通过离子通道的电流时，除了欧姆定律$$I = U/R = gU$$之外，HH模型还引入了三个**门控变量**m、n和h来表示离子通道的打开/关闭状态。准确地说，变量m和h控制着钠离子通道的状态，变量n控制着钾离子通道的状态。一个离子通道的真实电导是其最大电导$$\bar{g}$$和通道门控变量状态的乘积，比如通过Na+通道的电流$$I=U/R_{Na} = g_{Na}*U_{Na} = \bar{g} * m^3 h * (V-E_{Na})$$。

门控变量的动力学可以被表示为一种类马尔可夫的形式，其中$$\alpha_x$$代表门控变量$$x$$的激活速率，而$$\beta_x$$代表$$x$$的失活速率。下述$$\alpha_x$$和$$\beta_x$$的公式由实验数据拟合得到。
$$
\alpha_m(V) = \frac{0.1(V+40)}{1 - exp(\frac{-(V+40)}{10})}
$$

$$
\beta_m(V) = 4.0 exp(\frac{-(V+65)}{18})
$$

$$
\alpha_h(V) = 0.07 exp(\frac{-(V+65)}{20})
$$

$$
\beta_h(V) = \frac{1}{1 + exp(\frac{-(V + 35)}{10})}
$$

$$
\alpha_n(V) = \frac{0.01(V+55)}{1 - exp(\frac{-(V+55)}{10})}
$$

$$
\beta_n(V) = 0.125 exp(\frac{-(V+65)}{80})
$$

<center><img src="../../figs/neus/codes/zh/HH1.png">	</center>

<center><img src="../../figs/neus/codes/zh/HH2.png">	</center>

BrainPy仿真的HH模型的V-t图如下所示。我们在上一节中曾经提到，真实的动作电位可以分为去极化、复极化和不应期三个阶段，这三个阶段可以与下图一一对应。另外，在去极化时，可以看到膜电位先是累积外部输入缓慢上升，一旦越过某个特定值（图中约在-55mV左右）就转为快速增长，这也复现了真实动作电位的形状。

<center><img src="../../figs/neus/out/output_27_0.png">	</center>



### 参考资料

<span id="fn_1"></span>[1] Gerstner, Wulfram, et al. Neuronal dynamics: From single neurons to networks and models of cognition. Cambridge University Press, 2014.

