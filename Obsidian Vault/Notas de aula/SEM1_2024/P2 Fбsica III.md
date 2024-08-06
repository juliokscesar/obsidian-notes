# Capacitores 
## Capacitância
$$
C \equiv \frac{Q}{V}
$$
a medida é Faraday (F).
## Capacitor Plano
![[Pasted image 20240603211947.png]]
***Campo Elétrico***:
$$
\vec{E} = \frac{\sigma}{\varepsilon_0}
$$
- $\sigma$ é a densidade de carga: $\sigma = \frac{Q}{A}$
- $A$ é área das placas.

***Diferença de Potencial***:
$$
\begin{gather}
V = Ed \\
V = \frac{\sigma}{\varepsilon_0} d = \frac{Qd}{\varepsilon_0 A}
\end{gather}
$$

***Capacitância***:
$$
\begin{gather}
C = \frac{\varepsilon_0 A}{d}
\end{gather}
$$

## Capacitor Cilíndrico
![[Pasted image 20240603212931.png]]
***Campo Elétrico***:
$$
\begin{gather}
\vec{E}(\vec{\rho}) = E(\rho)\hat{\rho} = \frac{Q}{2 \pi l \rho \varepsilon_0} \hat{\rho}
\end{gather}
$$
- $l$ é o comprimento do cilindro.
***Potencial Elétrico***:
$$
V = \frac{Q}{2 \pi l \varepsilon_0} \ln{\left( \frac{b}{a} \right)}
$$
***Capacitância***:
$$
C = \frac{2 \pi \varepsilon_0 l}{\ln{\left( \frac{b}{a} \right)}}
$$
se $(b-a) \ll a$, então vale também $C \cong \frac{\varepsilon_0 A}{d}$, $A = 2\pi a l$.

## Capacitor Esférico
![[Pasted image 20240603214523.png]]
***Campo Elétrico***:
$$
\vec{E}(\vec{r}) = E(r)\hat{r} = \frac{Q}{4 \pi \varepsilon_0 r^2} \hat{r}
$$
***Diferença de Potencial***:
$$
V = \frac{Q}{4 \pi \varepsilon_0}\left( \frac{R_2 - R_1}{R_1 R_2} \right)
$$
***Capacitância***:
$$
C = 4 \pi \varepsilon_0 \left( \frac{R_1 R_2}{R_2 - R_1} \right)
$$

## Associação de Capacitores:
Em paralelo:
$$
C_{eq} = C_1 + C_2 + ... + C_n
$$
Em série:
$$
\frac{1}{C_{eq}} = \frac{1}{C_1} + \frac{1}{C_2} + ... + \frac{1}{C_n}
$$

### Energia Eletrostática Armazenada
$$
U = \frac{Q^2}{2C} = \frac{1}{2} C V^2 = \frac{1}{2} QV
$$
# Corrente Elétrica
$$
i = \frac{dq}{dt}
$$
## Densidade de Corrente
A densidade de corrente $\vec{j}$ através de uma seção transversal $S$ é:
![[Pasted image 20240603215424.png]]
$$
\begin{gather}
di = \vec{j} \cdot \hat{n} \ dS \\
\oint_S \vec{j} \cdot d\vec{S} = - \frac{dq}{dt}
\end{gather}
$$
- $\hat{n}$ é vetor normal à área
- $\vec{j}$ tem a direção e o sentido do movimento das cargas positivas.

Se é em um meio com densidade volumétrica $\rho$ de cargas:
$$
j = \rho v
$$
- $v$ é a velocidade que as cargas se deslocam

Considerando $n$ portadores de carga $q$, $\rho = nq$:
$$
j = nq v
$$
e se são diferentes grupos de cargas:
$$
j = \sum_i n_i q_i v_i
$$

### Densidade devido à condutividade do meio
$$
j = \sigma E
$$
- $\sigma$ é a condutividade elétrica do meio em $(\ohm m)^{-1}$


# Campo Magnético
## Definição do campo magnético $\vec{B}$:
$$
\vec{F_m} = q\vec{v} \times \vec{B}
$$
- a medida é 1 Tesla (T) = $10^4$ Gauss (G)

## Força de Lorentz (campo elétrico + magnético)
$$
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
$$

## Fluxo de $\vec{B}$
O fluxo $\Phi_B$ de $\vec{B}$ através de uma superfície $S$, com versor normal $\hat{n}$ é:
$$
\Phi_B = \int_S B \cdot \hat{n} \ dS
$$
E tem tb:
$$
\oint_S B \cdot \hat{n} \ dS = 0
$$

## Efeito Hall
É quando tem uma força na corrente elétrica devido a um campo magnético $B$. A força eletromotriz transversal $\varepsilon$ que aparece é:
$$
\varepsilon = \frac{j}{nq} Bd
$$
- $d$ é a largura da barra que passa a corrente elétrica de densidade $j$.


# Lei de Ampère
Para uma circuito fechado $C$ qualquer em que $B$ circula:
$$
\oint_C B \cdot dl = \mu_0 i_{tot}
$$
- $i_{tot}$ é a corrente total que atravessa $C$
- $\mu_0 \equiv 4 \pi \times 10^{-7}$ N/A$^2$ (permeabilidade magnética do vácuo)

Também tem com rotacional pra achar $j$:
$$
\nabla \times B = \mu_0 j
$$


## Campo magnético de um fio retilíneo infinito:
$$
\vec{B}(r) = \frac{\mu_0 i}{2 \pi r} \hat{\phi}
$$
- $r$ é a distância do fio ao ponto; $\vec{r}$ é o vetor que sai do ponto e vai pro fio; $\hat{r}$ é o versor unitário de $\vec{r}$.
- a direção $\hat{\phi}$ é o versor perpendicular ao versor $\hat{r}$ (faz regra da mão direita com arminha e o indicador aponta na direção do $\hat{r}$).

## Campo magnético no eixo de uma espira circular:
É o eixo que passa pelo meio dela.
Tomando $z = 0$ como o centro da espira:
$$
\vec{B}(z) = \frac{\mu_0 i R^2}{2(z^2 + R^2)^{3/2}} \hat{z}
$$
## Campo magnético de uma bobina tororidal:
![[Pasted image 20240603224434.png]]
$$
\begin{gather}
B(r) = \frac{\mu_0 N i}{2 \pi r} \hat{\theta}, a < r < b \\
B(r) = 0, fora \ do \ toroide
\end{gather}
$$
- $N$ é o número de espiras
### Campo magnético no interior de um solenoide infinito:
$$
B = \mu_0 n i 
$$
- $n$ é a densidade de espiras. $n = \frac{N}{l}$, $N$ é o número de espiras e $l$ é o comprimento do solenoide.

