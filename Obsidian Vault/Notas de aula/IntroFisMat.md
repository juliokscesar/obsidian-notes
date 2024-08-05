## Número imaginário e representações

Apresenta e envolve nos cálculos o número imaginário $i$:
$$ i^2 = -1 $$
Dado um número complexo da forma $z = a + bi$, temos que a *parte real* é Re$(z) = a$ e a *parte imaginária* é Im$(z) = b$. Assim o número $z$ pode ser representado como um par ordenado de forma que:
$$
\begin{aligned}
	z &= a + bi \\
	&= (Re(z), Im(z)) \\
	&= (a, b)
\end{aligned}
$$
Um número complexo sem parte real é chamado de *imaginário puro*. Tal como: $z_1 = \pi i$.

## Conjugado
Dado um número complexo $z=a+bi$, seu conjugado é $z^*=\overline{z} = a - bi$. O conjugado de um número complexo auxilia na remoção do $i$ no denominador em frações. É só inverter o sinal da(s) parte(s) imaginária(s). Exemplo:
$$
\begin{aligned}

\frac{2}{5+4i} * \frac{5-4i}{5-4i} &= \\
&= \frac{10-8i}{25-20i+20i-16i^2} \\
&= \frac{10-8i}{25+16} \\
&= \frac{10}{41} - \frac{8}{41} i

\end{aligned}
$$
## Raízes de números complexos
$$ x^2 = i$$

### Fórmula de Euler
Dada uma função complexa $u(\theta) = \cos{\theta} + i \sin{\theta}$, sua derivada, dada por $\frac{du}{d\theta}$, é:
$$
\begin{aligned}
	\frac{du}{d\theta} &= -\sin{\theta} + i \cos{\theta} \\
	&= i(\cos{\theta} + i \sin{\theta}) \\
	&= i u
\end{aligned}
$$
Logo, $\int \frac{du}{d\theta} = e^{i \theta}$.
A definição da fórmula de Euler fica:
$$e^{i \theta} = \cos{\theta} + i \sin{\theta}$$

O módulo do número complexo $z= a + bi$ é dado por:
$$ |z| = \sqrt{a^2 + b^2} $$
A *representação polar* de um número complexo fica:
$$ z = |z| e^{i \theta} = |z| \cos{\theta} + i |z| \sin{\theta} = |z| (\cos{\theta} + i \sin{\theta})$$
e o ângulo $\theta$ é denominado *argumento* do número complexo.
![[plano_complexo.png]]

Como $z = |z| e^{i \theta}$ e considerando que $e^{\ln{|z|}} = |z|$, temos que:
$$ z = e^{\ln{|z|} + i \theta} = e^{\alpha + i \theta} = e^{\alpha} e^{i \theta} = |z|e^{i \theta} $$
$$ \alpha = \ln{|z|} $$
### Operações com números complexos
Dados $z_1 = |z_1| e^{i \theta_2}$ e $z_2 = |z_2| e^{i \theta{2}}$:
$$
\begin{aligned}
z_1 z_2 &= |z_1 z_2| e^{i (\theta_1 + \theta_2)} \\

\frac{z_1}{z_2} &= | \frac{z_1}{z_2} | e^{i (\theta_1 - \theta_2)}, z_2 \

\end{aligned}
$$
### Raízes quadradas complexas de $i$
Achar $z$ tal que $z^2 = i$:
$$
\begin{aligned}

z &= |z| e^{i \theta} \\
z^2 &= |z|^2 e^{2i \theta} \\
Re(z^2) &= |z|^2 \cos{2 \theta} = 0, 2 \theta = \frac{\pi}{2}, \frac{3\pi}{2}... \\
Im(z^2)&= |z^2| \sin{2 \theta} = 1, 2 \theta = \frac{\pi}{2}, \frac{5\pi}{2}

\end{aligned}
$$
**Exemplo**: Calcule todas as raízes cúbicas de $e^{i \frac{\pi}{3}}$.
$$
\begin{aligned}

