## Provas e datas
1. **P1**: 18/04
2. **P2**: 20/06

## Integrais de Múltiplas Variáveis
### Integrais iteradas
Dada uma função $F: [c,d] \to \mathbb{R}$ dada por
$$F(y) = \int^{b}_{a} f(x,y)dx$$
é contínua. Supondo ainda que $f(x,y)$ seja contínua num retângulo $R$, $a \leq x \leq b$, $c \leq y \leq d$. Logo, a integral de Riemann do tipo:
$$\int^{d}_{c} F(y)dy = \int^{d}_{c} \left[ \int^{b}_{a} f(x,y) dx \right] dy$$
é chamada de *integral iterada* e, quando $f \gt = 0$, representa o volume sob o gráfico de $f$.
A região de integrais iteradas não precisa necessariamente ser um retângulo, por exemplo:

![[Pasted image 20240326072237.png]]
Na figura 1, temos:
$$
\int_{a}^{b} \int_{g_1 (x)}^{g_{2}(x)} f(x,y) dy dx
$$
em (2), temos:
$$
\int_{c}^{d} \int^{h_2 (y)}_{h_1 (y)} f(x,y) dx dy
$$

### Integrais múltiplas
Seja $B$ uma região tal que exista $f : B \subset \mathbb{R}^{n} \rightarrow \mathbb{R}$, e $B$ é um subconjunto limitado e $f$ é limitada sobre $B$. A *integral de $f$ sobre $B$* é:
$$
\int_{B} fdv
$$
onde $dv$ é o elemento de volume ($dv = dxdy, \ dv = dxdydz...$) dependendo do $\mathbb{R}^n$. Exemplo:
$$
\begin{aligned}
\int_{B} fdA = \int_B f(x,y)dxdy, \ &n=2 \\
\int_{B} f(x,y,z) dx dy dz, \ &n=3 \\
\int_B f(x_1, ..., x_n)dx_1,...,dx_n
\end{aligned}
$$

A interpretação geométrica da integral dupla $\int_B f(x,y)dxdy$ supõe $f$ positiva e contínua sobre $B$. Assim, o gráfico de $f$ é uma superfície que está acima do plano $xy$, pois $z = f(x,y)$. A soma de Riemann (e portanto a integral) é a soma dos volumes dos paralelepípedos cujas bases são os retângulos determinados pela rede ($xy$) e cujas alturas correspondentes são os valores $f(x_i, y_i)$. Quando a malha da rede tende a zero, os "mini-retângulos" se aproximam cada vez mais da superfície e a soma se aproxima do *volume do sólido S*, delimitado pelo domínio $B$. Definimos então:
$$
V(S) = \int_B f(x,y)dxdy
$$
![[Pasted image 20240326074158.png]]


### Regra geral para resolver integrais múltiplas
Para estabelecer os limites, escolhemos primeiro as variáveis externa, imediata e interna. Nesse exemplo são $y$, $x$ e $z$, respectivamente.
#### Primeira etapa:
Achar os valores extremos da variável externa. Por exemplo:
$$
\int_a^b dy \int dx \int f(x,y,z)dz
$$
#### Segunda etapa:
Fixe a variável externa num determinado valor, determinando um corte na região de $S$. Determine os valores extremos da variável imediata neste corte. Por exemplo:
$$
\int_a^b \int_{g(y)}^{h(y)} dx \int f(x,y,z) dz
$$
#### Terceira etapa:
Fixe agora, neste corte, a variável imediata, obtendo um segmento de reta. Determine os valores extremos da variável interna. Por exemplo:
$$
\int_a^b \int_{g(y)}^{h(y)} dx \int_{l(x,y)}^{S(x,y)} f(x,y,z) dz
$$
![[Pasted image 20240326075057.png]]


