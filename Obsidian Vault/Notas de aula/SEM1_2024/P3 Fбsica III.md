# Lei da Indução
## Fluxo de um campo magnético
Considerando uma espira $C$ de fio condutor (como a da imagem), imersa num campo magnético $\vec{B}$. O fluxo de $\vec{B}$ através da espira é:
$$
\Phi_C = \int_S \vec{B} \cdot \hat{n} \ dS
$$
sendo:
- $S$ a superfície da espira
- $dS$ o elemento de área da superfície $S$. No caso da espira, $dS = 2\pi r dr$.
- $\hat{n}$ o vetor normal à superfície $S$.
![[Pasted image 20240625215216.png]]

## F.e.m. e corrente induzida
A lei de Faraday (lei da indução) associa o fluxo do campo magnético que atravessa a espira com a ==força eletromotriz induzida== nela:
$$
\varepsilon = - \frac{d \Phi_C}{dt}
$$
Assim, assumindo que a espira tem uma resistência $R$, então a ==corrente induzida== $i$ será:
$$
i = - \frac{1}{R} \frac{d \Phi_C}{dt}
$$
O ==sentido== da corrente induzida será aquele em que a corrente gera um campo magnético contrário ao campo $\vec{B}$ que induz essa corrente (lei de Lenz).


## Indutância mútua
![[Pasted image 20240625220803.png]]
Considerando dois solenoides coaxiais (um menor dentro do outro maior) de mesmo comprimento $l$, o menor de raio $R_1$ e $N_1$ espiras, o maior de raio $R_2$ e $N_2$ espiras. Se passa uma corrente $i_1$ pelo solenoide 1 (menor), o campo $\vec{B}_1$ gerado pela corrente é:
$$
\begin{align}
\vec{B}_1 &= \frac{\mu_0 N_1 i_1}{l} \hat{z}, \ 0 \leq r \leq R_1 \\
&= 0, \ r \gt R_1
\end{align}
$$
O fluxo $\Phi_{2(1)}$ produzido por $\vec{B}_1$ sobre as $N_2$ espiras do solenoide 2 é:
$$
\begin{align}
\Phi_{2(1)} &= N_2 \int_{S_2} \vec{B}_1 \cdot \hat{z} \ dS \\
&= N_2 B_1 (\pi R_1^2) \\
&= \frac{\mu_0 N_1 N_2 \pi R_1^2}{l} i_1 \\
&\equiv L_{21} i_1
\end{align}
$$
que se torna uma constante multiplicada pela corrente em 1. Essa constante é chamada de ==indutância mútua== $L$:
$$
L_{21} = \frac{\mu_0 N_1 N_2 \pi R_1^2}{l}
$$
OBS: a indutância mútua é a mesma se a corrente estivesse passando em 2, ou seja:
$$
L_{12} = L_{21}
$$
A medida de indutância mútua é 1 H (Henry).

## Autoindutância
Além de produzir um fluxo magnético sobre o solenoide 2, o solenoide 1 também produz um fluxo sobre ele mesmo:
$$
\begin{gather}
\Phi_{1(1)} = N_1 \int_{S_1} \vec{B}_1 \cdot \hat{z} \ dS = N_1 B_1 (\pi R_1^2) = \frac{\mu_0 N_1^2 \pi R_1^2}{l}i_1 \\
\Phi_{1(1)} \equiv L_{11} i_1 = L_1 i_1
\end{gather}
$$
Onde $L_1$ é chamado de autoindutância do solenoide 1.

Se passa simultaneamente uma corrente $i_1$ pelo solenoide 1 e $i_2$ pelo solenoide 2, os fluxos magnéticos correspondentes através dos solenoides serão:
$$
\begin{gather}
\Phi_1 = L_1 i_1 + L_{12} i_2 \\
\Phi_2 = L_{21} i_1 + L_2 i_2
\end{gather}
$$