z^3 &= e^{i \frac{\pi}{3}} \\
z^3 &= |z|^3 e^{3i\theta} \\
|z|^3 e^{3i\theta} &= e^{i \theta} \\
|z|^3 = 1 \ &... \ |z| = 1 \\ \\

e^{3i \theta} &= e^{i \theta} \\
\cos{3 \theta} + i \sin{3 \theta} &= \cos{\frac{\pi}{3}} + i \sin{\frac{\pi}{3}} \\
\cos{3 \theta} &= \cos{\frac{\pi}{3}} \\ 
\sin{3 \theta} &= \sin{\frac{\pi}{3}} \\ \\

3 \theta &= \frac{\pi}{3} + k 2\pi, k=0, \pm 1, \pm2, \pm3... \\
\theta &= \frac{\pi}{9} + \frac{2 \pi}{3} k

\end{aligned}
$$
Nesse caso, o $\theta$ das raízes vai de $k=0,1,2$ apenas, pois depois começa a repetir os pontos.

Caso $z^{3} = i$.
$$
\begin{aligned}

z^3 &= i \\
z^3 &= \cos{\theta} + i \sin{\theta}, \theta = \frac{\pi}{2} \\
e^{3\alpha + 3i\theta} &= i = e^{i \frac{\pi}{2}} \\ \\

3\alpha + 3i \theta &= i \frac{\pi}{2} + k 2\pi i, k=0,\pm1,\pm2,... \\
\alpha = 0 \ &> |z|=1 \\
3 \theta &= \frac{\pi}{2} + k 2 \pi \\
\theta_{k} &= \frac{\pi}{6} + k \frac{2\pi}{3}


\end{aligned}
$$
### Funções de variável complexa
$$ f(z) = e^{z} = e^{x+iy} = e^x e^{iy} = e^{x} (\cos{y} + i \sin{y})$$
$$
\begin{aligned}

Re(f(z)) &= e^x \cos{y} \\
Im(f(z)) &= e^x \sin{y}

\end{aligned}
$$
Exemplo função cosseno:
$$
\begin{aligned}

e^{i \theta} &= \cos{\theta} + i \sin{\theta} \\
+\  e^{-i \theta} &= \cos{\theta} - i \sin{\theta} \\
e^{i \theta} + e^{-i \theta} &= 2 \cos{\theta} \\ \\

\cos{\theta} &= \frac{e^{i \theta} + e^{-i\theta}}{2} \\
\sin{\theta} &= \frac{e^{i \theta} - e^{-i \theta}}{2i}

\end{aligned}
$$

Função cosseno de números complexos, dado $z = x + iy$:
$$
\begin{aligned}

\cos{z} = \frac{e^{iz} + e^{-iz}}{2} \\
\sin{z} = \frac{e^{iz} - e^{-iz}}{2i}

\end{aligned}
$$
considerando que
$$
\begin{aligned}

e^{iz} &= e^{-y} \cos{x} + i e^{-y}\sin{x} \\
z &= x + iy = \sqrt{x^2 + y^2}(\cos{\theta} + i \sin{\theta}) \\

\cos{\theta} &= \frac{x}{\sqrt{x^2 + y^2}} \\
\sin{\theta} &= \frac{y}{\sqrt{x^2 + y^2}}

\end{aligned}
$$

### Fórmula de de Moivre

$$
\begin{aligned}

(\cos{\theta} + i \sin{\theta})^{n} &= (e^{i \theta})^{n} = e^{i n \theta} = \cos{n \theta} + i \sin{n \theta} \\
(\cos{\theta} + i \sin{\theta})^n &= \cos{n \theta} + i \sin{n \theta}

\end{aligned}
$$

### Logaritmo de uma variável complexa
$$
\begin{aligned}

z &= |z| e^{i \theta} \\
\ln{z} &= \ln{(|z| e^{i \theta})} \\
&= \ln{|z|} + \ln{e^{i \theta}} \\
&= \ln{|z|} + i \theta