## Mudança de variáveis
Em integrais simples (1-dimensionais), a mudança de variáveis é dada por:
$$
\int_{\phi(a)}^{\phi(b)} f(x)dx = \int_{a}^{b} f(\phi(u)) \phi'(u) du, \ x=\phi(u)
$$
Num espaço n-dimensional, uma troca de variáveis é feita por uma transformação $U^n \xrightarrow{T} \mathbb{R}^n$. Ou também: $T(u) = x$, onde $u \in U^{n}$ e $x \in \mathbb{R}^n$. Consideramos $U^n$ uma cópia de $\mathbb{R}^n$.

Assim, sendo $B$ uma região e subconjunto limitado de $U^n$ e uma caralhada de coisa de matemático, temos que:
$$
\int_{T(B)} f dv = \int_B (f \circ T) \cdot |\det J(T)| dv
$$
![[Pasted image 20240326194620.png]]
Onde $J(T)$ é a Matriz Jacobiana da transformação $T$. A matriz Jacobiana de uma função $T(x_1, ..., x_n) = (T_1(x_1), ..., T_m(x_n))$ é dada por


# Integral de Linha
## De função escalar
Se uma curva $C$ é parametrizada por uma função vetorial $\vec{r}(t)$ para $t \in [a,b]$, a integral de linha de uma função escalar $f$ sobre a curva $C$ é dada por:
$$
\int_C f \ ds = \int_a^b f(\vec{r}(t)) \ |\vec{r}'(t)| \ dt
$$
OBS: o termo $ds$ representa uma variação infinitesimal do comprimento da curva $C$. Para calculá-lo, digamos que a função $\vec{r}(t)$ que parametriza a curva $C$ seja dada por $\vec{r}(t) = (x(t), y(t))$, então o valor de $ds$ é a norma da variação dessa função:
$$
ds = || (x'(t)dt, y'(t)dt) || = \sqrt{dx^2 + dy^2}
$$
![[Pasted image 20240606114443.png]]
A curva azul na imagem seria a curva $C$ descrita por $\vec{r}(t)$.



## De função vetorial
Supondo uma função vetorial $\vec{F}: \Omega \rightarrow \mathbb{R}^3$  que é um campo de forças definido no conjunto $\Omega \subset \mathbb{R}^3$ e que essa função descreva a força sobre uma partícula, cujo movimento é descrito em $\Omega$ por $\gamma(t): [a,b] \rightarrow \Omega$ ($\gamma(t)$ é a posição da partícula no instante $t$). Se $\vec{F}$ for constante, o trabalho realizado por $\vec{F}$ sobre a partícula durante o intervalo de tempo $\Delta t = b-a$ é:
$$
W = \vec{F} \cdot [\gamma(b) - \gamma(a)] = || \vec{F} || \ || \gamma(b) - \gamma(a) || \ \cos{\theta}
$$
Agora supondo que $\vec{F}$ é contínua (não constante) e depende da posição $\gamma(t)$ da partícula, e $\gamma$ tem pelo menos derivada de primeira ordem. O trabalho $W$ agora então passa a ser uma integral:
$$
W = \int_{a}^{b} \vec{F}(\gamma(t)) \cdot \gamma'(t) dt = \int_\gamma \vec{F} \cdot d\gamma
$$
onde $\int_\gamma \vec{F}$ é uma notação para indicar a integral $\int_a^b \vec{F}(\gamma(t)) \cdot \gamma'(t) dt$. 

Considerando agora um campo vetorial contínuo qualquer $\vec{F}: \Omega \subset \mathbb{R}^n \rightarrow \mathbb{R}^n$, e uma curva $\gamma \ : [a,b] \rightarrow \Omega$ de classe $C_1$. Então definimos ***a integral de linha de $\vec{F}$ sobre $\gamma$ por***:
$$
\int_\gamma \vec{F} \cdot d\gamma = \int_a^b \vec{F}(\gamma(t)) \cdot \gamma'(t)dt
$$
também é comum utilizar a notação:
$$
\int_\gamma \vec{F} \cdot d \vec{r}
$$
onde $\vec{r}(t) = \gamma(t)$.

