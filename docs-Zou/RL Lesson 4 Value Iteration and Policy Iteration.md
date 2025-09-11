## RL Lesson 4: Value Iteration and Policy Iteration

### 1、 Value Iteration algorithm

With strong connection to RL Lesson 3, and according to the contraction mapping theorem, we use Value Iteration algorithm to solve the BOE to find the optimal policy and optimal state value. 

Looking back into the RL Lesson 3, what is the value iteration algorithm? 
$$
v_{k+1} = f (v_k) = \max_\pi (r_\pi+\gamma P_\pi v_k), \quad \quad k=1,2,3,...
$$
It can be decomposed to two steps:

* Step 1: policy update

  $$
  \pi_{k+1} = =arg \max_\pi(r_\pi+ \gamma P_\pi v_k) \quad---(1)
  $$
  where $v_k$ is given.

* Step 2: value update

  $$
  v_{k+1} = r_{\pi_{k+1}} + \gamma P_{\pi_{k+1}}v_k\quad\quad  ----(2)
  $$
  note that $v_k$ is not a state value, as it is not ensured that $v_k$ satisfies a Bellman equation.

_____

### How to implement the algorithm?

#### Step 1: Policy update

once the $v_k$ is given, we can find out the corresponding optimal policy(temporarily). 

$$
\pi_{k+1}(s) = arg \max_\pi \sum_a  \pi(a|s) \Bigg(\sum_r p(r|s,a)r+ \gamma \sum_{s^{'}} p(s^{'}|s,a)v_k(s^{'})\Bigg),\quad s \in S
$$

With RL Lesson 3,  we could easily solve this problem: 

$$
\pi^{* }(a|s) = \begin{cases}
 1\quad a = a_k^{* }(s)\\
 0\quad a \ne a_k^{* }(s)
 \end{cases}
$$

where $a_k^{*} = argmax_a q_k(a,s)$, and we can calculate the $q_k(a,s)$ easily according to: 

$$
q_k(s,a) = \sum_rp(r|s,a)r+\gamma \sum_{s'} p(s^{'}|s,a)v_k(s^{'})
$$

#### Step 2: Value update

once we got the new temporary optimal policy $\pi_{k+1}$, we can substitute it in the equation (2), and get the brand new $v_{k+1}(s)$

$$
v_{k+1}(s) =  \sum_a  \pi_{k+1}(a|s) \Bigg(\sum_r p(r|s,a)r+ \gamma \sum_{s^{'}} p(s^{'}|s,a)v_k(s^{'})\Bigg),\quad s \in S
$$

Since $\pi_{k+1}$ is greedy, the above equation is simply 

$$
v_{k+1}(s) = \max_a q_k(a,s)
$$

#### Procedure summary:

$$
v_k(s) \rightarrow q_k(s,a) \rightarrow greedy\quad policy\quad \pi_{k+1}(a|s) \rightarrow new\quad value\quad v_{k+1}= \max_a q_k(s,a)
$$

Iterating until $||v_k -v_{k-1}||$  is smaller than a predefined small threshold.

_____

### 2、 Policy Iteration algorithm

Strong connection to RL Lesson 2 & 3, Algorithm description:

Given a random initial policy $\pi_0$

* Step 1: policy evaluation(PE)

  Calculate the state value of  $\pi_k$  (The Bellman Equation)

  $$
  v_{\pi_k} = r_{\pi_k} + \gamma P_{\pi_k} v_{\pi_k}
  $$

* Step 2: policy improvement (PI)

  According to BOE, 

  $$
  \pi_{k+1} = =arg \max_\pi(r_\pi+ \gamma P_\pi v_k)
  $$

____

### Questions  to answer 

1. In the PE step, how to get the state value $v_{\pi_k}$ by solving the Bellman Equation?

   * Closed-form solution:

     $$
     v_{\pi_k} = (I-\gamma P_{\pi_k})^{-1} r_{\pi_k}
     $$

   * Iterative solution:

     $$
     v_{\pi_k}^{(j+1)} = r_{\pi_k} + \gamma P_{\pi_k}v_{\pi_k}^{(j)}, \quad j=0,1,2,...
     $$

2. It can be proved that the new policy $\pi_{k+1}$ is better than $\pi_k$ and such an iterative algorithm finally reach an optimal policy!

___

### How to implement the algorithm?

#### Step 1: Policy evaluation

$$
v_{\pi_k}^{(j+1)}(s)=\sum_a \pi_k(a|s)[\sum_rp(r|s,a)r+\gamma \sum_{s'} p(s^{'}|s,a)v_{\pi_k}^{(j)}(s^{'})]
$$

stop when $j \rightarrow \infty$ or $j$ is sufficiently large or $||v_{\pi_k}^{(j+1)} - v_{\pi_k}^{(j)}||$ is sufficiently small.

#### Step 2: Policy improvement

$$
\pi_{k+1}(s) = arg \max_\pi \sum_a  \pi(a|s) \Bigg(\sum_r p(r|s,a)r+ \gamma \sum_{s^{'}} p(s^{'}|s,a)v_{\pi_k}(s^{'})\Bigg),\quad s \in S
$$

Here, $q\_{\pi_k}(s,a)$ is the action value under policy $\pi_k$. Let 

$$
a_k^{* }(s) = arg \max_a q_{\pi_k}(a,s)
$$

Then, the new greedy policy is :

$$
\pi_{k+1}(a|s) = \begin{cases}
 1\quad a = a_k^{* }(s)\\
 0\quad a \ne a_k^{* }(s)
 \end{cases}
$$

____

