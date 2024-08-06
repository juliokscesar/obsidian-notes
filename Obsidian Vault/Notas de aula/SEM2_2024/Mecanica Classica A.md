# Introdução e Conceitos Básicos
....

# Movimento em 1D
Leis de Newton e Lei de conservação (momento, energia).
### Velocidade
Sendo $x(t)$ a posição de uma partícula no tempo $t$:
$$
v = x'(t) = \frac{dx}{dt}
$$
é uma grandeza relativa.

### Aceleração
Grandeza *absoluta* (não relativa)
$$
a = x''(t) = \frac{dv}{dt}
$$
### Força
O que causa a aceleração é a força.
$$
F = ma
$$
#### Força Gravitacional
Massa sente e *causa* força
$$
F_g = G \frac{m_1 m_2}{r^2}
$$
- Peso: Força gravitacional de uma massa (na Terra ou em qualquer outro corpo massivo de massa $M$):
$$
P = m \ G \frac{M}{r²} = mg
$$
### Momento linear
$$
\begin{gather}
p = mv \\
F = \frac{dp}{dt}
\end{gather}
$$
Momento total de $n$ partículas (se conserva sem ação de força externa):
$$
p_t = m_1 v_1 + m_2 v_2 + ... + m_n v_n
$$

### Energia e Trabalho
Trabalho ($W$):
$$
W = F \Delta x = \int_{x_1}^{x_2} F dx
$$
Energia Cinética ($K$):
$$
\begin{align}
W_{1 \to 2} &= \int_1^2 F dx \\
&= \int_1^2 m \frac{dv}{dt} dx = \int_1^2 m \frac{dv}{dt} \frac{dx}{dt} dt \\
&= \int_1^2 m \ \dot{v} \ v \ dt \\
&= m \left. \frac{v^2}{2} \right|_1^2 \\
K &= m\frac{v^2}{2}
\end{align}
$$
### Leis de Newton
- 1ª Lei: Lei da Inércia
- 2ª Lei: $F = \frac{dp}{dt} = ma$
- 3ª Lei: Ação e reação $\equiv$ Conservação do momento total: $m_1 a_1 = - m_2 a_2$ (caso não haja ação de força externa)