***Outra notação***:
Seja $\vec{F}(x,y) = P(x,y)\hat{i} + Q(x,y)\hat{j}$ um campo vetorial contínuo em $\Omega \subset \mathbb{R}^2$ e seja $\gamma \ : [a,b] \rightarrow \Omega$ uma curva de classe $C_1$ dada por $\gamma(t)=(x(t),y(t))$. Então:
$$
\int_\gamma \vec{F} \cdot d\vec{r} = \int_\gamma P(x,y)dx + Q(x,y)dy = \int_a^b \left[ P(x(t), y(t)) \frac{dx}{dt} + Q(x(t),y(t)) \frac{dy}{dt} \right] dt
$$


## Integral de linha em em relação a $x$ ou $y$ (ou $z$)
Considerando ainda a função $\gamma : [a, b] \rightarrow \Omega$, $\gamma(t) = (x(t), y(t))$, então a integral de linha da função $f(x,y)$ sobre $\gamma$ em relação a $x$ é:
$$
\int_\gamma f(x,y) dx = \int_a^b f(x(t),y(t)) \ x'(t) \ dt
$$
e é da mesma forma quando for em relação a $y$:
$$
\int_\gamma f(x,y) dy = \int_a^b f(x(t), y(t)) \ y'(t) dt
$$



## Mudança de Parâmetro
Sejam $\gamma_1 : [a,b] \rightarrow \mathbb{R}^n$ e $\gamma_2 : [c,d] \rightarrow \mathbb{R}^n$ duas curvas com derivadas de primeira ordem.  Supondo que exista uma função $g : [c,d] \rightarrow \mathbb{R}$, também derivável, com $g'(u) > 0$ em $(c,d)$ e $Im \ g = [a,b]$, tal que, pra todo $u \in [c,d]$ :
$$
\gamma_2(u) = \gamma_1 (g(u))
$$
Dizemos que $\gamma_2$ é obtida de $\gamma_1$ por uma mudança de parâmetro que conserva a orientação.
![[Pasted image 20240606173159.png]]

Se a condição $g'(u) > 0$ for substituída por $g'(u) < 0$, então dizemos que $\gamma_2$ é obtida de $\gamma_1$ por uma mudança de parâmetro que reverte a orientação.

Junções do teorema:
- Se $\gamma_2$ for obtida de $\gamma_1$ por uma mudança de parâmetro que *conserva a orientação* então:
$$
\int_{\gamma_{1}} \vec{F} \cdot d\gamma_1 = \int_{\gamma_{2}} \vec{F} \cdot d\gamma_2
$$
- Se $\gamma_2$ for obtida de $\gamma_1$ por uma mudança de parâmetro que *reverte a orientação* então:
$$
\int_{\gamma_1} \vec{F} \cdot d \gamma_1 = - \int_{\gamma_2} \vec{F} \cdot \gamma_2
$$

## Integral de linha sobre uma curva por partes
Uma curva $\gamma : [a,b] \rightarrow \mathbb{R}^n$ se diz por partes se for contínua e existirem uma partição $a = t_0 < t_1 < ... < t_n = b$ e curvas $\gamma_i : [t_{i-1}, t_i] \rightarrow \mathbb{R}^n, i = 1,2,...,n$ tais que, para todo $t \in [a, b]$, $\gamma(t) = \gamma_i(t)$. Ou seja, é a curva $\gamma : [a,b]$ cortada em pequenas partes $\gamma_1 : [t_0, t_1], \gamma_2 : [t_1, t_2], ..., \gamma_n : [t_{n-1}, t_n]$.

