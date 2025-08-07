## RL Lesson 2: Bellman Equation

### 1、State Value

The value of one state relies on the values of other state

​	![Bootstrapping](D:\ZJU\RL-learning\reinforcement_learning\printscreen\C2\Bootstrapping.png)

> What is the difference between the return and the state value?

Return is calculated for a single trajectory whereas state value is the average of returns of multiple trajectories.

To put it another way, for one policy, a state may have different trajectories.

> So what is the definition of state value?

It's the expectation of  G<sub>t</sub>

----------

#### PS: Typora Skills

* Formulas in the context

  * A<sub>b</sub> : A\<sub>b\</sub> ; 
  * A<sup>b</sup> : A\<sup>b\</sup>;
  * <font color=blue>blue</font> : \<font color=blue>blue\</font>;
  * <u>s</u> : \<u>s\</u>;

* Formula Para

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

* 

-------

#### Come back to the G<sub>t</sub>

$$
v_\pi(s)=E[G_t|S_t=s]
$$















