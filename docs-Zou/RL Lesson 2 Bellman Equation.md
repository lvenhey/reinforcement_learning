## RL Lesson 2: Bellman Equation

### 1、State Value

The value of one state relies on the values of other state

> What is the difference between the return and the state value?

Return is calculated for a single trajectory whereas state value is the average of returns of multiple trajectories.

To put it another way, for one policy, a state may have different trajectories.

> So what is the definition of state value?

It's the **expectation** of  G<sub>t</sub>

----------

### PS: Typora Skills

* Formulas in the context (MD)

  * A<sub>b</sub> : A\<sub>b\</sub> ; 
  * A<sup>b</sup> : A\<sup>b\</sup>;
  * <font color=blue>blue</font> : \<font color=blue>blue\</font>;
  * <u>s</u> : \<u>s\</u>;
  * **a** :\**a**;

* Formula Para(LaTex)

  * \sqrt{X}:

  $$
  \sqrt{X}
  $$

  

  * \sum

  $$
  \sum
  $$

  

  * \prod

  $$
  \prod
  $$

  

  * \div
    $$
    \div
    $$
    
  * \times
    $$
    \times
    $$
    
  * \frac{x}{y}
    $$
    \frac{x}{y}
    $$
    
  * \sin(x)
    $$
    \sin(X)
    $$
    
  * x_0
    $$
    x_0
    $$
    
  * x^0
    $$
    x^0
    $$
    

  For more, checks [here]([最全Typora语法大全（含详细数学表达式及流程图） - 知乎](https://zhuanlan.zhihu.com/p/138627806))
  
  

-------

#### Come back to the G<sub>t</sub>

$$
v_\pi(s)=E[G_t|S_t=s]
$$

#### What is G<sub>t</sub>?:

$$
G_t = R_+\gamma R_{t+2}+\gamma^2 R_{t+3}+....
$$

#### so it can also be written like:

$$
G_T=R_{t+1} +\gamma G_{t+1}
$$



_______

### 2、 Derivation of Bellman Equation

#### Firstly, what is the State value? How to calculate it?

$$
v_\pi(s)=E[G_t|S_t=s]
$$

The state value can also represented as : 
$$
v_\pi (s) = E[R_{t+1}|S_t=s]+\gamma E[G_{t+1}|S_t=s]\\
=\sum_a \pi(a|s) \sum_r p(r|s,a)r + \sum_{s^{'}} E[G_{t+1}|S_t=s,S_{t+1}=s^{'}]p(s^{'}|s)
$$
 This formula is relatively interesting, because it connects the $$v_\pi(s)$$ with $$v_\pi(s^{'})$$ .

#### $$E[G_{t+1}|S_t=s,S_{t+1}=s^{'}]$$=$$E[G_{t+1}|S_{t+1}=s^{'}]$$

makes sense due to the memoryless Markov  property.