Seja $\vec{F} : \Omega \subset \mathbb{R}^n$ um campo vetorial e seja $\gamma : [a,b] \rightarrow \Omega$ uma curva por partes, então:
$$
\int_\gamma \vec{F} \cdot d\gamma = \int_{\gamma_1} \vec{F} \cdot d \gamma_1 + \int_{\gamma_2} \vec{F} \cdot d \gamma_2 + ... + \int_{\gamma_n} \vec{F} \cdot d \gamma_n
$$
![[Pasted image 20240606174453.png]]


# Campos Conservativos
Um campo vetorial $\vec{F} : \Omega \subset \mathbb{R}^n \rightarrow \mathbb{R}^n$ denomina-se *conservativo* se existe um campo escalar diferenciável $\phi : \Omega \rightarrow \mathbb{R}$ tal que:
$$
\nabla \phi = \vec{F}
$$
A função $\phi$ que satisfaz essa condição é denominada *função potencial de $\vec{F}$*. 

Uma condição *necessária*, mas *não suficiente*, para que $\vec{F}$ seja conservativo é que o rotacional de $\vec{F}$ seja nulo ($\mathrm{rot} \ \vec{F} = \vec{O}$).

***Rotacional***
*OBS*: Rotacional é um operador que calcula, em uma superfície infinitesimal, o quanto os vetores de um campo vetorial se afastam ou se aproximam de um vetor normal a esta superfície (em outras palavras, calcula o quanto esse campo "roda"). 
Dado um campo vetorial $\vec{F}(x, y, z) = (F_x, F_y, F_z)$, seu rotacional será:
$$
\vec{\nabla} \times \vec{F} = \left| \begin{array} \hat{i} & \hat{j} & \hat{k} \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ F_x & F_y & F_z \end{array} \right| = \mathrm{rot} \ \vec{F}
$$
## Forma diferencial exata
Considerando $\vec{F}(x,y) = P(x,y) \hat{i}  + Q(x,y) \hat{j}$ vimos que:
$$
\int_\gamma \vec{F} \cdot dr = \int_\gamma P(x,y)dx + Q(x,y)dy
$$
A forma $P(x,y)dx + Q(x,y)dy$ será *diferencial exata* se existir uma função diferenciável $\phi$ tal que:
$$
\frac{\partial \phi}{\partial x} = P, \frac{\partial \phi}{\partial y} = Q
$$
em outras palavras, $\phi$ é uma primitiva da forma $P(x,y)dx + Q(x,y)dy$.

Assim, sendo $\phi$ uma função diferenciável, lembramos que a diferencial $d\phi$ no ponto $(x,y)$ é dada por:
$$
d \phi = \frac{\partial \phi}{\partial x} (x,y) dx + \frac{\partial \phi}{\partial y} (x,y) dy
$$
Portanto, dizer que a forma $P(x,y)dx + Q(x,y)dy$ é uma forma *diferencial exata* é equivalente a dizer que existe um campo escalar diferenciável $\phi : \Omega \rightarrow \mathbb{R}$ tal que, em todo $(x,y) \in \Omega$, a diferencial de $\phi$ é dada por:
$$
d \phi = P(x,y) dx + Q(x,y)dy
$$
Nota-se que para existir $\phi$, o campo vetorial $\vec{F}$ deve ser conservativo. 

Segue que uma condição para $P(x,y)dx + Q(x,y)dy$ ser exata é que:
$$
\frac{\partial P}{\partial y} = \frac{\partial Q}{\partial x}
$$

## Integral de linha de um campo conservativo
Se $\vec{F} : \Omega \subset \mathbb{R}^n \rightarrow \mathbb{R}^n$ for um campo vetorial conservativo e se $\phi : \Omega \rightarrow \mathbb{R}$ for uma função potencial para $\vec{F}$ ($\nabla \phi = \vec{F}$), e a curva for $\gamma : [a,b] \rightarrow \Omega$ então:
$$
\int_\gamma \vec{F} \cdot d\gamma = \int_\gamma \nabla \phi \cdot d\gamma = \phi(B) - \phi(A) = \phi(\gamma(b)) - \phi(\gamma(a))
$$

