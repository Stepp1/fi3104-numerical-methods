#### Métodos Numéricos

# Clase Ecuaciones Diferenciales Parciales

### EDPs

#### 3 tipos de PDE: hiperbólico, elíptico, parabólico.

1. Hiper: ec de onda, ec de adveccion

	pbs de Casos de Borde. La solución esta determinada por estos y la fuente f(x)

2. Eliptico: ec de poisson

3. Parabolico (mezcla las dos anteriores): ec de calor

	

* Como resolverlas?

	f(x,t) debe ser descrita en un conj. de puntos finitos (x,t)

	Existen 2 tipos de discretización:

	1. Métdos de Grillas —> f es representada en los puntos xi y tn de una grilla

		* Grillas Estructuradas

		1. Grillas Cartesianas: $\Delta x, \Delta y, \Delta t$ son regulares, equiespaciados

		2. Grillas no Cartesianas: mapeo de grillas no cartesiana a cartesiana

			

		* Grillas No Estructuradas:

		1. 2D —> triangulos
		2. 3D —> tetraedros

		Mosaicos de Veronoi

		

	2. Sin grillas —> función f(x) es representada por un conj de funciones de base (métodos espectrales) o por partículas (N Body, SPH).

	

	Escribir la PDE en estas grillas: 

	* métodos diferencias finitas —> las derivadas son aproximadas numericamente
	* métodos de Volumen finito —> donde se la version integral de la PDE

