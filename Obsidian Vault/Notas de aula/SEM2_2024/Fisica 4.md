# Equações de Maxwell
(a última tá sem o termo de Maxwell)
$$
\begin{gather}
\oint_S \vec{E} \cdot \vec{n} \ dS = \frac{q}{\varepsilon_0} \leftrightarrow \nabla \cdot \vec{E} = \frac{q}{\varepsilon_0} \\

\oint_S \vec{B} \cdot \vec{n} \ dS = 0 \leftrightarrow \nabla \cdot \vec{B} = \frac{q}{\varepsilon_0} \\

\oint_C \vec{E} \cdot d\vec{l} = - \frac{\partial}{\partial t} \int_S \vec{B} \cdot \vec{n} \ dS \leftrightarrow \nabla \times \vec{E} = - \frac{\partial B}{dt} \\

\oint_C \vec{B} \cdot d\vec{l} = \mu_0 i \leftrightarrow \nabla \times \vec{B} = \mu_0 \vec{J}
\end{gather}
$$
Derivando a ultima equação:
$$
\nabla \cdot (\nabla \times \vec{B}) = \mu_0 \nabla \cdot \vec{J}
$$
o primeiro termo zera (divergente do rotacional é 0). Mas o da direita não é sempre zero, então Maxwell acrescentou uma correção (termo de Maxwell):
$$
\nabla \times \vec{B} = \mu_0 \vec{J} + \mu_0 \varepsilon_0 \frac{\partial \vec{E}}{\partial t}
$$
Fazendo o rotacional da penúltima equação também:
$$
\begin{gather}
\nabla \times (\nabla \times \vec{E}) = - \frac{\partial}{\partial t} (\nabla \times \vec{B}) \\

\nabla (\nabla \cdot \vec{E}) - \nabla^2 \vec{E} = - \frac{\partial}{\partial t} \left[ \mu_0 \varepsilon_0 \frac{\partial \vec{E}}{\partial t} \right] \\

\nabla^2 \vec{E} = \mu_0 \varepsilon_0 \frac{\partial^2 \vec{E}}{\partial t^2}
\end{gather}
$$

### Equação de onda eletromagnética
$$
\nabla^2 \vec{E} = \mu_0 \varepsilon_0 \frac{\partial^2 \vec{E}}{\partial t^2}
$$
que equivale a uma equação de onda:
$$
\frac{\partial^2 f}{\partial x^2} = \frac{1}{v^2} \frac{\partial f}{\partial t^2}
$$
Portanto temos a velocidade de uma onda eletromagnética (*velocidade da luz*):
$$
c = \frac{1}{\sqrt{\mu_0 \varepsilon_0}} \approx 3 \cdot 10^8 \ \mathrm{m/s}
$$