Se $\vec{F}$ for de tal forma que $\vec{F} = P(x,y)\hat{i} + Q(x,y)\hat{j}$, teremos que, se a forma $P(x,y)dx + Q(x,y)dy$ for exata, com primitiva $\phi$ ($d \phi = P(x,y)dx + Q(x,y)dy$), teremos:
$$
\int_\gamma P(x,y) dx + Q(x,y) dy = \int_\gamma d\phi = \phi(B) - \phi(A)
$$
Se $\vec{F}$ for um campo conservativo e a curva $\gamma : [a,b] \rightarrow \Omega$ for por partes, ligando o ponto $A = \gamma(a)$ ao ponto $B = \gamma(b)$, teremos:
$$
\int_\gamma \vec{F} \cdot d \vec{r} = \phi(B) - \phi(A)
$$
ou seja, o valor da integral de linha de $\vec{F}$ não depende da curva que liga $A$ a $B$, apenas dos pontos inicial e final. Nesse caso, vale também a notação:
$$
\int_A^B \vec{F} \cdot d\vec{r}
$$

***Teorema da existência de função potencial***: Seja $\vec{F} : \Omega \subset \mathbb{R}^n \rightarrow \mathbb{R}^n$ um campo vetorial contínuo. Supondo que $\int_\gamma \vec{F} \cdot d \vec{r}$ seja independente do caminho de integração em $\Omega$, e assumindo $A \in \Omega$ como ponto inicial, então a função $\phi : \Omega \rightarrow \mathbb{R}$ dada por:
$$
\phi(X) = \int_A^X \vec{F} \cdot d \gamma
$$
é tal que $\nabla \phi = \vec{F}$ em $\Omega$.

## Condições necessárias e suficientes para um campo vetorial ser conservativo
Seja $\vec{F} : \Omega \subset \mathbb{R}^n \rightarrow \mathbb{R}^n$ um campo vetorial contínuo no aberto conexo por caminhos $\Omega$. Se $\vec{F}$ é conservativo, então são equivalentes as afirmações:
- $\vec{F}$ é conservativo
- $\oint_\gamma \vec{F} \cdot d\gamma = 0$ para toda curva $\gamma$, fechada.
- $\int_\gamma \vec{F} \cdot d\vec{r}$ é independente do caminho de integração.
*OBS*: $\oint_\gamma$ é a integral de linha sobre a curva FECHADA $\gamma$.

***Teorema de condição para um campo com rotacional zero ser conservativo:*** Seja $\Omega$ um aberto do $\mathbb{R}^2$ tal que existe um ponto $(x_0, y_0) \in \Omega$ tal que, pra todo $(x,y) \in \Omega$, a poligonal de vértices $(x_0, y_0), (x_0, y)$ e $(x,y)$ está contida em $\Omega$. Nestas condições, se $\mathrm{rot} \ \vec{F} = \vec{0}$, então $\vec{F}$ será conservativo.

# Teorema de Green
Seja $K \subset \mathbb{R}^2$ um compacto, com interior não vazio, cuja fronteira é imagem de uma curva $\gamma : [a,b] \rightarrow \mathbb{R}^2$, fechada, simples, classe $C_1$ e por partes e orientada no sentido anti-horário. Sejam $P$ e $Q$ funções deriváveis, então:
$$
\oint_\gamma P \ dx + Q \ dy = \iint_K \left[ \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right] dx dy
$$
![[Pasted image 20240610072307.png]]

## Teorema de Stokes no plano
Consequência do Teorema de Green. Seja $\vec{F} = P \vec{i} + Q \vec{j}$ um campo vetorial no aberto $\Omega \subset \mathbb{R}^2$ e sejam $\gamma$ e $K$ como no teorema de Green. Como vale que:
$$
\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = (\mathrm{rot} \ \vec{F}) \cdot \vec{k}
$$
ou seja:
$$
\oint_\gamma P \ dx + Q \ dy = \iint_K \mathrm{rot} \ \vec{F} \cdot \vec{k} \ dx \ dy
$$
lembrando que esta integral fechada é sempre com $\gamma$ no sentido anti-horário.

