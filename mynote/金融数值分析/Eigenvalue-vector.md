- 理解幂法首先需要理解矩阵,矩阵是一种变换.更准确的说,这种变化是一种在特征向量上进行投影的操作.特征向量的特征值对应投影的"程度",特征值越大,意味这个矩阵进行的变换是更强的向该特征值对应的特征向量进行投影.因此,幂法就是通过不断的进行矩阵变换,使初始向量越来越与特征向量重合.

## Algorithim
```
def PowerMethod_EigenValueVector(A, E):
    n = len(A)
    z0 = np.random.random((n,1))
    lambda0 = 0.9
    lambda1 = 1.0
    while abs(lambda1 - lambda0) > E:
        lambda0 = lambda1
        w = np.dot(A, z0)
        absw = abs(w)
        i_maxabsw = np.argmax(absw)
        z1 = w/w[i_maxabsw]
        lambda1 = w[0]/z0[0]
        z0 = z1
    eigvalue = lambda1
    eigvector = z1
    return eigvalue, eigvector
```
## Theory
$\text{define z as n-dimensional vector,}A_{n*n}\text{ is target matrix}$
$$
z=c_{1}v_{1}+c_{2}v_{2}+\dots+c_{n}v_{n}
$$
$v_{1},v_{2}\dots\text{is the eigenvector of A}$
$此时把z放进由A特征向量张成的空间里去看,这里运用了特征向量彼此正交的性质$
$对z向量左乘A,再归一化.进行n次这样的操作后$
$$
\begin{aligned}
z^{(m)}&=\sigma_{m} \frac{\lambda_{1}^m\left( c_{1}v_{1}+\frac{\lambda_{2}^m}{\lambda_{1}^m}c_{2}v_{2}+\dots+ \left( \frac{\lambda_{n}}{\lambda_{1}} \right)^mc_{n}v_{n} \right)}{||\lambda_{1}^m\left( c_{1}v_{1}+\frac{\lambda_{2}^m}{\lambda_{1}^m}c_{2}v_{2}+\dots+ \left( \frac{\lambda_{n}}{\lambda_{1}} \right)^mc_{n}v_{n} \right)||}\\
&=\frac{v_{1}}{||v_{1}||}
\end{aligned}
$$
由此,m次变换后的z是对应特征值最大的特征向量.该特征向量是归一化的,但并不是单位向量
$$
\lambda_{1}=\frac{z^{m}*A}{z^m}
$$