\end{aligned}
$$
No entanto, considerando que vale $e^{i \theta} = e^{i \theta + 2\pi i n}$, temos:
$$
\begin{aligned}

\ln{(|z| e^{i \theta})} &= \ln{(|z| e^{i \theta + 2 \pi i n})} \\
&= \ln{|z|} + i \theta + 2 \pi n i

\end{aligned}
$$
o que indica que a definição feita é ambígua, e pra cada $n$ existe um logaritmo diferente. Então limita-se a função para o intervalo $\theta \in [0, 2\pi]$.

**Mudança de base**:
Dados $v, w, z \in \mathbb{C}$:
$$
\begin{aligned}

z^w = v & \rightarrow \log_z{v} = w \\
\ln{z^w} &= \ln{v} \\
\log_z{v} &= w = \frac{\ln{v}}{\ln{z}} \\
\log_z{v} &= \frac{\ln{|v|} + i \theta_v}{\ln{|z|} + i \theta_z}

\end{aligned}
$$

## Equações diferenciais
$$
\begin{aligned}

y &= f(\theta) = \cos{\theta} + i \sin{\theta} \\
\frac{dy}{d\theta} &= - \sin{\theta} + i \cos{\theta} \\
&= i (\cos{\theta} + i \sin{\theta}) \\
&= iy \\
y &= e^{i \theta} \\ \\

\mathrm{Considerando} \ &Re[f(\theta)] \ \mathrm{e} \ Im[f(\theta)] \\
f(\theta) &= Re[f(\theta)] + i Im[f(\theta)] \\
\frac{df}{d\theta} &= \frac{d}{d\theta} Re[f(\theta)] + i \frac{d}{d\theta} Im[f(\theta)]

\end{aligned}
$$

Equação diferencial em $\mathbb{R}$:
$$
\begin{aligned}

y &= e^{-ax} \\
\frac{dy}{dx} &= -ay \\
dy &= -aydx \\
dy + aydx &= 0

\end{aligned}
$$
### Equação diferencial de 1ª ordem
Equação diferencial de 1ª ordem em x e y, dado $x, y \in \mathbb{R}$:
$$
M(x,y)dx + N(x,y)dy = 0
$$
o objetivo é transformar na seguinte fórmula $p(x) \frac{dy}{dx} + q(x)y = f(x)$. Assim, fazemos:
$$
\begin{aligned}
M(x,y) &= q(x)y - f(x) \\
N(x,y) &= p(x)
\end{aligned}
$$
Exemplo básico:
$$
\begin{aligned}
M(x,y) &= h(x) \\
N(x,y) &= g(y) \\ \\
h(x)dx + g(y)dy &= 0 \\
g(y)dy &= -h(x)dx \\
\int{g(y)dy} &= - \int{h(x)dx}
\end{aligned}
$$
outro (Boyce ex. 2):
$$
\begin{aligned}
\frac{dy}{dx} &= \frac{3x^2 + 4x + 2}{2(y-1)} \\
\int{(2y-2)dy} &= \int{(3x^2 + 4x + 2)dx}
\end{aligned}
$$

#### Diferenciais (recordação)
Variação de uma função $f$:
$$
\Delta f(x) = f(x + \Delta x) - f(x)
$$
o diferencial $df$ é a variação no limite indo a 0. Ficando:
$$
df = f'(x)dx
$$
#### Eq. diferencial exata
$M(x,y)dx + N(x,y)dy = 0$ é *e.d.o. exata* se e somente se existe $f(x,y)$ tal que $df = Mdx + Ndy$.
Se for exata, deve valer:
$$
\frac{\partial M}{\partial y} = \frac{\partial N}{\partial x}
$$
Exemplo 4 (Boyce):
$$
\begin{aligned}

3xy + y^2 + &(x^2 + xy)\frac{dy}{dx} = 0 \rightarrow (* dx) \\
(3xy + y^2)dx + (x^2 + xy)dy &= 0 \rightarrow M(x,y) = 3xy + y^2, \ N(x,y) = x^2 + xy \\