## F.e.m induzida em AC
Se passa por um circuito 1 uma corrente alternada $i_1(t)$, então o fluxo em um circuito 2 $\Phi_{2(1)}(t)$ do campo magnético gerado pela corrente também dependerá do tempo. Logo, a f.e.m. induzida no circuito 2 será:
$$
\varepsilon_2 = -\frac{d \Phi_{2(1)}}{dt} = -L_{21} \frac{d i_1}{dt}
$$
Então, no circuito 1, a variação de $i_1(t)$ também produz uma f.e.m devido à autoindutância:
$$
\varepsilon_1 = -L_1 \frac{d i_1}{dt}
$$



# Circuitos

## Leis de Kirchhoff
- 1ª Lei (lei das malhas): A soma de todas as quedas de tensão ao longo de uma malha de um circuito é nula. Formalmente:
![[Pasted image 20240625224202.png]]
Considerando o circuito como o da imagem em que cada retângulo representa um elemento de um circuito $R$, $L$ ou $C$. Se tomamos um contorno $\Gamma$ fechado, temos:
$$
\oint_\Gamma \vec{E} \cdot d\vec{l} = 0
$$
onde, por exemplo,
$$
\int_1^2 \vec{E} \cdot d\vec{l} = -\int_1^2 dV = V_1 - V_2 = - \varepsilon
$$
é a *queda de tensão* entre os pontos 1 e 2. OBS: A queda de tensão é positiva quando vamos de um ponto a outro no sentido da corrente, e negativa caso contrário.

- 2ª Lei (lei dos nós): A soma de todas as correntes que saem de um nó é 0. Formalmente:
![[Pasted image 20240625224630.png]]
Considerando o circuito da imagem, se tomamos uma superfície fechada $S_A$ em torno do nó $A$, temos que, considerando $\vec{j}$ a densidade de corrente:
$$
\oint_{S_A} \vec{j} \cdot d\vec{S} = I_2 + I_3 - I_1 = 0
$$

## Circuito RC
![[Pasted image 20240625224859.png]]
Considerando um capacitor $C$ inicialmente descarregado e ligado a uma bateria de f.e.m $\varepsilon$ em um circuito de resistência $R$, pela 1ª lei de Kirchhoff, temos que a soma das quedas de potencial da bateria, do capacitor e do resistor devem ser 0, ou seja:
$$
RI(t) - \varepsilon + \frac{q(t)}{C} = 0
$$
onde $I(t)$ é a corrente no instante $t$ e $q(t)$ a carga armazenada no capacitor nesse instante.
Como $I(t) = \frac{dq}{dt}$, derivamos a relação e temos a e.do. do circuito RC:
$$
R \frac{dI}{dt} + \frac{I(t)}{C} = 0
$$
Integrando, temos que a solução para a corrente é:
$$
\begin{gather}
I(t) = \frac{\varepsilon}{R} \exp{\left( - \frac{t}{\tau_c} \right)} \\
\tau_c \equiv RC
\end{gather}
$$
onde $\tau_c$ é a constante de tempo do circuito (tempo que leva pra corrente cair a 1/$e$ do valor inicial). 
A corrente $I(t)$ descreve este comportamento:
![[Pasted image 20240625225651.png]]
Caso inicialmente o capacitor estivesse carregado e a bateria fosse removida, o capacitor se descarregaria com a mesma lei exponencial e mesma constante de tempo.


## Circuito RL
![[Pasted image 20240625225810.png]]
Considerando um indutor $L$ em um circuito com resistência $R$ e alimentado por uma bateria de f.e.m $\varepsilon$.
A 1ª lei de Kirchhoff aplicada à esse circuito fica:
$$
RI(t) - \varepsilon + L \frac{dI}{dt} = 0
$$
Integrando, temos que a solução para a corrente nesse circuito é:
$$
\begin{gather}
I(t) = \frac{\varepsilon}{R} \left[ 1 - \exp{\left( - \frac{t}{\tau_L} \right)} \right] \\
\tau_L \equiv \frac{L}{R}
\end{gather}
$$
onde $\tau_L$ é a constante de tempo.
E a corrente descreve o seguinte comportamento:
![[Pasted image 20240625230312.png]]
onde $I_\infty \cong \frac{\varepsilon}{R}$.