`

*  Ec de adveccion:

$$
\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = 0
$$

​	 —> c es la velocidad de adveccion  (propagación de $u(x,0)$).
$$
u (x- ct)
$$
Es solución de la ec.

Sea,
$$
U_i^n = U(x_i, t_n)
$$

$$
\frac{\partial u}{\partial t}(x,t) \implies \frac{U_i^{n+1} - U_i^{n}}{\Delta t}\\
\land\\
\frac{\partial u}{\partial x}(x,t) \implies \frac{U_{i}^{n} - U_{i-1}^{n}}{\Delta x}
$$

Así, la ec. queda: 
$$
\frac{U_i^{n+1} - U_i^{n}}{\Delta t} = -c\big( \frac{U_{i}^{n} - U_{i-1}^{n}}{\Delta t}\big)\\
\textrm{Derivada depende de de vañores anteriores, método se llama de corriente arriba (*upwinding*)}\\
\land\\
U_i^{n+1} = U_i^n = -\frac{c\Delta t}{\Delta x} \bigg( U_i^n - U_{i-1}^n\bigg)
$$





* Estabilidad: 

	Análisis de Von Neumman:

	Sea $U_i^n = y_i^n +\epsilon_i^n$

	Donde se tiene la sol. discreta igual a la sol. exacta más error local.
	$$
	\dots
	$$
	El error relativo entre $\epsilon^{n+1}_j$ y $\epsilon^{n}_j$ está dado por:
	$$
	G = \frac{\epsilon^{n+1}_j}{\epsilon^{n}_j} = e^{\alpha \Delta t} = 1 -r[1-e^{-ik\Delta x}]\\
	\implies \\
	G= 1-r[1 - cosk\Delta x + i sink\Delta x]
	$$
	Método es estable si $|G| <= 1$:
	$$
	|G|^2 = \dots \implies 2r(1-cosk\Delta x) (1-r) >= 0\\
	\implies \\
	1-r >= 0\\
	\implies \\
	c\frac{c\Delta t}{\Delta x}<= 1\\
	\textrm{Condicion CFL, Courant-Friederichs-Levy}
	$$
	







…..





#### Ecuacion de Flujo Conservado

$$
\frac{\partial u}{\partial t} = - \frac{\partial F(u)}{\partial x}
$$



* Advección
	$$
	F(u) = -cu \implies \frac{\partial u}{\partial t} = c\frac{\partial u}{\partial x}
	$$
	

* Calor

$$
F(u) = D\frac{\partial u}{\partial x} \implies \frac{\partial u}{\partial t} = \frac{\partial }{\partial t} \bigg(\frac{\partial u}{\partial x}\bigg)
$$



* Onda
	$$
	\frac{\partial^2 u}{\partial t^2} = c^2\frac{\partial^2 u}{\partial x^2}
	\\
	\land
	\\
	r= c\frac{\partial u}{\partial x}  \quad \land \quad s = \frac{\partial u}{\partial t}
	$$


$$
\frac{\partial r}{\partial t} = c\frac{\partial u}{\partial x}
\\
\iff
\\
\frac{\partial s}{\partial t} = c\frac{\partial r}{\partial x}
$$
Así 
$$
\vec{u} = \begin{bmatrix}
    r \\
    s 
\end{bmatrix}
$$

$$
\frac{\partial \vec{u}}{\partial t} = - \frac{\partial \vec{F(\vec{u})}}{\partial t}
\\
\implies
\\
\vec{F} = 
\begin{bmatrix}
    0 & -c \\
    - & 0
\end{bmatrix}
\cdot
\begin{bmatrix}
    r \\
    s 
\end{bmatrix}
$$


* Método de Lax - Wendroff



FOTO CONSU



* Ecuación de Difusión (parabolica)

$$
\frac{\partial u}{\partial t} = \frac{\partial}{\partial x}\bigg(D\frac{\partial u}{\partial x}\bigg)
$$

Con $D = D(x), D(u)$ cte



<u>Ec. de tipo flujo conservado</u> si $F=- D\frac{\partial u}{\partial x}$

Supongamos D>=0 (si no es inestable)



Sea  $D = cte \implies \frac{\partial u}{\partial t}=  D\frac{\partial^2l u}{\partial x^2}$ (calor)



Usamos FTCS: (método explícito)
$$
\frac{U_i^{n+1} - U_i^{n}}{\Delta t} = D \bigg[ \frac{U^{n}_{j+1} - 2U^{n}_{j} + U^{n}_{j-1}}{(\Delta x)^2}\bigg] + O(\Delta t)+ O(\Delta x)
$$
FTCS era inestable para advección pero para calor es estable! si $2D \frac{\Delta t}{\Delta (x)^2 } <= 1$



Ahora implícito:
$$
\frac{U_i^{n+1} - U_i^{n}}{\Delta t} = D \bigg[ \frac{U^{n+1}_{j+1} - 2U^{n+1}_{j} + U^{n+1}_{j-1}}{(\Delta x)^2}\bigg]
$$


Este es un sis de ecs algebraicas con $U^{n+1}_j$ como incógnita:
$$
-\alpha U^{n+1}_{j-1} + (1+2\alpha) U^{n+1}_{j} -\alpha U^{n+1}_{j+11} = U^n_ j
$$
$j = 1,2,…,n-1$

$+$ CB. en $j=0$  y $j=n$



FOTO MATRIZ GIGANTE CONSU



Crank - Nicholson



* Ec de Calor

	​													

	​									     		___________________________________________________________________________________________________________________

	​												|_______________________________________________________________________________________________________________________|

​														$y=0$                                                     $y=L$ 


$$
\frac{\partial u}{\partial t} = D \frac{\partial^2 u}{\partial x^2}
$$
$+$ CB:
$$
u(0,t)=u_L(t)\\
u(L,t)= u_R(t)\\
t>0
$$
$+$ C.I.
$$
u(x,0) = g(x) \\
\textrm{para } 0<=x<=L
$$


Por simplicidad,  $L=1, D=1$

C.B. $u_L(t) = u_R(t)=0$

La solución de la ec. 
$$
U(x,t) = \sum^{inf}_{n=1} A_n e^{\lambda^2 nt} sin(\lambda_nx)\\
\textrm{con } \lambda_n = n\pi \space \textrm{y } A_n = 2\int^1_0 g(x) sin(\lambda_nx)dx
$$


<u>Caso 1</u>: $g(x) = sin(2\pi x) \quad 0\leq x \leq1$
$$
\implies U(x,t) = e^{4\pi^2 t} sin(2\pi x)
$$


<u>Caso 2</u>:
$$
g(x) = \begin{cases}
       1 \quad \textrm{si} \space a\leq x\leq b\\
       0 \quad \textrm{resto}
       \end{cases}\\
       \implies\\
A_n = \frac{2}{\pi n} [cos(a\pi n) - cos(b\pi n)]
$$


* Ec. Schrodinger



….



