# Error of interpolation(Lagrange version)
$\text{define }P_{n}(x)\text{ as the Lagrange's third-order interpolation function}$
$$
P_{n}(x)=y_{0}L_{0}(x)+y_{1}L_{1}(x)+\dots+y_{n}L_{n}(x)
$$
then Error is
$$
f(x)-P_{n}(x)=\frac{f^{n+1}(\varepsilon)}{(n+1)!}(x-x_{0})\dots(x-x_{n})
$$
$\text{define }w(x)=(x-x_{0})\dots(x-x_{n})\text{, }\varepsilon在[x_{0},x_{n}]之内$

$Prove:$
	main idea is Rolle's Mean value theorem,and an auxiliary function

define $R_{n}(x)=f(x)-P_{n}(x)$

when $x=x_{0},x_{1}\dots x_{n}$ , $R_{n}(x)=0$ ,so define $R_{n}(x)$ in another way
$$
\begin{aligned}
R_{n}(x)=K(x)*w(x)
\end{aligned}
$$
To determine the form of $K(x)$, we create $\phi(t)$ 
$$
f(x)-P_{n}(x)=K(x)*w(x)
$$
$两边对x求n+1阶导数,为了能够得到一个更干净的函数形式,以下的求导结果是当x=x_{1},x_{2},x_{n}时的结果$
$$
f^{(n+1)}(x)=K(x)(n+1)!
$$
以上是我**错误**的思路,从这里可以看出构建辅助函数的trick在哪里.它解决了我求出来的K(x)只在$x_{1},x_{2},x_{n}$适用的局限性.它的主要思想是求$K(x)$,那就把$K(x)$固定住.然后把x看成一个与x1,x2相同的值,t只有等于$x,x_{1}\dots$时才有$\phi=0$
果然走错路之后才懂正确的理论正确在哪XD


# Newton interpolation and Taylor expansion
## Theroy of Newton interpolation
$$
P_{n}(x)=f(x_{0})+f[x_{0},x_{1}](x-x_{0})+f[x_{0},x_{1},x_{2}](x-x_{1})(x-x_{0})+f[x_{0},x_{1},x_{2},x_{3}](x-x_{1})(x-x_{0})(x-x_{2})+\dots+f[x_{0},x_{1},\dots,x_{n}](x-x_{0})(x-x_{1})\dots(x-x_{n-1})
$$
如何理解该公式?
	牛顿法的基本思想是等差数列的叠加.n个点确定n-1层等差数列.一阶差商就刻画了第一层等差数列.这种理解只有才确定新一项的函数形式的时候才生效.外推的时候有一定变化,但在理解层面上足够了. 
	而对于$w(x)$,更通顺的理解需要把$x_{1}看成x_{0}+h,x_{n}=x_{0}+nh$,它其实是用了拉格朗日基函数的思想.求差商的时候除掉的要用w(x)补回来

## Error of Newton interpolation
$\text{see t as a new point like }x_{1},x_{2}\dots$
$$
f(t)-P_{n}(t)=(t-x_{0})(t-x_{1})\dots(t-x_{n})f[x_{0},x_{1},\dots,x_{n},t]
$$
$\text{compare to Lagrange version}$
$$
f(x)-P_{n}(x)=\frac{f^{n+1}(\varepsilon)}{(n+1)!}(x-x_{0})\dots(x-x_{n})
$$
$\text{we often use Lagrange version to estimate the error}$
$$
R_{n}(x)\leq\frac{w(t)*f^{(n+1)}(c_{x})}{(n+1)!}
$$