## Circuito LC
![[Pasted image 20240625230552.png]]
Considerando o capacitor inicialmente carregado e desprezando qualquer efeito de resistência, a energia do circuito se conserva e temos:
$$
\frac{Q}{C} + L \frac{dI}{dt} = 0
$$
e derivando em relação ao tempo, considerando $\frac{dQ}{dt} = I$:
$$
\begin{gather}
\frac{I}{C} + L \frac{d^2 I}{dt^2} = 0 \\
\frac{d^2 I}{dt^2} + \omega_0^2 I = 0
\end{gather}
$$
onde
$$
\omega_0 = \frac{1}{\sqrt{LC}}
$$
que descreve a ==frequência angular== de oscilações livres nesse circuito.

A solução para $I$ (e de $Q$) é a de um oscilador harmônico:
$$
\begin{gather}
I(t) = A \cos{(\omega_0 t + \phi)} \\
Q(t) = \frac{A}{\omega_0} \sin{(\omega_0 t + \phi)}
\end{gather}
$$
E as constantes arbitrárias $A$ e $\phi$ são:
$$
\begin{gather}
A = \sqrt{I_0^2 + \omega_0^2 Q_0^2} \\
\phi = \arctan{\left( \frac{\omega_0 Q_0}{I_0} \right)}
\end{gather}
$$

A ==energia armazenada no capacitor== no instante $t$ é:
$$
U_C(t) = \frac{Q^2(t)}{2C} = \frac{A^2}{2 \omega_0^2 C} \sin^2{(\omega_0t + \phi) = \frac{1}{2} L A^2 \sin^2(\omega_0 t + \phi)}
$$

A ==energia armazenada no indutor== no instante $t$ é:
$$
U_L(t) = \frac{1}{2} L I^2(t) = \frac{1}{2}L A^2 \cos^2{(\omega_0 t + \phi)}
$$
A ==energia total== é:
$$
U = U_L + U_C = \frac{1}{2} L A^2 = \frac{1}{2} \frac{A^2}{\omega_0^2 C}
$$

## Circuito RLC
![[Pasted image 20240625231855.png]]
Considerando um circuito análogo ao anterior porém levando em conta a resistência $R$ do circuito, temos:
$$
\frac{Q}{C} + RI + L \frac{dI}{dt} = 0
$$
derivando em $t$ e dividindo por $L$ temos:
$$
\begin{gather}
\frac{d^2 I}{dt^2} + \frac{R}{L} \frac{dI}{dt} + \frac{1}{LC}I = 0 \\
\ddot{I} + \gamma \dot{I} + \omega_0^2 I = 0
\end{gather}
$$
que cai em uma e.d.o. de oscilador harmônico amortecido, onde
$$
\begin{gather}
\omega_0 = \frac{1}{\sqrt{LC}} \\
\gamma = \frac{R}{L} \equiv \frac{1}{\tau_L}
\end{gather}
$$
==**Amortecimento subcrítico:**==
No caso em que
$$
\frac{\gamma}{2} \lt \omega_0
$$
temos um amortecimento subcrítico, e a solução para a corrente fica:
$$
\begin{gather}
I(t) = A e^{-\frac{\gamma}{2} t} \cos{(\omega_1 t + \phi)} \\
\omega_1(t) \equiv \sqrt{\omega_0^2 - \frac{\gamma^2}{4}}
\end{gather}
$$
e descreve o seguinte comportamento:
![[Pasted image 20240625232717.png]]
A corrente oscila, mas com amortecimento exponencial (envoltória) de constante de tempo $2/\gamma \equiv 2 \tau_L$.

