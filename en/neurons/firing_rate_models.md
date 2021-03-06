
## 1.4 Firing Rate models

Firing Rate models are simpler than reduced models. Typically, firing rate models are used in network models, and they are regarded as compute units, with each of them representing a neuron group. The state of a computation unit is not described by the membrane potential variable $$V$$ but by the firing rate variable $$a$$ (or $$r$$ or $$\nu$$). Here we introduce a firing rate unit in the classical Wlison and Cowan model.

### 1.4.1 Firing Rate Unit

Wilson and Cowan (1972) proposed this unit to represent the activities in excitatory and inhibitory cortical neuron columns. Each element of variables $$a_e$$ and $$a_i$$ refers to the average activity of a neuron column group contains multiple neurons.

$$
\tau_e \frac{d a_e(t)}{d t} = - a_e(t) + (k_e - r_e * a_e(t)) * \mathcal{S}(c_1 a_e(t) - c_2 a_i(t) + I_{ext_e}(t))
$$

$$
\tau_i \frac{d a_i(t)}{d t} = - a_i(t) + (k_i - r_i * a_i(t)) * \mathcal{S}(c_3 a_e(t) - c_4 a_i(t) + I_{ext_i}(t))
$$

$$
\mathcal{S}(x) = \frac{1}{1 + exp(- a(x - \theta))} - \frac{1}{1 + exp(a\theta)}
$$

The subscript $$x\in\{e, i\}$$ points out whether this parameter or variable corresponds to excitatory or inhibitory neuron group. In the differential equations, $$\tau_x$$ refers to the time constant of neuron columns, parameters $$k_x$$ and $$r_x$$ control the refractory periods, $$a_x$$ and $$\theta_x$$ refer to the slope factors and phase parameters of sigmoid functions, and external inputs $$I_{ext_{x}}$$ are given separately to excitatory and inhibitory neuron groups.

<center><img src="../../figs/neus/codes/en/frunit1.png">	</center>

<center><img src="../../figs/neus/codes/en/frunit2.png">	</center>