\frac{\partial M}{\partial y} &= 3x + 2y \neq \frac{\partial N}{\partial x} = 2x + y

\end{aligned}
$$
como $\frac{\partial M}{\partial y} \neq \frac{\partial N}{\partial x}$, essa e.d.o. não é exata.

#### Fator integrante ($\mu$)
Supõe-se um fator $\mu (x)$ e multiplicamos a equação anterior toda por ele.
$$
\mu(x) (3xy+y^2)dx + \mu(x)(x^2 + xy)dy = \mu(x) 0 = 0
$$
Supondo agora que essa e.d.o. ficou exata.
$$
\begin{aligned}

M = \mu(x) (3xy + y^2)&, \ N = \mu(x) (x^2+xy) \\
\frac{\partial}{\partial y}[\mu(x)(3xy + y^2)] &= \frac{\partial}{\partial x}[\mu(x)(x^2+xy)] \\

\mu(x)(3x+2y) &= \frac{d\mu(x)}{dx} (x^2+xy) + \mu(x)(2x+y) \\
(x^2+xy)\frac{d\mu(x)}{dx} &+ \mu(x) (2x+y-3x-2y) = 0 \\
(x^2+xy)\frac{d\mu(x)}{dx} &+ \mu(x) (-x-y) = 0 \\
x(x+y) \frac{d\mu(x)}{dx} &= \mu(x) (x+y) \\
x\frac{d\mu(x)}{dx} = \mu(x) &\rightarrow \frac{d\mu}{du} = \frac{dx}{x} \\
\int{\frac{d\mu}{du}} &= \int{\frac{dx}{x}} \\
\ln{|\mu(x)|} &= \ln{|x|} + C \\
|\mu(x)| &= |x| e^C, \ e^C = C' \\
\mu(x) &= \pm |x| C' \\
\mu(x) &= \pm x C', \ C'' = \pm C' \\
\mu(x) &= x C''

\end{aligned}
$$
escolhemos $C'' = 1$ pq sim. Testando fazendo $M(x,y) = x(3xy +y^2)$ e $N(x,y) = x(x^2+xy)$, dá exato (tem que dar se estiver certo) quando testamos $\frac{\partial M}{\partial y} = \frac{\partial N}{\partial x}$. Agora, sendo exata, temos:
$$
df = Mdx + Ndy = 0
$$
que indica que $f(x,y) = C$. Temos:
$$
df = (\frac{\partial f}{\partial x}dx = Mdx) + (\frac{\partial f}{\partial y}dy = Ndy)
$$
Integrando $\frac{\partial f(x,y)}{\partial x} = 3x^2y + xy^2$ em x, e $\frac{\partial f(x,y)}{\partial y}dy = x^3 + x^2y$ em y, temos:
$$
\begin{aligned}
\int{dx} = f(x,y) &= x^3y + \frac{x^2}{2} y^2 + g(y) \\
\int{dy} = f(x,y) &= x^3y + \frac{x^2}{2} y^2 + h(x)
\end{aligned}
$$
como em ambas integrações vale que $f(x,y) = f(x,y)$, então $g(y) = h(x) \ \forall \ x, y$. Logo $g(y) = h(x) = k$. Como $f$ é constante, então:
$$
\begin{aligned}

C = x^3 y + \frac{1}{2} x^2 y^2 + k&, \ C-k = B \\
x^3 y + \frac{1}{2} x^2 y^2 &= B \\
x^2 y^2 + 2x^3 y - D &= 0, \ 2B = D

\end{aligned}
$$
faz o Bhaskara na ultima equação e encontra duas soluções pra e.d.o. pra y(x).

#### Como achar o $\mu$

Com a equação após multiplicar por $\mu$, temos uma relação $\mu' = g(x) \mu$. Assim:
$$
\mu(x) = e^{\int{g(x)dx}}
$$