==**Amortecimento fraco**==
No caso em que
$$
\gamma \ll \omega_0 \therefore \omega_1 \approx \omega_0
$$


## Circuito RLC forçado (com gerador AC)
![[Pasted image 20240625233654.png]]
Considerando o circuito RLC agora ligado a uma fonte externa geradora de corrente alternada tal que:
$$
V = V_m \cos{(\omega t)}
$$
Temos que:
$$
V = \frac{Q}{C} + L \frac{dI}{dt} + RI
$$
E portanto:
$$
\begin{gather}
I(t) = I_m \cos(\omega t - \phi) \\
I_m = \frac{V_m}{Z} = \frac{V_m}{\sqrt{R^2 + \left( \omega L - \frac{1}{\omega C} \right)^2}}
\end{gather}
$$
onde $Z$ é a impedância do circuito:
$$
Z = \sqrt{R^2 + \left(\omega L - \frac{1}{\omega C} \right)^2}
$$
Ou seja, pela relação para $I_m$, a ==corrente será máxima quando== $\omega = \omega_0 = \frac{1}{\sqrt{LC}}$ (frequência angular natural é a frequência de ressonância). E essa corrente máxima também pode ser obtida por:
$$
I_m(\omega = \omega_0) = \frac{V_m}{R}
$$
Além disso, a fase $\phi$ é dada por:
$$
\begin{gather}
\tan \phi = \frac{\omega L - \frac{1}{\omega C}}{R} \\
\tan \phi = \frac{\omega_0 L}{R} \left( \frac{\omega}{\omega_0} - \frac{\omega_0}{\omega} \right)
\end{gather}
$$


# Materiais magnéticos
![[Pasted image 20240626092151.png]]
Considerando uma barra cilíndrica cortada no meio como a da imagem. A magnetização resulta de correntes microscópicas, chamadas de correntes de Ampère, nas quais os efeitos de elementos adjacentes se cancelam (as correntes do meio se cancelam). 
Então, sobra só uma corrente superficial, confinada à superfície do cilindro (linha tracejada na imagem).

![[Pasted image 20240626092650.png]]

## Densidade de corrente de magnetização
Sendo $\vec{J}_m$ a ==densidade de corrente superficial de magnetização==, definida de tal forma que:
$$
\vec{J}_m = \frac{di}{dz} \hat{\phi}
$$
É importante notar que $\vec{J}_m$ tem medida de corrente por unidade de comprimento, e não de volume. Mais pra frente aparece uma densidade volumétrica de magnetização $\vec{j}_m$. 

Temos que a espira anular da imagem tem um *momento de dipolo magnético* dado por:
$$
\begin{gather}
d\vec{m} = (di) \vec{S} = (di) \pi a^2 \hat{z} \\
||d\vec{m}|| = ||\vec{J}_m|| (\pi a^2) dz = ||\vec{J}_m|| dv
\end{gather}
$$
onde $dv$ é o volume do cilindro de altura $dz$.

## Magnetização
A ==*Magnetização*== $\vec{M}$ é, por definição, o momento de dipolo magnético por unidade de volume:
$$
\vec{M} \equiv \frac{d\vec{m}}{dv}
$$
Assim, como $\hat{\phi} = \hat{z} \times \hat{\rho}$, resulta em outra relação para $\vec{J}_m$:
$$
\vec{J_m} = \vec{M} \times \hat{\rho} = \vec{M} \times \hat{n}
$$
onde $\hat{n}$ é a normal externa à superfície do cilindro.

Daí e de outras deduções, sai também que:
$$
\vec{J}_m = \mathrm{rot} \vec{M} = \vec{\nabla} \times \vec{M}
$$
que serve especificamente para calcular a densidade volumétrica de corrente de magnetização devido a uma magnetização inomogênea.