## Fluxo
Seja $\gamma : [a,b] \rightarrow \mathbb{R}^2$ uma curva tal que, para todo $t \in (a,b), \gamma'(t) \neq \vec{0}$. Então $\gamma$ é regular.

Supondo uma curva descrita por $\gamma(t) = (x(t), y(t)), t \in [a,b]$ que seja regular. Consideramos o vetor $\vec{n}$ dado por:
$$
\vec{n}(\gamma(t)) = \frac{1}{|| \gamma'(t)||} (y'(t) \vec{i} - x'(t)\vec{j})
$$
que é um vetor normal a $\gamma'(t)$, ou seja, $\vec{n}$ associa, a cada ponto $\gamma(t)$ da imagem de $\gamma$, um vetor unitário e normal a $\gamma$ no ponto $\gamma(t)$.
Seja $\vec{F}(x,y)$ um campo vetorial. Seja $F_n = \vec{F} \cdot \vec{n}$ a função de valores reais dada por:
$$
F_n(\gamma(t)) = \vec{F}(\gamma(t)) \cdot \vec{n}(\gamma(t))
$$
A função $F_n(\gamma(t))$ é a componente escalar de $\vec{F}(\gamma(t))$ na direção $\vec{n}(\gamma(t))$ no ponto $\gamma(t)$. Dessa forma, definimos o ***fluxo*** de $\vec{F}$ através de $\gamma$, na direção $\vec{n}$, por:  
$$
\int_\gamma \vec{F} \cdot \vec{n} \ ds = \int_a^b \vec{F}(\gamma(t)) \cdot \vec{n}(\gamma(t)) \ || \gamma'(t) || \ dt
$$
Referimos a $\vec{n}(\gamma(t))$ como a *normal exterior* a $K$.
![[Pasted image 20240611073804.png]]

## Teorema da divergência no plano
Seja $\vec{F} = P \vec{i} + Q \vec{j}$ um campo vetorial num aberto $\Omega \subset \mathbb{R}^n$ e seja $K$ uma região compacta com interior não vazio cuja fronteira é a imagem de $\gamma(t) = (x(t), y(t))$, regular e orientada no sentido anti-horário. Seja $\vec{n}$ a normal unitária exterior a $K$, então:
$$
\oint_\gamma \vec{F} \cdot \vec{n} \ ds = \iint_K \mathrm{div} \vec{F} \ dx \ dy
$$
Se a curva $\gamma$ não fechar a região $K$, não tem como usar esse teorema.

***OBS: DIVERGENTE***
O divergente é um operador que mede a magnitude de "fonte" ou "poço/sorvedouro" de um campo vetorial em um dado ponto, ou seja, é como um escalar que mede a dispersão ou divergência dos vetores do campo num determinado ponto (o quanto os vetores se afastam/aproximam). 
Dado um campo vetorial $\vec{F}(x,y,z) = F_x \vec{i} + F_y \vec{j} + F_z \vec{k}$, o seu divergente $\mathrm{div} F$ é:
$$
\mathrm{div} \ F = \nabla \cdot F = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}
$$




# Área e Integral de Superfície
## Superfície Parametrizada
Uma superfície parametrizada $\sigma$ é uma transformação $\phi : A \rightarrow \mathbb{R}^3$ onde $A \subset \mathbb{R}^2$. Supondo que as componentes de $\sigma$ sejam dadas por $x = x(u,v), y = y(u,v), z = z(u,v)$, então $\sigma(u,v) = (x(u,v), y(u,v), z(u,v))$. 
O lugar geométrico descrito por $\sigma(u,v)$ é a *imagem* de $\sigma$.
![[Pasted image 20240611075645.png]]

