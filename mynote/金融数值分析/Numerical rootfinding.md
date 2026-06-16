
## 二分法
### 算法
```
	def bisection(a,b,e):   # 二分法求根，a为起点，b为终点，e为误差容限
    c=(a+b)/2  
    sign_fc=np.sign(equation(c))  
    sign_fa=np.sign(equation(a))  
    sign_fb=np.sign(equation(b))  
    while b-c>e:  
        if sign_fb*sign_fc<=0:  
            a=c  
            sign_fa=sign_fc  
        else:  
            b=c  
            sign_fb=sign_fc  
        c=(a+b)/2  
        sign_fc=np.sign(equation(c))  
    root=c  
    return root
    
    def myfun_equation(x):  # 要对哪一个函数进行求根
    f = 1000*((1+x/12)**480-1) - 5000*(1-(1+x/12)**(-240))
    return f
```
### 误差与收敛速度

$设a_{n},b_{n},c_{n}分别表示a,b,c第n次的计算值,c为ab中点$
$$b_{n+1}-a_{n+1}=\underbrace{ \frac{1}{2}(b_{n}-a_{n}) }_{ 收敛速度 }$$ 
$递推可得$
$$b_{n}-a_{n}=\frac{1}{2^{n-1}}(b-a)$$
$b-a为原始区间长度,又因为\alpha-c_{n} \leq \frac{1}{2}(b_{n}-a_{n})$
$$|\alpha-c_{n}|\leq \underbrace{ \frac{1}{2^n}(b-a)  }_{ error\ tolerance  }$$

## 不动点迭代 
### Algorithm (以牛顿法为例)
```
	def newton(x0,e):   # equation 和 equation_diff需要自己定义
    f=equation(x0)  
    df=equation_diff(x0)  
    x1=x0-f/df      # 根据迭代的具体形式修改,形式为x1=f(x0)
    while abs(x1-x0)>e:  
        x0=x1  
        f=equation(x0)  
        df=equation_diff(x0)  
        x1=x0-f/df  
    root=x1  
    return root
```
### Convergence conditions
Define   $x_{k+1}=\phi(x_{k})$  in $[a,b]$   as iteration function.**To keep convergence**,it needs two condition
$$\begin{aligned}
 a \leq \phi(x) \leq b \\
 |\phi'(x)|\leq 1
\end{aligned}
$$
$Prove$
$$
|x_{k}-\tilde{x}|=|\phi(x_{k-1})-\phi(\tilde{x})|\leq |\phi'(\varepsilon)||x_{k-1}-\tilde{x}|\leq \phi'^k|x_{0}-\tilde{x}|
$$
$because\quad |\phi'(\varepsilon)\leq 1|$