## O campo H
O campo magnético $\vec{B}$ produzido pelas correntes de magnetização $\vec{j}_m$ se soma àquele devido às correntes livres $\vec{j}$ (correntes devidas ao transporte de portadores de carga).
Logo, na presença de magnetização, a lei de Ampère fica:
$$
\mathrm{rot} \ \vec{B} = \mu_0 (\vec{j} + \vec{j}_m) = \mu_0 \vec{j} + \mu_0 \ \mathrm{rot} \ \vec{M}
$$
Assim, define-se um novo campo $H$:
$$
\begin{gather}
\mathrm{rot} \ \vec{H} = \vec{j} \\
\vec{H} \equiv \frac{\vec{B}}{\mu_0} - \vec{M}
\end{gather}
$$
Também temos que:
$$
\mathrm{div} \ \vec{H} = - \mathrm{div} \ \vec{M}
$$
de forma que as linhas de $\vec{H}$ não são fechadas, como as de $\vec{B}$, se $\vec{M}$ não for homogêneo.

Se temos um meio magnético linear, homogêneo e isotrópico, a magnetização $\vec{M}$ é proporcional ao campo $\vec{B}$ no interior do meio:
$$
\vec{M} = \chi_m \vec{H}
$$
onde $\chi_m$ chama-se susceptibilidade magnética do meio. Daí resulta:
$$
\vec{B} = \mu_0 (\vec{H} + \vec{M}) = \mu_0 (1 + \chi_m) \vec{H} = \mu \vec{H}
$$
onde
$$
\mu = \mu_0 (1 + \chi_m) \equiv \mu_0 \kappa_m
$$
A constante material $\mu$ chama-se permeabilidade magnética do meio, e $\kappa_m = 1 + \chi_m$ é a permeabilidade magnética relativa. Em particular, no vácuo $\mu = \mu_0$.

# Equações de Maxwell

### Equações básicas de campos eletromagnéticos
Até agora, as principais equações básicas de campos eletromagnéticos foram:
- Em forma integral:
$$
\begin{gather}
\oint_S \vec{E} \cdot \hat{n} \ dS = \frac{q}{\varepsilon_0} \ \tag{1} \\
\oint_S \vec{B} \cdot \hat{n} \ dS = 0 \ \tag{2} \\
\oint_C \vec{B} \cdot d\vec{l} = \mu_0 I_C \ \tag{3} \\
\varepsilon = \oint_C \vec{E} \cdot d\vec{l} = - \frac{d}{dt} \int_S \vec{B} \cdot \hat{n} \ dS = -\frac{d \Phi_B}{dt} \ \tag{4} \\
\end{gather}
$$
- Em forma diferencial
$$
\begin{gather}
\mathrm{div} \ \vec{E} = \frac{\rho}{\varepsilon_0} \\
\mathrm{div} \ \vec{B} = 0 \\
\mathrm{rot} \ \vec{B} = \mu_0 \vec{j} \\
\mathrm{rot} \ \vec{E} = - \frac{\partial B}{\partial t}
\end{gather}
$$
além de termos também a força de Lorentz:
$$
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
$$

## Equações de Maxwell (no vácuo)
$$
\begin{gather}
\mathrm{rot} \ \vec{B} = \mu_0 \vec{j} + \varepsilon_0 \mu_0 \frac{\partial \vec{E}}{\partial t} \tag{I} \\
\mathrm{rot} \ \vec{E} = - \frac{\partial B}{\partial t} \tag{II} \\
\mathrm{div} \ \vec{E} = \frac{\rho}{\varepsilon_0} \tag{III} \\
\mathrm{div} \ \vec{B} = 0 \tag{IV}
\end{gather}
$$
A principal "novidade" é o segundo termo da equação $(\mathrm{I})$, e representa que um campo elétrico variável com o tempo produz um campo magnético (reciproco da lei de Faraday).

O segundo termo também recebe o nome de ==*corrente de deslocamento*==:
$$
\vec{j}_d = \varepsilon_0 \frac{\partial \vec{E}}{\partial t}
$$