***Algumas parametrizações de superfícies***:
![[Pasted image 20240611102857.png]]
***Parametrização de Cilindros***:
Para um cilindro de raio $r$, temos $\sigma(u,v) = (x,y,z)$:
$$
\begin{cases}
x = r \cos{u} \\
y = r \sin{u} \\
z = v
\end{cases}
$$
com $0 \leq u \leq 2\pi$ e $0 \leq v \leq h$, onde $h$ é a altura do cilindro desejado.
![[Pasted image 20240611103418.png]]
***Parametrização de esfera***:
Para uma esfera de raio $r$, temos $\sigma(\theta, \phi) = (x,y,z)$:
$$
\begin{cases}
x = r \sin{\phi} \cos{\theta} \\
y = r \sin{\phi} \sin{\theta} \\
z = r \cos{\phi}
\end{cases}
$$
com $0 \leq \theta \leq 2\pi$ e $0 \leq \phi \leq \pi$.

## Plano Tangente
Dada uma superfície parametrizada $\sigma : \Omega \subset \mathbb{R}^2 \rightarrow \mathbb{R}^3$ e seja $(u_0, v_0)$ um ponto de $\Omega$. Se $\frac{\partial \sigma}{\partial v}(u_0, v_0) \neq \vec{0}$, então $\frac{\partial \sigma}{\partial v}(u_0, v_0)$ será um vetor tangente a esta curva no ponto $\sigma(u_0, v_0)$. De modo análogo, se $\frac{\partial \sigma}{\partial u}(u_0, v_0) \neq \vec{0}$, então $\frac{\partial \sigma}{\partial u}(u_0, v_0)$ também será um vetor tangente no mesmo ponto.
O plano tangente à superfície $\sigma$ no ponto $(x_0, y_0, z_0) = \sigma(u_0, v_0)$ tem por equação:
$$
(x,y,z) = \sigma(u_0, v_0) + s \frac{\partial \sigma}{\partial u}(u_0, v_0) + t \frac{\partial \sigma}{\partial t}(u_0, v_0)
$$

## Área de superfície
Seja $\sigma : K \rightarrow \mathbb{R}^3$, onde $K$ é um compacto com fronteira de conteúdo nulo e interior não vazio. A área de uma superfície parametrizada $\sigma(u,v)$ é dada por:
$$
A_\sigma = \iint_K \left|\left| \frac{\partial \sigma}{\partial u} \times \frac{\partial \sigma}{\partial v} \right|\right| \ du \ dv
$$
![[Pasted image 20240611080951.png]]

## Integral de superfície
Seja $K$ um compacto de $\mathbb{R}^2$. Seja $\sigma: K \rightarrow \mathbb{R}^3$ uma superfície parametrizada. Seja $f(x,y,z)$ uma função a valores reais definida e contínua na imagem de $\sigma$. Definimos a integral de superfície de $f$ sobre $\sigma$ por:
$$
\iint_\sigma f(x,y,z) \ dS = \iint_K f(\sigma(u,v)) \left|\left| \frac{\partial \sigma}{\partial u} \times \frac{\partial \sigma}{\partial v} \right|\right| \ du \ dv
$$
onde $dS = \left|\left| \frac{\partial \sigma}{\partial u} \times \frac{\partial \sigma}{\partial v} \right|\right| \ du \ dv$ é o elemento de área.

No caso de $f(x,y,z) = 1$, para todo $(x,y,z) \in \mathrm{Im} \ \sigma$, temos:
$$
\iint_\sigma f(x,y,z) \ dS = \iint_\sigma dS = A_\sigma
$$
que é a integral da área de $\sigma$.

