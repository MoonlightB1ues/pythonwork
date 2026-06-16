## 梯形方法
$$
\begin{aligned}
Y'(x)=\lambda Y(x)
\end{aligned}
$$
$两边同时做积分,用梯形方法近似$
$$
\begin{aligned}
Y(x_{k+1})&=Y(x_k)+\frac{\lambda*h}{2}[Y(x_{k+1})-Y(x_{k})]\\
Y(x_{k+1})&=Y(x_{k})\left( \frac{1+\frac{h\lambda}{2}}{1-\frac{h\lambda}{2}} \right)\\
\end{aligned}
$$
$when\quad \lambda<0,\text{the iteration is stable}$


## 龙格-库塔法
	方法涉及多元泰勒展开,并且数值解和解析解符号上分清楚就很困难.因此只分析该方法带来的一些直觉
### Theory
$\text{In 梯形方法 we have}$
$$
\left\{
\begin{aligned}
y_{n+1}&=y_{n}+\frac{h}{2}(K_{1}+K_{2})\\
K_{1}&=f(x_{n},y_{n})\\
K_{2}&=f(x_{n+1},y_{n+1})
\end{aligned}
\right.

$$
$\text{直觉上,梯形法可以理解为用}x_{n},x_{n+1}\text{处的斜率加权一下,然后来预测}y_{n+1}$

$龙格法延拓了这种思想$
$$
\left\{
\begin{aligned}
y_{n+1}&=y_{n}+h(\alpha_{1}K_{1}+\alpha_{2}K_{2}+\alpha_{3}K_{3})\\
K_{1}&=f(x_{n},y_{n})\\
K_{2}&=f(x_{n+1},y_{n+1})\\
K_{3}&=f(x_{n+2},y_{n+2})\\
\alpha_{1}&+\alpha_{2}+\alpha_{3}=1
\end{aligned}
\right.
$$
$\text{its third order longge way,it has 三阶精度}$
