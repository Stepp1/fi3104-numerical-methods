# Control 1 Métodos Númerico

### Contenidos 

- Integración Gaussiana.
- Integrales impropias.


## Resumen
1. Errores Absoluto y Relativo:

	* Absoluto:
		$$
		\epsilon_a = \overline{X} - X_i
		$$
		​		*El error absoluto es un indicador de la imprecisión que tiene una determinada media.*

	* Relativo: 
		$$
		\epsilon_r = \frac{\epsilon_a}{\overline{X}}
		$$
		​		*El error relativo tiene la misión de servir de indicador de la calidad de una medida.* 

	

2. Derivadas Discretas:

	* Hacia adelante:

	
	$$
	f'(t)=\frac{f(t+h) - f(t)}{h} + O(h)
$$
	
	* Hacia atras:
$$
		f'(t)=\frac{f(t) - f(t - h)}{h} + O(h)
		$$

* Central:
		$$
		f'(t)=\frac{f(t+h) - f(t - h)}{2h} + O(h^2)
	$$
	

	

Los errores se obtienen con las aproximaciones de Taylor
	


* Segunda derivada: 
		$$
		f''(t) = \frac{f(t+h) - 2f(t) + f(t-h)}{h^2} + O(h^2)
	$$
	

	
3. Interpolación:  **interpolation** is a method of constructing new data points within the range of a discrete set of known data points.

	* Lineal: 
		$$
		y = y_a + (y_b - y_a) \space \cdot \space \frac{x - x_a}{x_b - x_a}
		$$
		Previous equation states that the new line between $(x_a,y_a)$ and $(x,y)$ has the **same slope as the slope** of the line between $(x_a,y_a)$ and $(x_b,y_b)$


​		

4. Método de Lagrange:

  De manera general: 	$p(x) = a_n x^n + a_{n-1}x^{n-1} +…+ a_2x^2 +a_1x + a_0$

  Así,
  $$
  L(x)=f(x) = \frac{(x - x_2)(x - x_3)...(x - x_n)}{(x_1 - x_2)(x_1 - x_3) ...(x_1 - x_n)} \cdot y_1 \space ... \space \frac{(x - x_1)(x - x_2)...(x - x_{n-1})}{(x_n - x_1)(x_n - x_2) ...(x_n - x_{n-1})}\cdot y_n
  $$

  

  Donde cada termino que acompaña a un $y_i$ se le denomina como $l_i$

  ```python
  # Interpolation
      resultado = 0
      n = len(valX)
      for i in range(n):
          L = 1
          for j in range(n):
              if(i == j):
                  continue
              L *= float(x - valX[j])/float(valX[i] - valX[j])
                  
          resultado += L*valY[i]
  ```

  