# Teorema de Gauss
## Fluxo de um campo vetorial
Seja $\sigma : K \subset \mathbb{R}^2 \rightarrow \mathbb{R}^3$, onde $K$ é uma região fechada com interior não vazio. Considerando os campos vetoriais $\vec{n}_1$ e $\vec{n}_2$ dados por:
$$
\begin{gather}
\vec{n}_1 (\sigma(u,v)) = \frac{ \frac{\partial \sigma}{\partial u}(u,v) \times \frac{\partial \sigma}{\partial v}(u,v) }{ \left|\left| \frac{\partial \sigma}{\partial u}(u,v) \times \frac{\partial \sigma}{\partial v}(u,v) \right|\right| }, (u,v) \in K \\
\vec{n}_2 (\sigma(u,v)) = - \vec{n}_1 (\sigma(u,v))
\end{gather}
$$
O campo $\vec{n}_1$ associa a cada ponto $\sigma(u,v)$ um vetor unitário e normal a $\sigma$ e aponta para o lado externo ($\vec{n}_2$ para o interno). 

Assim, seja $\vec{F} : \mathrm{Im} \ \sigma \rightarrow \mathbb{R}^3$ um campo vetorial contínuo. Denomina-se *fluxo de $\vec{F}$ através de $\sigma$, na direção $\vec{n}$* a integral:
$$
\iint_\sigma \vec{F} \cdot \vec{n} \ dS = \iint_K \vec{F}(\sigma(u,v)) \cdot \vec{n}(\sigma(u,v)) \left|\left| \frac{\partial \sigma}{\partial u}(u,v) \times \frac{\partial \sigma}{\partial v}(u,v) \right|\right| \ du \ dv
$$
Também é comum usar a notação:
$$
\iint_\sigma \vec{F} \cdot \vec{dS}, \ \vec{dS} = \vec{n} \ dS
$$

## Teorema da Divergência ou de Gauss
Seja $B \in \mathbb{R}^3$ uma região, com interior não vazio, cuja fronteira coincide com a imagem de uma cadeia $\sigma = (\sigma_1, \sigma_2, ..., \sigma_m)$. Suponhamos que, para cada índice $i$, seja possível escolher um vetor unitário normal $\vec{n}_i$ a $\sigma_i$, com $\vec{n}_i$ apontando para fora de $B$. Seja $\vec{n}$ um campo vetorial definido na fronteira de $B$ e que coincide com $\vec{n}_i$ sobre $\sigma_i$. Seja $\vec{F} = P \vec{i} + Q \vec{j} + R \vec{k}$ definido num aberto contendo $B$. Assim, é válida a relação:
$$
\iint_\sigma \vec{F} \cdot \vec{n} \ dS = \iiint_B \mathrm{div} \ \vec{F} \ dx \ dy \ dz
$$

# Teorema de Stokes no espaço
Seja $\sigma : K \rightarrow \mathbb{R}^3$ uma porção de superfície regular dada por $\sigma(u,v) = (x(u,v), y(u,v), z(u,v))$. Seja $\vec{F} = P \vec{i} + Q \vec{j} + R \vec{k}$ um campo vetorial num aberto que contém $\mathrm{Im} \ \sigma$. Assim, tem-se:
$$
\int_\Gamma \vec{F} \cdot \vec{dr} = \iint_\sigma (\mathrm{rot} \ \vec{F}) \cdot \vec{n} \ dS
$$
onde $\Gamma$ é uma curva fronteira de $\sigma$ orientada positivamente em relação à normal $\vec{n}$:
$$
\vec{n} = \frac{ \frac{\partial \sigma}{\partial u} \times \frac{\partial \sigma}{\partial v} }{ \left|\left| \frac{\partial \sigma}{\partial u} \times \frac{\partial \sigma}{\partial v} \right|\right| }
$$
Segue que $\Gamma(t) = \sigma(\gamma(t))$, onde $\gamma$ é uma curva fechada com imagem igual à fronteira de $K$ e orientada no sentido anti-horário.