## Equação diferenciais de segunda ordem com coeficientes constantes
$$
a \frac{d^2 x}{dt^2} + b \frac{dx}{dt} + cx = g(t)
$$
Supõe-se que $a \neq 0$ e define-se dois novos coeficientes: $p=\frac{b}{a}$ e $q=\frac{c}{a}$ e divide-se a equação toda por $a$:
$$
\frac{d^2 x}{dt^2} + p \frac{dx}{dt} + qx = f(t) = \frac{g(t)}{a}
$$
Definimos então o *operador diferencial linear* $\mathbb{L}$:
$$
\mathbb{L} \equiv \frac{d^2}{dt^2} + p \frac{d}{dt} + q
$$

Reorganizando a definição de $\mathbb{L}$ usando a notação de raiz de equação quadrática:
$$
\mathbb{L} = ( \frac{d}{dt} - x_{+} ) (\frac{d}{dt} - x_{-})
$$
considerando que ($x_{+} \ \mathrm{e} \ x_{-}$ são as raízes do operador $\mathbb{L}$ quando é 0):
$$
\begin{aligned}
-(x_+ + x_{-}) &= p \\
x_{+} x_{-} &= q
\end{aligned}
$$
Reescrevemos a e.d.o. então para:
$$
\mathbb{L} x(t) = f(t)
$$
a equação então se desenvolve:
$$
\begin{aligned}
(\frac{d}{dt} - x_{-}) &[(\frac{d}{dt} - x_{+}) x(t)] = f(t) \\
y(t) &= (\frac{d}{dt} - x_{+}) x(t) \\
(\frac{d}{dt} &- x_{-}) y(t) = f(t)
\end{aligned}
$$
**Exemplo (com fator integrante)**: chamando y(t)=g(t), $x_{-}$=c, h(t)=f(t)
$$
\begin{aligned}

(\frac{d}{dt} - c) g(t) &= h(t) \\
\frac{d}{dt} g(t) - c g(t) &= h(t), \ \times \mu(t)  \\
\mu(t) \frac{dg}{dt} - \mu(t)c g(t) &= h(t) \mu(t) \\

\frac{d}{dt}[\mu(t) g(t)] &= \mu(t)h(t), \ \rightarrow \mu'(t) = c\mu(t) \rightarrow \mu(t) = e^{-ct} \\



\end{aligned}
$$

--------------------------------------------
Aula 29/04

## Transformada de Laplace
Dada uma $f(x)$, a transforamada de Laplace de $f$, denotada por $\mathcal{L}[f(x)$] é:
$$
\mathcal{L} [f(x)](s) \equiv \int_0^{\infty} dx e^{-sx} f(x)
$$
sempre que essa integral imprópria convergir.

A ideia de usar a Transformada de Laplace é simplificar as expressões algébricas em problemas mais simples. Primeiro realiza a transformada, então resolve-se o problema para a transformada $\mathcal{L}$ e no final recupera a função inicial $f$.

**Condição de existência**: Para existir a transformada $\mathcal{L}$ de uma função $f$, deve valer que $|f(x)| \leq Ke^{ax}$ quando $t \geq M$, onde $K, a, M$ são constantes reais com $K$ e $M$ necessariamente positivas. Assim, a transformada existe se $s > a$ (parâmetro $s$ da definição).

Exemplos de transformadas:
Seja $f(t) = 1, t \geq 0$:
$$
\mathcal{L}[1] = \int_0^{\infty} e^{-st}dt = - \lim_{A \rightarrow \infty} \frac{e^{-st}}{s} |_{0}^{A} = \frac{1}{s}, s>0
$$

Seja $f(t) = e^{at}, t \geq 0$:
$$
\begin{align}
\mathcal{L}[e^{at}] &= \int_0^{\infty} e^{-st} e^{at} dt \\
&= \int_0^{\infty} e^{-(s-a)t} dt \\
&= \frac{1}{s-a}, s > a
\end{align}
$$

Seja $f(t) = \sin{at}$, $t \geq 0$:
$$
\begin{align}

\mathcal{L}[\sin{at}] &= \int_0^{\infty} e^{-st} \sin{at} \ dt \\

