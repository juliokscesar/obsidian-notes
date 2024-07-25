## Transformada de Laplace
Dada uma $f(x)$, a transforamada de Laplace de $f$, denotada por $\mathcal{L}[f(x)$] é:
$$
\mathcal{L} [f(x)](s) \equiv \int_0^{\infty} dx e^{-sx} f(x)
$$
sempre que essa integral imprópria convergir.
**Operação Linear com $\mathcal{L}$:** A transformada é um operador linear, então vale:
$$
\mathcal{L}[c_1 f_1(t) + c_2 f_2(t)] = c_1 \mathcal{L}[f_1(t)] + c_2 \mathcal{L}[f_2(t)]
$$
***Derivadas e Transformada das derivadas:***
Para uma função $f(t)$, a transformada de $f(t)$ e de $f'(t)$ estão relacionadas da seguinte forma:
$$
\mathcal{L}[f'(t)] = s \mathcal{L}[f(t)] - f(0)
$$
Isso também vale para a n-ésima derivada de $f$:
$$
\mathcal{L}[f^{(n)}(t)] = s^n \mathcal{L}[f(t)] - s^{n-1} f(0) - ... - s f^{(n-2)}(0) - f^{(n-1)}(0)
$$
***Solução de e.d.o. de segunda ordem com coeficientes constantes***:
Dada a e.d.o. de segunda ordem:
$$
ay'' + by' + cy = f(t) \cdot 1
$$
Supondo que a solução $y=\phi(t)$ existe, podemos calcular a Transformada da e.d.o.:
$$
a[s^2 Y(s) - sy(0) - y'(0)] + b[sY(s) - y(0)] + cY(s) = F(s)
$$
onde $F(s)$ é a transformada de $f(t)$ e $Y(s)$ é a transformada de $y$. Resolvendo para $Y(s)$, temos:
$$
Y(s) = \frac{(as+b)y(0) + ay'(0)}{as^2 + bs + c} + \frac{F(s)}{as^2+bs+c}
$$
Agora é só *inverter a transformada* $Y(s)$ para encontrar $\phi(t)$ ($\mathcal{L}[\phi(t)] = Y(s)$).

#### Tabela de algumas Transformadas de Laplace
![[Pasted image 20240527075337.png]]

## Séries
### Séries de Potências
É basicamente aproximar a função $f(x)$ como uma soma de potências:
$$
f(x) = \sum_{n=0}^{\infty}a_n x^n
$$
### Série de Taylor
Dada uma função $f(x)$, o valor de $f(x)$ em torno de um ponto $x_0$ pode ser aproximada pela série infinita:
$$
f(x) = \sum_{n=0}^{\infty} \frac{1}{n!} f^{n} (x_0) (x-x_0)
$$
Se o raio de convergência da série é $\rho > 0$, $f(x)$ é dita analítica em $x=x_0$.

### Solução em série em de potências em torno de um ponto ordinário
Com a e.d.o. da seguinte forma:
$$
P(x) \frac{d^2 y}{dx^2} + Q(x) \frac{dy}{dx} + R(x) y = 0
$$
Verificamos se o ponto $x_0$ é ordinário garantindo que $P(x_0) \neq 0$. Então dividimos a e.d.o. toda por $P(x)$:
$$
\begin{gather}
p(x) \equiv \frac{Q(x)}{P(x)} \\
q(x) \equiv \frac{R(x)}{P(x)} \\
\frac{d^2 y}{dx^2} + p(x) \frac{dy}{dx} + q(x) y = 0
\end{gather}
$$
Sendo $p(x)$ e $q(x)$ duas funções analíticas (existe série de Taylor pra ambas no intervalo em torno de $x_0$). Se alguma não for, o ponto é singular.
Podemos escrever $p(x)$ e $q(x)$ como séries de Taylor:
$$
\begin{gather}

p(x) = \sum_{n=0}^{\infty} \frac{p^{(n)} (x_0)}{n!} (x-x_0)^n \\
q(x) = \sum_{n=0}^{\infty} \frac{q^{(n)} (x_0)}{n!} (x-x_0)^n

\end{gather}
$$
Supondo que existe uma função analítica $\phi(x)$ em torno de $x_0$ tal que:
$$
y = \phi(x) = \sum_{n=0}^{\infty} a_n (x-x_0)^n
$$
onde
$$
a_n = \frac{\phi^{(n)}(x_0)}{n!}
$$
Ao final, encontra-se duas funções $y_1$ e $y_2$ tal que:
$$
y = a_0 y_1(x) + a_2 y_2(x)
$$
onde $y_1$ e $y_2$ são duas séries de potências que também convergem em torno de $x_0$ e formam um conjunto fundamental de soluções (só tacar no Wronskiano e verificar).

### Solução em série em torno de um ponto singular regular
***O que é ponto singular***
Dada uma e.d.o. da forma:
$$
P(x)y'' + Q(x)y' + R(x)y = 0
$$
Um ponto $x_0$ tal que $P(x_0) = 0$ e pelo menos um entre $Q(x)$ e $R(x)$ não se anula em $x_0$ é chamado de ponto singular.

Um ponto singular em $x_0$ é dito regular quando, dada a e.d.o. da forma
$$
\frac{d^2 y}{dx^2} + p(x) \frac{dy}{dx} + q(x)y = 0
$$
com a mesma definição de $p(x) = \frac{Q(x)}{P(x)}$ e $q(x) = \frac{R(x)}{P(x)}$, vale:
$$
\begin{gather}
\lim_{x \rightarrow x_0} (x-x_0)p(x) = p_0 \\
\lim_{x \rightarrow x_0} (x-x_0)^2 q(x) = q_0
\end{gather}
$$
com $p_0$ e $q_0$ números finitos e $(x-x_0)p(x)$ e $(x-x_0)^2q(x)$ funções analíticas em $x_0$ (tem série de Taylor). Caso algum dos limites não seja finito, então o ponto $x_0$ é chamado de um ponto singular irregular.

Multiplicando a e.d.o. por $x^2$:
$$
x^2 \frac{d^2 y}{dx^2} + x [xp(x)] \frac{dy}{dx} + [x^2 q(x)] y = 0
$$
Como $xp(x)$ e $x^2 q(x)$ são funções analíticas em $x_0$, temos:
$$
\begin{gather}

xp(x) = \sum_{n=0}^{\infty} p_n x^n = p_0 + p_1x + p_2x^2 ... = p_0 \left( 1 + \frac{p_1}{p_0} x + \frac{p_2}{p_0}x^2 ... \right) \\

x^2q(x) = \sum_{n=0}^{\infty} q_n x^n = q_0 + q_1x + q_2x^2 ... = q_0 \left( 1 + \frac{q_1}{q_0} x + \frac{q_2}{q_0}x^2 ... \right)

\end{gather}
$$
Supondo que $p_0 \neq 0$ e $q_0 \neq 0$. No caso em que $x_0 = 0$, como estamos interessados em soluções para $x > 0$  próximas de $x_0 = 0$, vemos que $x << 1$ e a e.d.o. se aproxima da chamada **Equação de Euler**:
$$
x^2 \frac{d^2 y}{dx^2} + x p_0 \frac{dy}{dx} + q_0 y = 0
$$
Quando chega numa equação na forma de uma Equação de Euler, supõe-se uma solução da forma:
$$
y=x^r (a_0 + a_1 x + a_2 x^2 + ...) = \sum_{n=0}^{\infty} a_n x^{r+n}
$$
que fica fácil de encontrar uma relação, saindo dessa, para $y'$ e $y''$. 
Usando essa suposição, encontra-se uma equação no meio da solução que é da forma:
$$
r(r-1) + p_0r + q_0
$$
e aí é só achar as raízes dessa equação.
Essa equação é chamada de ***equação indicial***.

### Soluções da Equação de Euler
Uma Equação de Euler é da forma:
$$
L[y] = x^2 y'' + \alpha x y' + \beta y = 0
$$
Como $P(x)=x^2$, o único ponto singular é $x_0 = 0$. Supondo que a equação tem uma solução da forma
$$
y = x^r
$$
obtemos
$$
\begin{align}
L[x^r] &= x^2 (x^r)'' + \alpha x (x^r)' + \beta x^r \\
&= x^r[r(r-1) + \alpha r + \beta]
&= x^r F(r)
\end{align}
$$
Se $r$ é raiz da equação de segundo grau
$$
F(r) = r(r-1) + \alpha r + \beta
$$
então $L[x^r]$ é zero e $y=x^r$ é uma solução. As raízes de $F(r)$ são:
$$
r_1,r_2 = \frac{-(\alpha-1) \pm \sqrt{(\alpha-1)^2 - 4\beta}}{2}
$$
e $F(r)=(r-r_1)(r-r_2)$. 

- Caso raízes reais e distintas:
Se $F(r)$ tem raízes reais $r_1 \neq r_2$, então $y_1 (x) = x^{r_1}$ e $y_2(x) = x^{r_2}$ são soluções. Como o Wronskiano
$$
W[x^{r_1}, x^{r_2}] = (r_2 - r_1)x^{r_1 + r_2 - 1}
$$
não se anula se $r_1 \neq r_2$ e $x>0$, então a solução para a equação de Euler é:
$$
y = c_1 x^{r_1} + c_2 x^{r_2}
$$
OBS: se $r$ não for racional, então $x^r$ é definida por $x^r = e^{x \ln{r}}$.

- Caso raízes iguais:
Se as raízes são tais que $r_1 = r_2$, obtemos somente a solução $y_1(x) = x^{r_1}$. Como $r_1 = r_2$, $F(r) = (r-r_1)^2$. Assim, além de $F(r_1) = 0$, temos também que $F'(r_1) = 0$. Diferenciando a equação, temos:
$$
\frac{\partial}{\partial r} L[x^r] = \frac{\partial}{\partial r} [x^r F(r)]
$$
Substituindo $F(r)$, trocando as ordens de integração em relação a $x$ e a $r$, e notando que $\frac{\partial(x^r)}{\partial r} = x^r \ln{x}$:
$$
L[x^r \ln{x}] = (r-r_1)^2 x^r \ln{x} + 2(r-r_1)x^r
$$
A expressão a direita do sinal de igualdade é 0 para $r = r_1$. Portanto:
$$
y_2(x) = x^{r_1} \ln{x}
$$
é uma segunda solução da Equação de Euler. Calculando o Wronskiano:
$$
W(x^{r_1}, x^{r_1} \ln{x}) = x^{2r_1-1}
$$
Logo, $x^{r_1}$ e $x^{r_1} \ln{x}$ formam um conjunto fundamental de soluções para $x>0$ e a solução geral é:
$$
y = (c_1 + c_2 \ln{x})x^{r_1}, x>0
$$

- Caso raízes complexas:
Caso as raízes sejam complexas conjugadas, de forma: $r_1 = \lambda + i\mu$  e $r_2 = \lambda - i\mu$, e lembrando que $x^r = e^{r \ln{x}}$, usamos a fórmula de Euler para $e^{i\mu \ln{x}}$:
$$
\begin{aligned}
x^{\lambda + i \mu} = e^{(\lambda + i \mu)\ln{x}} &= e^{\lambda \ln{x}} e^{i\mu \ln{x}} = x^{\lambda} e^{i \mu \ln{x}} \\
&= x^{\lambda} [\cos{(\mu \ln{x})} + i \sin{(\mu \ln{x})}]
\end{aligned}
$$
Assim encontra-se uma solução para a Equação de Euler com raízes complexas:
$$
y = c_1 x^{\lambda + i \mu} + c_2 x^{\lambda - i \mu}
$$
A fim de evitar utilizar valores complexos, utilizamos as partes real e imaginária de $x^{\lambda + i \mu}$, que são, respectivamente:
$$
\begin{gather}
x^{\lambda} \cos{(\mu \ln{x})} \\
x^{\lambda} \sin{(\mu \ln{x})}
\end{gather}
$$
que também são soluções da Equação de Euler com raízes complexas. O Wronskiano confirma isso:
$$
W[x^{\lambda} \cos{(\mu \ln{x})}, x^{\lambda} \sin{(\mu \ln{x})}] = \mu x^{2\lambda - 1}
$$
Portanto essas soluções formam um conjunto fundamental de soluções para $x>0$. A solução geral é:
$$
y = c_1 x^{\lambda} \cos{(\mu \ln{x})} + c_2 x^{\lambda} \sin{(\mu \ln{x})}, x> 0
$$