A equação (I) pode ser escrita também na forma integral, relacionando o campo magnético com a variação do fluxo elétrico:
$$
\oint_{\partial S} \vec{B} \cdot d\vec{l}= \mu_0 \left( \iint_S \vec{J} \cdot d\vec{S} + \varepsilon_0 \frac{d}{dt} \iint_S \vec{E} \cdot d\vec{S} \right) = \mu_0I_S + \mu_0 \varepsilon_0 \frac{d \Phi_E}{dt}
$$


# Exercícios resolvidos
## P3 Física III 2023
1.
![[Pasted image 20240626105048.png]]
Para calcular o fluxo do campo magnético gerado pela corrente no fio, através da espira, temos:
$$
\begin{gather}
\vec{B}(r) = \frac{\mu_0 i}{2\pi r} \\
\Phi = \int_S \vec{B} \cdot \hat{n} \ dS
\end{gather}
$$
Adotando um sistema de coordenadas comum (y vertical e x horizontal) temos que o vetor $\hat{n} = \hat{j}$. Pela regra da mão direita, as linhas de campo magnético que passam pela espira são paralelas ao vetor normal (então o produto escalar será simplesmente $\vec{B} \cdot \hat{n} = B$). Além disso, nosso elemento de área corresponde a um pedaço retangular da espira tal que $dS = adr$, com $r$ saindo de $y_0$ e indo até $y_0 + b$. Logo:
$$
\Phi =  \frac{\mu_0 i a}{2\pi} \int_{y_0}^{y_0 + b} \frac{1}{r} dr = \frac{\mu_0 i a}{2 \pi} \ln{\left( \frac{y_0 + b}{y_0} \right)}
$$
Então, substituindo os valores, temos que, quando a parte inferior da espira está a uma distância $y_0 = 1$ cm, $\Phi = 2,7 \times 10^{-8} T \cdot m^2$.

A corrente induzida na espira será devida à fem induzida nela pela variação do fluxo:
$$
\begin{gather}
I_{ind} = \frac{\varepsilon_{ind}}{R} \\
\varepsilon_{ind} = - \frac{d \Phi}{dt}
\end{gather}
$$
Para encontrar $\frac{d \Phi}{dt}$, sabemos que a espira é afastada com uma velocidade constante $v$ de 5 cm/s, e portanto a distância $y$ entre o fio e a parte inferior da espira se afastam com uma velocidade constante. Logo, dado uma distância $y$:
$$
\begin{gather}
\Phi(y) = \frac{\mu_0 i a}{2 \pi} \ln{\left( \frac{y + b}{y} \right)} \\
\frac{d \Phi}{dt} = \frac{d \Phi}{dy} \frac{dy}{dt} = \frac{d\Phi}{dy} v = -\frac{\mu_0 i a b}{2\pi y(b+y)} v
\end{gather}
$$
Assim, a uma distância $y_0$:
$$
\begin{gather}
\varepsilon_{ind} = - \frac{d \Phi}{dt}(y_0) = \frac{\mu_0 i a b}{2\pi y_0(b+y_0)} v  \\
I_{ind} = \frac{\varepsilon_{ind}}{R} = 17 \ \mu\mathrm{A}
\end{gather}
$$
O sentido da corrente induzida será aquele que cria um campo magnético contrário ao que atravessa a espira. Assim, nesse caso, o sentido será horário.


2.
![[Pasted image 20240626111658.png]]
Lembrando que as frequências dadas estão em Hz, e precisamos usar as frequências angulares:
$$
\omega = 2\pi f
$$
Para encontrar a resistência $R$, sabemos que:
$$
\begin{gather}
Z = \sqrt{R^2 + \left( L\omega - \frac{1}{\omega C} \right)^2} \\
\tan \phi = \frac{\omega L - \frac{1}{\omega C}}{R}
\end{gather}
$$
sendo $\omega$ a frequência de excitação da fonte, e não a de ressonância.
Assim:
$$
R = \frac{Z}{\sqrt{1 + \tan^2 \phi}} = 1 \ k\Omega
$$