&= \lim_{A \rightarrow \infty} \int_0^A \left[ -\frac{e^{-st} \cos{at}}{a} |_0^A - \frac{s}{a} \int_0^A e^{-st} \cos{at} \ dt \right] \\
&... \\
&= \mathcal{L}[\sin{at}] = \frac{a}{s^2 + a^2}, s>0

\end{align}
$$


**Operação Linear com $\mathcal{L}$:** A transformada é um operador linear, então vale:
$$
\mathcal{L}[c_1 f_1(t) + c_2 f_2(t)] = c_1 \mathcal{L}[f_1(t)] + c_2 \mathcal{L}[f_2(t)]
$$

##### Solução de problemas de valor inicial com Transformada de Laplace
Para uma função $f(t)$, a transformada de $f(t)$ e de $f'(t)$ estão relacionadas da seguinte forma:
$$
\mathcal{L}[f'(t)] = s \mathcal{L}[f(t)] - f(0)
$$
Isso também vale para a n-ésima derivada de $f$:
$$
\mathcal{L}[f^{(n)}(t)] = s^n \mathcal{L}[f(t)] - s^{n-1} f(0) - ... - s f^{(n-2)}(0) - f^{(n-1)}(0)
$$

**Solução de uma equação diferencial homogênea**:
Considerando a equação diferencial $y'' - y' - 2y = 0$ com condições iniciais $y(0)=1, y'(0)=0$. Supomos que o problema tem solução $y = \phi(t)$. Usando a transformada de Laplace na e.d.o. e a propriedade de linearidade:
$$
\mathcal{L}[y''] - \mathcal{L}[y'] - 2 \mathcal{L}[y] = 0
$$
Usando a relação de derivadas da transformada:
$$
s^2 \mathcal{L}[y] - sy(0) - y'(0) - (s\mathcal{L}[y] - y(0)) - 2 \mathcal{L}[y] = 0
$$
ou
$$
(s^2 - s - 2)Y(s) + (1-s)y(0) - y'(0) = 0
$$
onde $Y(s) = \mathcal{L}[y]$. Substituindo $y(0)$ e $y'(0)$ e resolvendo para $Y(s)$:
$$
Y(s) = \frac{s-1}{s^2-s-2} = \frac{s-1}{(s-2)(s+1)}
$$
Obtivemos a expressão para a transformada de Laplace da função $y$, $Y(s) = \mathcal{L}[y]$. Agora devemos encontrar a função cuja transformada é $Y$. 
Expandindo a expressão encontrada em frações parciais:
$$
Y(s) = \frac{s-1}{(s-2)(s+1)} = \frac{a}{s-2} + \frac{b}{s+1} = \frac{a(s+1)+b(s-2)}{(s-2)(s+1)}
$$
para encontrar os coeficientes $a$ e $b$:
$$
s-1 = a(s+1) + b(s-2)
$$
que é uma equação que deve ser satisfeita para todos os valores de $s$. Fazendo $s=2$, encotra-se $a= \frac{1}{3}$. Se $s=-1$, então $b=\frac{2}{3}$. Substituindo, temos:
$$
Y(s) = \frac{1/3}{s-2} + \frac{2/3}{s+1}
$$
Usando as Transformadas encontradas anteriormente, temos que:
$$
\begin{gather}

\mathcal{L}[\frac{1}{3} e^{2t}] = \frac{1/3}{s-2} \\
\mathcal{L}[\frac{2}{3} e^{-t}] = \frac{2/3}{s+1}

\end{gather}
$$
Portanto, pela linearidade da Transformada:
$$
y(t) = \phi(t) = \frac{1}{3} e^{2t} + \frac{2}{3} e^{-t}
$$

### Solução de equações lineares gerais de segunda ordem com coeficientes constantes
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
Agora é só *inverter a transformada* $Y(s)$ para encontrar $\phi(t)$.


#### Tabela de algumas Transformadas de Laplace
![[Pasted image 20240527075337.png]]
## Séries
#### Revisão de Séries de Potências
Uma série de potências $\sum_{n=0}^{\infty} a_n (x-x_0)^n$ converge em um ponto $x$ se o limite
$$
\lim_{m \rightarrow 0} \sum_{n=0}^{m} a_n (x-x_0)^n
$$
existe. A série $\sum_{n=0}^{\infty} a_n (x-x_0)^n$ converge *absolutamente* em um ponto $x$ se a série
$$
\sum_{n=0}^{\infty} | a_n (x-x_0)^n | = \sum_{n=0}^{\infty} |a^n| |x-x_0|^n
$$
converge. O teste da razão serve para verificar a convergência absoluta de uma série, com $a_n \neq 0$ e, se para um valor de $x$:
$$
\lim_{n \rightarrow \infty} \left| \frac{a_{n+1} (x-x_0)^{n+1}}{a_n (x-x_0)^n} \right| = |x-x_0| \lim_{n \rightarrow \infty} \left| \frac{a_{n+1}}{a_n} \right| = |x-x_0| L
$$
entäo a serie de potências converge absolutamente naquele valor de $x$ se $|x-x_0|L < 1$ e diverge se $|x-x_0|L > 1$. Se $|x-x_0|L = 1$, o teste nao é conclusivo.
Existe um número não negativo $\rho$, chamado ***raio de convergência***, tal que $\sum_{n=0}^{\infty} a_n (x-x_0)^n$ converge absolutamente para $|x-x_0| < \rho$. Para uma série que converge apenas em $x_0$, define-se $\rho=0$; para uma que converge em todo $x$, $\rho = \infty$. Se $\rho > 0$, o intervalo $|x-x_0| < \rho$ é chamado de intervalo de convergência.

### Série de Taylor
Dada uma função $f(x)$, o valor de $f(x)$ em torno de um ponto $x_0$ pode ser aproximada pela série infinita:
$$
f(x) = \sum_{n=0}^{\infty} \frac{1}{n!} f^{n} (x_0) (x-x_0)
$$
Se o raio de convergência da série é $\rho > 0$ é dita analítica em $x=x_0$.

*Exemplo solução oscilador harmônico*
$$
\begin{gathered}
\frac{d^2 y}{dx^2} + y = 0 \\
\end{gathered}
$$
Consideramos que
$$
y = \sum_{n=0}^{\infty} a_n x^n
$$
Logo,
$$
\begin{align}

\frac{dy}{dx} &= \sum_{n=0}^{\infty} n a_n x^{n-1} \\
&= \sum_{n=1}^{\infty} n a_n x^{n-1}

\end{align}
$$
e pra derivada segunda:
$$
\begin{align}

\frac{d^2 y}{dx^2} &= \sum_{n=1}^{\infty} n (n-1) a_n x^{n-2} \\
&= \sum_{n=2}^{\infty} n (n-1) a_n x^{n-2}

\end{align}
$$
Substituindo na e.d.o. do oscilador harmônico:
$$
\begin{gather}

\sum_{n=2}^{\infty}{n(n-1) a_n x^{n-2}} + \sum_{n=0}^{\infty} a_n x^n = 0 \\

\sum_{n=0}^{\infty}{(n+2)(n+1)a_{n+2} x^n} + \sum_{n=0}^{\infty}{a_n x^n} = 0 \\

\sum_{n=0}^{\infty}[(n+2)(n+1) a_{n+2} + a_n]x^n = 0


\end{gather}
$$
Como uma solução em série tem que valer pra todo x em um intervalo onde a série converge, segue que os coeficientes de cada $x^n$ têm que se anular:
$$
a_{n+2} = - \frac{a_n}{(n+2)(n+1)}
$$
Então vemos que:
$$
\begin{gather}

a_2 = - \frac{a_0}{2.1} = -\frac{a_0}{2!} \\
a_3 = - \frac{a_1}{3!} \\
a_4 = - \frac{a_2}{4.3} = \frac{a_0}{4!} \\
a_5 = - \frac{a_3}{5.4} = \frac{a_1}{5!}

\end{gather}
$$
Logo, a solução pode ser escrita como:
$$
y = a_0 \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n)!}x^{2n} + a_1 \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)!} x^{2n+1}
$$
Onde $a_0$ e $a_1$ são constantes arbitrárias. Nota-se que há duas soluções linearmente independentes, que correspondem às séries de Taylor da função $\cos{x}$ e $\sin{x}$, respectivamente:
$$
\begin{gather}