5. Método de Newton:

  Given a set of *k* + 1 data points $$(x_0,y_0)…(x_j,y_j)…(x_k,y_k)$$ y ningún $x_j$ es igual a otro:

  ![N(x):=\sum _{{j=0}}^{{k}}a_{{j}}n_{{j}}(x)](https://wikimedia.org/api/rest_v1/media/math/render/svg/b7bb15443c96172a7ef235cb973010feab25e428)

  ![n_{j}(x):=\prod _{{i=0}}^{{j-1}}(x-x_{i})](https://wikimedia.org/api/rest_v1/media/math/render/svg/227efa64e8b5301108a7a5da5cbbb86dcf59af04)

  Con $n_0 = 1$

  Entonces,

  ![N(x)=[y_{0}]+[y_{0},y_{1}](x-x_{0})+\cdots +[y_{0},\ldots ,y_{k}](x-x_{0})(x-x_{1})\cdots (x-x_{{k-1}}).](https://wikimedia.org/api/rest_v1/media/math/render/svg/b68037ee2fd3c52e2f564605fcd6308048dee2f1)

  Ademas, sea (equiespaciado) $h=x_{i+1}-x_i$ —> $x = x_0 +sh$ 
  $$
  N(x)=\sum^{k}_{i=0} \binom{s}{i}i!h^i[y_0,..y_i]
  $$

  ​							*Newton's formula is Taylor's polynomial based on finite differences instead 														 	instantaneous rates of change*

  

6. Integración Numérica:

	* Regla Trapezoidal:
		![Screen Shot 2019-04-24 at 14.58.15](/Users/R/Desktop/Metodos Numericos/Screen Shot 2019-04-24 at 14.58.15-6132492.png)
		$$
		T_i= \frac{1}{2} (x_{i+1} - x_i)(f_{i+1} + f_i)
		$$
		

		Así, la integral: $I \approx I_T= T_0 + T_1 +… T_{N-1}$

		En el caso equiespaciado: $h = \frac{b-a}{N} \implies x_i=a+ih \implies T_i= \frac{1}{2} h(f_{i+1} + f_i)$

		Así, 
		$$ {da}
		\begin{align}
		I_T(h) =  \frac{1}{2}hf_0+hf_1 + … + hf&_{N-1} + \frac{1}{2}hf_N \\
		= \frac{1}{2}h(f_0+f_N) + h\sum^{N-1}_{i=1} f_i 
		\end{align}
		$$
		Para calcular el error:

		![{\displaystyle E_{t}=-{\frac {1}{12}}f''(\xi )(b-a)^{3}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/523edb27b0310bad7e16af07eec0a3591109e2b4)

		donde $\xi \in [a, b]$

		

7. Fórmula Newton-Cotes: *Generalización de muchas fórmulas equiespaciadas.*

	* Formulas cerradas: usan los valores en todos los $x_i, \space x_i=h\cdot i+x_0, \space h=\frac{b-a}{n}$
		$$
		\begin{align}
		&\int _{a}^{b}f(x)\,dx\approx \sum _{{i=0}}^{n}w_{i}\,f(x_{i}) \quad w_i: pesos/weigths\\
		\end{align}
		$$
		

		Usando Polinomio de Lagrange:

		![{\displaystyle \int _{a}^{b}f(x)\,dx\approx \int _{a}^{b}L(x)\,dx=\int _{a}^{b}\left(\sum _{i=0}^{n}f(x_{i})\,l_{i}(x)\right)\,dx=\sum _{i=0}^{n}f(x_{i})\underbrace {\int _{a}^{b}l_{i}(x)\,dx} _{w_{i}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2c499732c85ec048ef1279eab57cf653d2acda83)

		Con diferentes grados $n$ :

| Degree *n* |                        Step size *h*                         |                         Common names                         |                           Formula                            |                          Error term                          |
| :--------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|     1      | ![{\displaystyle h=(b-a)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c158e4ba83cf5e0d310507698389439babc6920e) | [Trapezoid rule](https://en.wikipedia.org/wiki/Trapezoid_rule) | ![{\displaystyle {\frac {h}{2}}(f_{0}+f_{1})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/190810541a767e7404bb18a6ad65e7b27e928d0c) | ![-{\frac  {(b-a)^{3}}{12}}\,f^{{(2)}}(\xi )](https://wikimedia.org/api/rest_v1/media/math/render/svg/832a38281b02d44403f66937c749653209eefe07) |
|     2      | ![{\displaystyle h={\frac {(b-a)}{2}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/415038a2eb6e57cc1703224df91e562a419b0781) | [Simpson's rule](https://en.wikipedia.org/wiki/Simpson's_rule) | ![{\displaystyle {\frac {h}{3}}(f_{0}+4f_{1}+f_{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8cea0ac47e190b2b8c49d0e198becf0e6e1ff2ee) | ![{\displaystyle -{\frac {(b-a)^{5}}{90\cdot 2^{5}}}\,f^{(4)}(\xi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5b2710aa9cd1df7d7be3e3d169542d95f73ef07e) |
|     3      | ![{\displaystyle h={\frac {(b-a)}{3}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aa2078209bb2e5105943d1ca703d8983c90f18c4) | [Simpson's 3/8 rule](https://en.wikipedia.org/wiki/Simpson's_rule#Simpson's_3/8_rule) | ![{\displaystyle {\frac {3}{8}}\cdot h(f_{0}+3f_{1}+3f_{2}+f_{3})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ccc0ab0cd061d01b3a8313fed17fa14c1074a2b8) | ![{\displaystyle -{\frac {3(b-a)^{5}}{80\cdot 3^{5}}}\,f^{(4)}(\xi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b496d9784f524d9f2be3939955b3d0fdb82b68) |
|     4      | ![{\displaystyle h={\frac {(b-a)}{4}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43d304a0454f8882444f5c4a3dc71cb5cffc0e09) |  [Boole's rule](https://en.wikipedia.org/wiki/Boole's_rule)  | ![{\displaystyle {\frac {2h}{45}}(7f_{0}+32f_{1}+12f_{2}+32f_{3}+7f_{4})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a86158a4ee409ea52d1f989cac7d5d1744907635) | ![{\displaystyle -{\frac {8(b-a)^{7}}{945\cdot 4^{7}}}\,f^{(6)}(\xi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed957a117732d99eb23732bb98f61f78a6da6cc9) |

​					*For large n a Newton–Cotes rule can sometimes suffer from catastrophic [Runge's phenomenon](https://en.wikipedia.org/wiki/Runge's_phenomenon) 					where the error grows exponentially for large n.* 

​		—> Se prefiere utilizar I. de Gauss con punto que no estén equidistribuidos.
​		—> Si sólo hay equidistribuidos, se puede descomponer el intervalo de integración.



8. Integración Gaussiana:

	

9. Integrales impropias:

10. Raíces de ecuaciones.

11. Método de bisección.

```python
n = 0
        start= time.time()
        while(n < nMax):
            c = float((a + b))/float(2)
            # If f(c) = 0 we have a root, if ((b - a)/2) < tol then we meet a stopping criteria
            if(f(c) == 0 or ((b - a)/2) < tol):
                valor = [c,n]
                end = time.time()
                print("Esta iteración tomó " + str((end - start)) + " segundos")
                return valor
            
            # else, do another subinterval
            n += 1
            
            # new interval
            if(np.sign(f(c)) == np.sign(f(a))):
                a = c
            else:
                b = c
```

* Verlet.

- Métodos de Runge-Kutta.