Manipulando também a relação de $\tan \phi$ e fazendo $C = \frac{1}{\omega_0^2 L}$, temos:
$$
	L = \frac{R \tan \phi}{\omega - \frac{\omega_0^2}{\omega}} = 0,04 H
$$

Portanto:
$$
C = 19,89 \ \mathrm{nF}
$$

(na solução da prova ta diferente, mas na solução pro capacitor multiplicaram pela frequência em Hertz, e não a frequência angular). 

3.
![[Pasted image 20240626214430.png]]
O fio vai ser enrolado em um solenoide com $N=50$ espiras, raio $R=1$ cm e comprimento $l=10$ cm, e dentro dele tem um cilindro de madeira com mesmo raio e comprimento. 

a) Pra calcular a autoindutância do sistema utilizamos $L=\frac{\Phi}{i}$.
Temos que, supondo uma corrente $i$ que passa pelo fio de cobre, e considerando a direção $\hat{z}$ passando por dentro do solenoide (coaxial), podemos calcular o campo magnético e seu fluxo:
$$
\begin{gather}
\vec{B} = \frac{\mu_0 N i}{l} \hat{z} \\
\Phi = N \int_S \vec{B} \cdot \hat{z} \ dS = \frac{\mu_0 N^2 i}{l} (\pi R^2)
\end{gather}
$$
Logo, a autoindutância será (que seria simplesmente ter a formula de autoindutância de um solenoide):
$$
L = \frac{\Phi}{i} = \frac{\mu_0 N^2 \pi R^2}{l} = 9,87 \ \mu H
$$

b) Ligando a um gerador AC de tensão $V = V_0 \sin{(\omega t)}$ e a um capacitor $C = 1$ mF, temos um circuito RLC, já que o fio tem resistividade. Assim, temos a relação da fase $\phi$:
$$
\tan \phi = \frac{\omega L - \frac{1}{\omega C}}{R} \equiv \frac{\omega_0 L}{R} \left( \frac{\omega}{\omega_0}- \frac{\omega_0}{\omega} \right)
$$
Ou seja, pela relação a fase $\phi$ será 0 quando $\omega = \omega_0$. Logo:
$$
\omega = \omega_0 = \frac{1}{\sqrt{LC}} = 10065,84 \ s^{-1}
$$

c) A amplitude da corrente elétrica na ressonância é dada por:
$$
I_m = \frac{V_m}{R}
$$
Nesse caso $V_m = V_0 = 0,1 \ V$. Pra achar $R$, leva em conta a resistividade $\rho$ do fio, e além disso, o comprimento do fio será $l=2\pi R N$, já que ele foi enrolado em 50 espiras, e sua seção transversal tem área $\pi$ mm$^2$. Logo:
$$
R = \rho \frac{l}{A} = 2 \cdot 10^{-2} \ \Omega
$$
Assim:
$$
I_m = 5 \ A
$$

4.
![[Pasted image 20240626223837.png]]
A corrente de condução é dada por $\vec{J}$, e a corrente de deslocamento é dada por $\epsilon_0 \frac{\partial \vec{E}}{\partial t}$. Assim, a amplitude da corrente de condução será:
$$
J = \sigma E_0
$$
E a amplitude da corrente de deslocamento, considerando que $E = E_0 \sin{(\omega t)}$, será:
$$
\epsilon_0 \frac{\partial \vec{E}}{\partial t} = \epsilon_0 E_0 \omega
$$
Então para serem iguais:
$$
\begin{gather}
\sigma E_0 = \epsilon_0 E_0 \omega \\
\sigma = \epsilon_0 \omega \\
\omega = \frac{\sigma}{\epsilon_0} = 1,1 \cdot 10^{18} \ s^{-1}
\end{gather}
$$