y_1 \equiv \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n)!}x^{2n} = \cos{x} \\
\\

y_2 \equiv \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)!} x^{2n+1} = \sin{x}

\end{gather}
$$

### Solução em série em de potências em torno de um ponto ordinário
Considerando uma e.d.o. da seguinte forma:
$$
P(x) \frac{d^2 y}{dx^2} + Q(x) \frac{dy}{dx} + R(x) y = 0
$$
com condições iniciais $y(x_0) = y_0$ e $y^{(1)} (x_0) = y'_0$.
Suponha que, em torno de um *ponto ordinário* $x_0$ temos:
$$
\begin{gather}
p(x) = \frac{Q(x)}{P(x)} \\
q(x) = \frac{R(x)}{P(x)}
\end{gather}
$$
Sendo $p, q$ duas funções analíticas, ou seja, as séries de Taylor para $p$ e $q$ existem em um intervalo em torno de $x_0$. No entanto, se pelo menos uma destas funções não for analítica no ponto $x_0$, então este ponto é dito singular. Supondo $x_0$ ordinário, podemos escrever:
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
onde $y_1$ e $y_2$ são duas séries de potências que também convergem em torno de $x_0$ e formam um conjunto fundamental de soluções.

### Solução em série em torno de um ponto singular regular

***O que é ponto singular***
Dada uma e.d.o. da forma:
$$
P(x)y'' + Q(x)y' + R(x)y = 0
$$
Um ponto $x_0$ tal que $P(x_0) = 0$ e pelo menos um entre $Q(x)$ e $R(x)$ não se anula em $x_0$ é chamado de ponto singular.

