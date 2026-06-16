# 梯形法
## Algorithm
```
def myfun_integral_fun(x):
    f = np.sin(x)
    return f
def myfun_integral_trapezoid(a, b, n):
    x_0 = a
    x_n = b
    h = (x_n - x_0)/n
    xp = np.arange(x_0, x_n+h, h)
    fxp = myfun_integral_fun(xp)
    fxp[0] = fxp[0]/2
    fxp[-1] = fxp[-1]/2
    Tn = np.sum(fxp)*h
    return Tn
```

## 复合梯形公式
$$
\int_{a}^b f(x)=h\left[  \frac{1}{2}f(a)+f(x_{1})+f(x_{2})+\dots+\frac{1}{2}f(b)  \right]
$$
## Error
$$
R_{n}(x)=\int _{a}^b f(x)dx-T_{n}(f)=-\frac{h^2(b-a)}{12}f''(c_{n})\approx-\frac{h^2}{12}(f'(b)-f'(a))
$$
$Prove:$
$积分的近似基本思想都来源于插值函数,是把f(x)替换为可积的多项式函数,然后再细分积分区间.$
**因此,分析积分的误差,是在分析插值法的误差**
$梯形法的误差实际上是由线性插值的误差表示的$
$$
R(x)=\int_{a}^b \left( f(x)-\left( \frac{x-b}{a-b}f(a)+\frac{x-a}{b-a}f(b) \right) \right )dx
$$
$显然线性插值的误差积分得到了梯形法的误差,先考虑一个子区间$
$$
\begin{aligned}
R_{1}(x)&=\int_{x_{0}}^{x_{1}} f(x)-\left( \frac{x-x_{1}}{x_{0}-x_{1}}f(x_{0})+\frac{x-x_{0}}{x_{1}-x_{0}}f(x_{1}) \right) \\
&=\int _{x_{0}}^{x_{1}} \frac{f^{(2)}(\gamma)}{(n+1)!}(x-x_{0})(x-x_{1}) 
\end{aligned}

$$
$假设x_{0},x_{1}\dots等距,距离为h.则x_{0}=0,x_{1}=h$
$$
\begin{aligned}
R_{1}(x)=-\frac{f^{(2)}(\gamma_{1})h^3}{12}\\
\end{aligned}
$$
$\gamma_{1}在区间(0,h)之内$
$$
\begin{aligned}
R(x)=\sum_{j=1}^n R_{j}(x)&=- \frac{h^3}{12} (f^{(2)}(\gamma_{1})+f^{(2)}(\gamma_{2})+f^{(2)}(\gamma_{3})+\dots+f^{(2)}(\gamma_{n}))\\
&=- \frac{h^2}{12}(x_{n}-x_{0})(f^{(2)}(c_{n}))

\end{aligned}
$$
$\gamma足够密集时,还可以用积分表示$
$$
R(x)=-\frac{h^2}{12}\int_{0}^{x_{n}}f^{(2)}(x)dx=-\frac{h^2}{12} (f'(x_{n})-f'(0))
$$
## 辛普森复合插值公式
	只是采用2阶拉格朗日插值替换了f(x)

$对单个区间有$
$$
\begin{aligned}
\int_{0}^{2h}f(x)dx &\approx \int_{0}^{2h}\left( \frac{(x-h)(x-2h)}{(0-h)(0-2h)}f(0)+ \frac{(x-0)(x-2h)}{(h-0)(h-2h)}f(h)+\frac{(x-0)(x-h)}{(2h-h)(2h-0)}f(2h)     \right )dx\\
 &= \frac{h}{3}[f(a)+4f(h)+f(2h)]
\end{aligned}
$$
$\text{take all bin together}$
$$
\int_{x_{0}}^{x_{n}}f(x)dx=\frac{h}{3}(f(x_{0})+4f(x_{1})+2f(x_{2})+4f(x_{3})+\dots+2f(x_{n-2})+4f(x_{n-1})+f(x_{n}))
$$
$\text{h is the diestance between }x_{n-1}\text{ and }x_{n}$
**n must be odd number**
## Error
$\text{similar to Error of trapezoid way}$
$$
R(x)=- \frac{h^4(b-a)}{180}f^{(4)}(c_{n})=-\frac{h^4}{180}(f^{(3)}(b)-f^{(3)}(a))
$$
二阶插值理论上误差应该只是三阶导,但由于对称性,三阶导被消掉了.因此需要对三阶导进行展开.得到误差为四阶导.

## 理查森外推
$$
R(x)=-\frac{(a-b)^4}{180n^4}(f^{(3)}(b)-f^{(3)}(a))

$$
$define\quad c=\frac{(a-b)^4}{180}(f^{(3)}(b)-f^{(3)}(a))\quad p=4$
$$
R(x)=\frac{c}{n^p}
$$
因此可以进行两次数值积分,从误差路径导向真实值
$$
\begin{aligned}
I-I_{n}=\frac{c}{n^p}\\
I-I_{2n}=\frac{c}{n^p 2^p}\\
\end{aligned}
$$
$化简得到$
$$
I-I_{2n}=\frac{I_{2n}-I_{n}}{2^p-1}
$$