$$
\lim_{ k \to \infty }|x_{k}-\tilde{x}| =0
$$
$即当\phi'(x)\leq 1时,该迭代方法收敛到唯一值.该定理多在局部条件下运用.做题时只需要判断\phi'(\tilde{x})是否小于1即可$
![[Pasted image 20251222150417.png]]
### 误差与收敛速度
$$
\begin{aligned}
L&=max(\phi'(x))\\
|x_{k}-\tilde{x}|&\leq \frac{L^k}{1-L}|x_{1}-x_{0}|\\
|x_{k}-\tilde{x}|&\leq \frac{1}{1-L}|x_{k+1}-x_{k}|
\end{aligned}
$$
两个公式体现了两种研究方法
- 研究误差,是看在原有选定范围$[x_{0},x_{1}]$之间,每一次迭代缩短了多少.$x_{1}和x_{0}$已知的情况下,选定误差,就是选定了迭代次数
- 研究误差收敛速度,是与上一次迭代$x_{k+1}-x_{k}$做对比,当L小于1时,可以看见该迭代可能是在逐渐加速的,但这里由于是不等号,收敛的过程可能一段时间快,一段时间慢.因此需要更严谨的定义**收敛速度**

$prove$
$$
\begin{aligned}
\because\phi'(x)&\leq 1 \quad 迭代收敛\\
\therefore |x_{k+1}-x_{k}|\leq |x_{k}-x_{k-1}|&\leq |x_{k-1}-x_{k-2}|\leq \dots\leq |x_{1}-x_{0}|\\
则有|x_{k+p}-x_{k}|&\leq |x_{k+p}-x_{k+p-1}+x_{k+p-1}-x_{k+p-2}+\dots-x_{k}|\\
&\leq |x_{k+p}-x_{k+p-1}|+|x_{k+p-1}-x_{k+p-2}|+\dots+|x_{1}-x_{0}|\\
&\leq (L^{k+p-1}+L^{k+p-2}+\dots+L^k)|x_{1}-x_{0}|\\
&\leq \underset{ 当p趋于无穷时成立 }{ \frac{L^k}{1-L}|x_{1}-x_{0}| }

\end{aligned}
$$

第二个不等式证明同理可得

### 迭代法收敛速度
定义$e_{k}=x_{k}-\tilde{x}$表示第k次迭代的误差,则误差速度定义为
$$
\lim_{ k \to \infty }\frac{|e_{k+1}|}{|e_{k}|^p}=c
$$
	若c为常数,则称该算法是**p阶收敛**.
		$p=1,c>0$时,称为线性收敛
		$p=1,c=0$时,称为超线性收敛
		$p=2$时,称为平方收敛.
		p越大,说明收敛的越快.

迭代法的收敛阶数**取决于$\phi(x)$在$\tilde{x}$处的导数**.求导求到哪一阶不为0了,该迭代就是几阶收敛.
换句话说,一个p阶收敛的迭代函数$\phi(x)$,它需要满足p-1阶导数都为0,p阶导数不为0.
证明如下
$$
\begin{aligned}
x_{k+1}=\phi (x_{k})&=\phi(\tilde{x})+\phi'(\tilde{x})(x_{k}-\tilde{x})+\phi''(\tilde{x})(x_{k}-\tilde{x})^2+\dots+\frac{\phi^{(p-1)}(\tilde{x})(x_{k}-\tilde{x})^{p-1}}{(p-1)!}+\frac{\phi^{(p)}(\varepsilon)(x_{k}-\tilde{x})^p}{p!}\\
&=\phi(\tilde{x})+\frac{\phi^{(p)}(\varepsilon)(x_{k}-\tilde{x})^p}{p!}
\\
\end{aligned} 
$$

$当k趋向于无穷时,由于该迭代法是收敛的,因此有\lim_{ k \to \infty }\varepsilon=\tilde{x}$
$$
 \frac{x_{k+1}-\tilde{x}}{(x_{k}-\tilde{x})^p}=\frac{\phi^{(p)}(\tilde{x})}{p!}  \tag1 
$$

### 牛顿法的误差与收敛速度
$牛顿法的基本思想是一阶泰勒展开$
$$
\begin{aligned}
f(x)=f(\tilde{x})+f'(\tilde{x})(x-\tilde{x}) 
\end{aligned}
$$
$取f(x)=0时的x值$
$$
\begin{aligned}
0=f(\tilde{x})+f'(\tilde{x})(x-\tilde{x})\\
x=\tilde{x}-\frac{f(\tilde{x})}{f'(\tilde{x})}
\end{aligned}
$$
$\phi x=\tilde{x}-\frac{f(\tilde{x})}{f'(\tilde{x})}即为迭代公式,于是牛顿法的误差问题便转化为迭代公式\phi x的误差问题$
$$
\begin{aligned}
\phi'x&=1-\frac{f'(x)^2-f(x)*f''(x)}{f'(x)^2}\\
\phi'x&=\frac{f(x)*f''(x)}{f'(x)^2}
\end{aligned}

$$
$当这里x为不动点\tilde{x}时,\phi 'x=0,因此牛顿法至少是二阶收敛的,令p=2,代入公式(1),可得到误差估计$
$$
x_{k+1}-\tilde{x}=-\frac{f''(\tilde{x})}{2f'(\tilde{x})}(x_{k}-\tilde{x})^2
$$
$\text{define } M=-\frac{f''(\tilde{x})}{2f'(\tilde{x})}$
$$
\begin{aligned}
M(x_{k+1}-\tilde{x})&=(M(x_{k}-\tilde{x}))^2\\
M(x_{k+1}-\tilde{x})&=\underbrace{ (M(x_{0}-\tilde{x}))^{2^n} }_{ 牛顿法的误差公式 }
\end{aligned}
$$
$因此,如果想要选择的初值能够收敛到不动点,则要求x_{0}满足以下$
$$
\begin{aligned}
M(x_{0}-\tilde{x})&<1\\
|\tilde{x}-x_{0}|&<|\frac{2f'(\tilde{x})}{f''(\tilde{x})}|
\end{aligned}
$$
### 割线法
```
	def myfun_rootfinding_secant(x0, x1, e):
    f0 = myfun_equation(x0)
    f1 = myfun_equation(x1)
    x2 = x1 - f1/((f1-f0)/(x1-x0))
    while abs(x2 - x1) > e:
        x0 = x1
        f0 = f1
        x1 = x2
        f1 = myfun_equation(x1)
        x2 = x1 - f1/((f1-f0)/(x1-x0))
    root = x2
    return root
```
$\text{define }\phi x=x_{1}-\frac{f(x_{1})}{f(x_{1})-f(x_{0})}*(x_{1}-x_{0})$
误差没看懂,此处略过.
## 病态求根
### 重根情形
	以牛顿法为例

$若\tilde{x}是f(x)的m重根,则f(x)可以写成:$
$$
f(x)=(x-\tilde{x})^mg(x)
$$
$同样有\phi(x)=x-\frac{f(x)}{f'(x)},但一阶导有变化$
$$
\phi'(x)=1-\frac{1}{m}
$$
$当m不为1时,根据迭代法的收敛规则,一阶导不为0,那么牛顿法最多只有线性收敛的速度$

$因此进行相应改进$
$$
\phi(x)=x-\frac{mf(x)}{f'(x)}
$$
$此时牛顿法为二阶收敛,但很显然,m提前并不知道,因此该方法不实用.更好的方法还没看懂$

### 扰动分析
讨论$\varepsilon$对$\alpha$ 的影响
$$
\alpha(\varepsilon)=\alpha-\varepsilon\frac{g(\alpha_{0})}{f'(\alpha_{0})} 
$$
扰动对根的影响取决于扰动程度,扰动程度对原函数的改变程度,根处原函数的一阶导.
根处原函数一阶导等于0时,相当于只有一个交点,有一点扰动就会没根.

$prove:$
$假设根为\alpha,\alpha 也是\varepsilon的函数,对\alpha 在\varepsilon=0点处泰勒展开$
$$
\alpha(\varepsilon)=\alpha_{0}+\alpha'_{0}\varepsilon \tag2
$$
$$F(x)=f(x)+\varepsilon g(x)
$$
$\varepsilon看成一个变量,F是\varepsilon 的函数$

$$
\begin{aligned}
F(\alpha(\varepsilon))=0
\end{aligned}
$$
$相当于F和\alpha关于\varepsilon 的函数恒=0,因此其导数也恒为0$
$$
f'(\alpha(\varepsilon))\alpha'(\varepsilon)+g(\alpha(\varepsilon))+\varepsilon g'(\alpha(\varepsilon))\alpha'(\varepsilon)=0
$$
$\text{when }\varepsilon=0$
$$
f'(\alpha_{0})\alpha'_{0}+g(\alpha_{0})=0 
$$
$\text{take }\alpha_{0}'\text{ to (2) and get}$
$$
\alpha(\varepsilon)=\alpha-\varepsilon\frac{g(\alpha_{0})}{f'(\alpha_{0})} 
$$

## Aitken acceleration
$$
\begin{aligned}
y_{k}=\phi(x_{k})\\
z_{k}=\phi(y_{k})
\end{aligned}
$$
$\text{assume }\phi'(x)\text{ keep unchange }\phi' =q$
$$
\begin{aligned}
y_{k}-\tilde{x}=q(x_{k}-\tilde{x})\\
z_{k}-\tilde{x}=q(y_{k}-\tilde{x})
\end{aligned}
$$
$\text{divide the two equation}$
$$
\tilde{x}=x_{k}-\frac{(y_{k}-x_{k})^2}{z_{k}-2y_{k}+x_{k}}
$$
$\text{replce xtilde to xk+1 then get the alteration function}$

$$
Tooldep=\alpha_{1}+\beta_{11}*Demand+\beta_{12}GPA+\beta_{13}*Risk+\beta_{14}*Attitude+\beta_{15}*Control+\varepsilon_1
$$![[12.24重构.docx]]