Supondo um ponto singular regular em $x_0$ e escolhemos o sistema em que a origem escolhida é o próprio $x_0$, ou seja, $x_0 = 0$. Um ponto singular em $x_0=0$ é dito regular quando, dada a e.d.o. da forma
$$
\frac{d^2 y}{dx^2} + p(x) \frac{dy}{dx} + q(x)y = 0
$$
vale:
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
Supondo que $p_0 \neq 0$ e $q_0 \neq 0$. Como estamos interessados em soluções para $x > 0$ próximas de $x_0 = 0$, vemos que $x << 1$ e a e.d.o. se aproxima da chamada **Equação de Euler**:
$$
x^2 \frac{d^2 y}{dx^2} + x p_0 \frac{dy}{dx} + q_0 y = 0
$$
Quando chega numa equação na forma de uma Equação de Euler, supõe-se uma solução da forma:
$$
y=x^r (a_0 + a_1 x + a_2 x^2 + ...) = \sum_{n=0}^{\infty} a_n x^{r+n}
$$
que fica fácil de encontrar uma relação, saindo dessa, para $y'$ e $y''$. 
Usando essa suposição, encontra-se uma equação no meio da solução que é da forma de exemplo:
$$
2r(r-1) - r+1 = 0
$$
que é chamada de ***equação indicial (indicial equation)***, que sai dos exponentes de cada $x^{r+n}$ e de seus coeficientes. As raízes dessa equação são chamadas de ***expoentes na singularidade*** para o ponto singular regular $x_0$. Eles determinam o comportamento qualitativo da solução $y=x^r$ nas proximidades do ponto $x_0$.


***Solução da Equação de Euler***:
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
\begin{align}

x^{\lambda + i \mu} = e^{(\lambda + i \mu)\ln{x}} &= e^{\lambda \ln{x}} e^{i\mu \ln{x}} = x^{\lambda} e^{i \mu \ln{x}} \\

&= x^{\lambda} [\cos{(\mu \ln{x})} + i \sin{(\mu \ln{x})}]

\end{align}
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
