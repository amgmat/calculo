---
title: "Tema 2 - Sucesiones y límites"
author: "Juan Gabriel Gomila, Arnau Mir y Llorenç Valverde"
date: ''
output: 
  ioslides_presentation: 
    css: Mery_style.css
    fig_caption: yes
    keep_md: yes
    logo: Images/calculus.gif
    widescreen: yes
---
<script src="https://kit.fontawesome.com/a0edb659c7.js" crossorigin="anonymous"></script>



# Introducción


## Ejemplos

<div class="example">

**Ejemplo 1.** Consideremos las sucesivas aproximaciones decimales de $\sqrt{2}$,

$$
1,1.4,1.41,1.414,1.4142,1.41421,\ldots
$$ 
Cada uno de estas aproximaciones mejora la anterior, puesto que cada una difiere de $\sqrt{2}$ en menos de $10^{-n}$, donde $n$ indica el número de cifras decimales de la aproximación racional. Obsérvese tambien que una vez alcanzada una determinada precisión, los términos siguientes mejoran dicha precisión.

En general, dado un $\epsilon$, es decir, una precisión, podemos asegurar que, a partir de un término dado que diste menos que esa precisión de la raíz cuadrada de 2, los subsiguientes términos distan de $\sqrt{2}$ menos que esa precisión. 
</div>

## Ejemplos

<div class="example">
Para generar los 15 primeros términos de la sucesión anterior en `python` haríamos lo siguiente:

```python
import math
def trun_n_d(n,d):
    s=repr(n).split('.')
    if (len(s)==1):
        return int(s[0])
    return float(s[0]+'.'+s[1][:d])
x=math.sqrt(2)
n=15
for i in range(1,n):
   print "%.15f" % (trun_n_d(x,i))
```

</div>

## Ejemplos

<div class="example">

```
## 1.400000000000000
## 1.410000000000000
## 1.414000000000000
## 1.414200000000000
## 1.414210000000000
## 1.414213000000000
## 1.414213500000000
## 1.414213560000000
## 1.414213562000000
## 1.414213562300000
## 1.414213562370000
## 1.414213562373000
## 1.414213562373000
## 1.414213562373090
```

</div>

## Ejemplos 

<div class="example">

**Ejemplo 2.** 

Análogamente, las sucesivas aproximaciones decimales del número $\pi$:
$$
3,3.1,3.14,3.141,3.1415,3.14159, \ldots
$$
aproximan el número $\pi$

Los 15 primeros términos de la sucesión anterior en `python` serían los siguientes:

```python
x=math.pi
n=15
for i in range(1,n):
   print "%.15f" % (trun_n_d(x,i))
```
</div>

## Ejemplos 

<div class="example">

```
## 3.100000000000000
## 3.140000000000000
## 3.141000000000000
## 3.141500000000000
## 3.141590000000000
## 3.141592000000000
## 3.141592600000000
## 3.141592650000000
## 3.141592653000000
## 3.141592653500000
## 3.141592653580000
## 3.141592653589000
## 3.141592653589700
## 3.141592653589790
```

</div>

## Sucesiones

<l class="definition"> **Definición: Sucesión**</l>

Una **sucesión** $\{a_n \}_{n \in \mathbb{N}}$ de números reales es un conjunto de números reales ordenado según un subíndice que recorre los números naturales. Dicho de una manera más formal, una sucesión de números reales es la imagen de una aplicación del conjunto $\mathbb{N}$ en los reales $\mathbb{R}$.



## Ejemplos de sucesiones

<div class="example">

**Ejemplos**

**Ejemplo 7.** La sucesión de **Fibonacci** és una sucesión *recurrente* definida a partir de dos números $x_1$ y $x_2$, de la forma

$$
x_n=x_{n-1} +x_{n-2}
$$
De tal manera que si $x_1 = x_2=1$, sus términos son:
$$
1,1,2,3,5,8,13,21,34, \ldots 
$$
**Ejemplo 8.** La sucesión, también recurrente, $x_1=c>0$, $x_{n+1}=\dfrac{1}{2} \left(x_n + \dfrac{a}{x_n}\right)$, donde $a$ es un nombre real positivo.

La expresión explícita de la sucesión anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=x%281%29%3Dc+and+x%28n%2B1%29%3D%281%2F2%29*%28x%28n%29%2Ba%2Fx%28n%29%29%2C)
</l>
</div>

## Ejemplos de sucesiones
<div class="example">
**Ejemplo**

Para $c=\frac{1}{4}$ y $a=10$, el gráfico de la sucesión definida anteriormente es el siguiente: 
![](CorreccionsTema2Arnau_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

</div>



#  Límite de una sucesión







## Observaciones

<div class="observ"> **Observaciones**

1. De una sucesión con límite diremos que es <l class="important">**convergente**</l>

1. Hay que tener en cuenta que  $\epsilon$  determina el lugar a partir del cual los términos de la sucesión satisfacen  $|a_n - a|<\epsilon$.  Un **cambio en  $\epsilon$** sólo cambia el lugar a partir del cual se satisface la desigualdad. Por eso no debe sorprender si alguna vez aparece un  **$\epsilon$  multiplicado o dividido por una constante**. La única restricción es que la expresión resultante en función de  $\epsilon$  pueda hacerse tan pequeña como se desee, es decir que una expresión del tipo $\epsilon +K$  no sirve.

2. La **existencia o no del límite** de una sucesión no depende de los primeros términos de la misma, es decir sólo depende del **comportamiento final** de los términos de la sucesión. Es decir, si se remplaza qualquier número finito de términos de una sucesión, la sucesión resultante seguirá teniendo límite o no, según lo tuviera o no la sucesión original.

</div>



## Límites y operaciones (4).

<div class="dem">

**Demostración**
  
  c) Veamos, en primer lugar, que si $\lim {a_n} =a \neq 0$, entonces existe $n_1 \in \mathbb{N}$ tal que para todo $n >n_1$,  $|a_n| > \dfrac{|a|}{2}$. Dado que $\epsilon=\dfrac{|a|}{2} >0$, existe $n_1 \in \mathbb{N}$ tal que para todo $n >n_1$, es $|a|-|a_n| \leq |a-a_n| < \dfrac{|a|}{2}$, en definitiva es $-|a_n| < -|a|+ \dfrac{|a|}{2} = -  \dfrac{|a|}{2}$ . En definitiva hemos visto que $|a_n|> \dfrac{|a|}{2}$, para todo $n > n_1$.
  
Ahora, si $\lim {a_n} =a \neq 0$, tenemos, por una parte que existen $\epsilon >0$ y $n_2$ tal que para todo $n > n_2$ es $|a_n-a|< \dfrac{ \epsilon}{2}$

Dado que $\{a_n\}_{n \in \mathbb{N}}$ tiene límite diferente de $0$, existe $n_1$ tal que $|a_n|$ para todo $n>n_1$ tal que $|a_n| > \dfrac{|a|}{2}$, es decir  $\displaystyle{ \left|\dfrac{1}{a_n}\right|} <  \dfrac{2}{|a|}$

Finalmente, si $n>n_0= \max\{n_1,n_2\}$, $\displaystyle{\left|\dfrac{1}{a}-\dfrac{1}{a_n}\right|} = \displaystyle{ \left|\dfrac{a_n -a}{aa_n} \right|} < \dfrac{\epsilon}{2} \dfrac{2|a|}{|a|}=\epsilon$



## Límites y operaciones (5).

<div class="dem">

  d) En primer lugar, veamos que si $\lim_{n \rightarrow \infty} a_n =a$ y $a_n \geq 0$ para todo $n \in \mathbb{N}$, entonces $a \geq 0$. Supongamos que no, que $a<0$, entonces $\epsilon = -a > 0$, entonces, existe $n_0 \in \mathbb{N}$ tal que $|a_n-a|< \epsilon = -a$ para todo $n \geq n_0$, entonces tendríamos que $a<a_n-a<-a$, lo que signicaría que $a_n < 0$, lo cual contradice la hipótesis, por lo tanto debe ser $a \geq 0$.

Ahora, si $a_n \leq b_n$, entonces $b_n - a_n \geq 0$ y, por lo tanto $b-a = \lim (b_n - a_n) \geq 0$

</div>


# Cálculo de límites


## Cálculo de límites (3)

<div class="example"> 

**Ejemplos** 

1. $\lim \dfrac{3n^4-4n^3-5}{2n^5+5n^3-2n} = 0$
2. $\lim \dfrac{2n^3+4n+1}{3n^3+2n^2}= \dfrac{2}{3}$
3. $\lim \dfrac{3n^5+4n^4+2n}{7n^4+2n^3+n^2+5n}= \infty$
4. $\lim \dfrac{\sqrt{3n^2-1}-\sqrt{n}}{n+1}= \sqrt{3}$
</div>


## Cálculo de límites (3)

<div class="example"> 
Los límites anteriores se resolverían en `python` de la forma siguiente:

```python
from sympy import *
from sympy.abc import n
limit_seq((3*n**4-4*n**3-5) / (2*n**5+5*n**3-2*n),n)
```

```
## 0
```

```python
limit_seq((2*n**3+4*n+1) / (3*n**3+2*n**2),n)
```

```
## 2/3
```

</div>


## Cálculo de límites (3)

<div class="example"> 

```python
limit_seq((3*n**5+4*n**4+2*n) / (7*n**4+2*n**3+n**2+5*n),n)
```

```
## oo
```

```python
limit_seq(((3.*n**2.-1.)**0.5-n**0.5)/(n+1.),n)
```

```
## 1.73205080756888
```
</div>


## Cálculo de límites (3)

<div class="example"> 
Los límites anteriores en `Wolfram Alpha` se pueden ver en los enlaces siguientes:

* $\lim \dfrac{3n^4-4n^3-5}{2n^5+5n^3-2n} = 0$: [![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit+of+%283+n%5E4-4+n%5E3-5%29%2F%282+n%5E5%2B5+n%5E3-2+n%29%2C+when+n+tends+to+infinity)

* $\lim \dfrac{2n^3+4n+1}{3n^3+2n^2}= \dfrac{2}{3}$: [![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit+of+%282+n%5E3%2B+4n+%2B1%29%2F%283+n%5E3%2B2+n%5E2%29%2C+when+n+tends+to+infinity)

* $\lim \dfrac{3n^5+4n^4+2n}{7n^4+2n^3+n^2+5n}= \infty$: [![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit+of+%283n%5E5%2B4+n%5E4%2B+2n%29%2F%287+n%5E4%2B2n%5E3%2Bn%5E2%2B5n%29%2C+when+n+tends+to+infinity)

* $\lim \dfrac{\sqrt{3n^2-1}-\sqrt{n}}{n+1}= \sqrt{3}$: [![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit+of+%28Sqrt%5B3+n%5E2-1%5D-Sqrt%5Bn%5D%29%2F%28n%2B1%29%2C+when+n+tends+to+infinity)
</div>



## Cálculo de límites (4)

<l class="prop"> Indeterminaciones del tipo $\infty -\infty$

En estos casos es conveniente multiplicar y dividir por el conjugado de la expresión dada.

<div class="example"> **Ejemplo**

 $\lim (\sqrt{n^2-n+4}-\sqrt{n^2+2})$

$= \lim \dfrac{(\sqrt{n^2-n+4}-\sqrt{n^2+2})(\sqrt{n^2-n+4}+\sqrt{n^2+2})}{\sqrt{n^2-n+4}+\sqrt{n^2+2}}$

$= \lim \dfrac{n^2-n+4-n^2-2}{\sqrt{n^2-n+4}+\sqrt{n^2+2}} = \lim \dfrac{-n+2}{\sqrt{n^2-n+4}+\sqrt{n^2+2}} = -\dfrac{1}{2}$

</div>

## Cálculo de límites (4)

<div class="example"> 
El límite anterior se resolvería en `python` de la forma siguiente:

```python
limit_seq(((n**2-n+4.)**(0.5))-((n**2+2.)**(0.5)),n)
```

```
## -oo
```

y el límite resuelto en `Wolfram Alpha` se puede ver en el enlace siguiente: [![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit+of+Sqrt%5Bn%5E2-n%2B4%5D-Sqrt%5Bn%5E2%2B2%5D+when+n+tends+to+infinity)

</div>


## Otros límites relacionados con el número $e$

<l class="prop">**Proposición** </l>

Sea $a_n$ una sucesión tal que $a_n \rightarrow \infty$. Entonces 
$$
\lim \left( 1 + \dfrac{1}{a_n}\right)^{a_n} = e
$$

## Otros límites relacionados con el número $e$

<div class="dem">**Demostración**

Recordemos, en primer lugar, que dado un número real $\beta$, el mayor entero  que es menor que $\beta$ se llama *parte entera* de $\beta$ y se denota por $\lfloor \beta \rfloor$.

Consideremos, en primer lugar que $a_n \rightarrow +\infty$. Sea $\beta_n = \lfloor a_n \rfloor$, dado que $\beta_n \leq a_n \leq \beta_n +1$, tendremos que 
$$
1 + \dfrac{1}{\beta_n +1} \leq 1+ \dfrac{1}{a_n} \leq 1+ \dfrac{1}{\beta_n}
$$
y, por lo tanto,
$$
\left(1 + \dfrac{1}{\beta_n +1} \right)^{\beta_n} \leq \left(1 + \dfrac{1}{\beta_n +1} \right)^{a_n} \leq \left( 1+ \dfrac{1}{a_n}\right)^{a_n} \leq \left( 1+ \dfrac{1}{a_n}\right)^{a_n +1} \leq \left( 1+ \dfrac{1}{\beta_n} \right)^{\beta_n +1}
$$
</div>

## Otros límites relacionados con el número $e$ (2)

<div class="dem"> **Demostración** (Continuación)

Ahora, dado que cada $\beta_n$ es un número natural y que 
$$ 
\left(1 + \dfrac{1}{\beta_n +1} \right)^{\beta_n} =\dfrac{\left(1 + \dfrac{1}{\beta_n +1} \right)^{\beta_n +1}}{1 + \dfrac{1}{\beta_n +1} } \quad \text{ y } \left( 1+ \dfrac{1}{\beta_n} \right)^{\beta_n +1} = \left( 1+ \dfrac{1}{\beta_n} \right)^{\beta_n}\left( 1+ \dfrac{1}{\beta_n} \right)
$$
resulta que las dos sucesiones son subsucesiones de la sucesión $\left( 1+ \dfrac{1}{n} \right)^{n}$ dividida y multiplicada, respectivamente, por sucesiones que tiene límite $1$ y, por lo tanto, las dos tienen el mismo límite: $e$.

En definitiva:
$$
\lim \left( 1 + \dfrac{1}{a_n}\right)^{a_n} = e
$$
 Consideraciones análogas, sirven para el caso que  $a_n \rightarrow -\infty$
</div>   


## Otros límites relacionados con el número $e$ (2)

<l class="prop"> **Proposición** </l>

Sean $x_n$ una sucesión tal que $x_n \rightarrow x$ y $a_n$ tal que $a_n \rightarrow \infty$. Entonces
$$
\lim \left( 1 + \dfrac{x_n}{a_n}\right)^{a_n} = e^x
$$
<div class="dem"> **Demostración**

Sea $b_n = \dfrac{a_n}{x_n}$. Como $b_n \rightarrow \infty$, con esta notación tendremos que
$$
\lim \left( 1 + \dfrac{x_n}{a_n}\right)^{a_n} = \left( \lim \left( 1 + \dfrac{1}{b_n}\right)^{b_n} \right)^{x_n} = e^{\lim x_n} = e^x
$$
</div>

## Otros límites relacionados con el número $e$ (3)

<l class="prop"> **Proposición** </l>

Sean $a_n$ y $b_n$ tales que $a_n \rightarrow 1$ y $b_n \rightarrow \infty$. Entonces
$$
\lim a_n ^{b_n} = e^{\lim (b_n(a_n-1))}
$$
<div class="dem"> **Demostración**

Dado que $a_n \rightarrow 1$, podemos poner $a_n = 1+ \delta_n$, con $\delta_n \rightarrow 0$. Ahora, si $x_n=\delta_n b_n = (a_n-1)b_n$, tendremos que
$$
\lim a_n ^{b_n} =  \lim (1+\delta_n)^{b_n} = \lim \left(1 +\dfrac{x_n}{b_n} \right)^{b_n} = e^{\lim x_n } = e^{\lim (b_n(a_n-1))}
$$


</div>

## Indeterminaciones del tipo $1^{\infty}$

Para este tipo de indeterminaciones sirven cualquiera de los dos resultados anteriores:

<div class="example"> 
**Ejemplo **

Calcular el $\lim_{n \rightarrow \infty} \left( \dfrac{n+2}{n-3} \right) ^{\dfrac{2n-1}{5}}$

Se trata de una indeterminaciópn del tipo $1^\infty$, puesto que si $a_n = \dfrac{n+2}{n-3}$ y $b_n= \dfrac{2n-1}{5}$, entonce $\lim a_n=1$ y $\lim b_n = \infty$, por lo tanto, podemos aplicar el resultado anterior, es decir calculamos el 
$$
\lim b_n(a_n-1)=\lim \dfrac{2n-1}{5}\cdot \left(\dfrac{n+2}{n-3} -1 \right) = \lim \dfrac{(2n-1)(n+2-n+3)}{5(n-3)}=2
$$
y, por lo tanto

$$
\lim_{n \rightarrow \infty} \left( \dfrac{n+2}{n-3} \right) ^{\dfrac{2n-1}{5}} = e^2
$$
</div>

## Indeterminaciones del tipo $1^{\infty}$
<div class="example"> 

El límite anterior en `python` se resolvería de la forma siguiente:

```python
limit_seq(((n+2)/(n-3))**((2*n-1)/5),n)
```

```
## exp(2)
```
y en el enlace siguiente hay la resolución usando `Wolfram Alpha`:
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit+of+%28%28n%2B2%29%2F%28n-3%29%29%5E%28%282n-1%29%2F5%29+when+n+tends+to+infinity)

</div>



## Sucesiones definidas en forma recurrente (5)

<div class="example"> **Ejemplo** 

Sea $a>0$, definimos la sucesión $\{a_n \}$ de la forma $a_1= \sqrt{a}$, $a_n = \sqrt{a+a_{n-1}}$. Calcula $\lim_{n \rightarrow \infty} a_n$.

La sucesión es creciente, puesto que $a_1 = \sqrt{a} < \sqrt{a+\sqrt{a}} =a_2$ y, si $a_{n-1} < a_{n}$, entonces, $a + a_{n-1} = a_n^2 < a_{n+1}^2 = a + a_{n}$, es decir $a_n <a_{n+1}$.

Además, la sucesión está acotada por $a+1$, puesto que es  $a_n^2 =a + a_{n-1}$, es decir $a_n = a + \dfrac{a_{n-1}}{a_n} < a+1$, dado que la sucesión es creciente y, por lo tanto, $\dfrac{a_{n-1}}{a_n} <1$.

Es decir, se trata de una sucesión monótona creciente y, por lo tanto, tiene límite, sea $l= \lim_{n \rightarrow \infty} a_n$. Aplicando la definición de la recurrencia y las propiedades aritméticas del límite, tendremos que
$\lim a_n^2 =  a+ \lim a_{n-1}$, és decir $l^2 =a +l$ y por lo tanto $l$ es una de las soluciones de esta ecuación de segundo grado, como una de ellas, $\dfrac{1-\sqrt{1+4a}}{2}$, es negativa y todos los términos de la sucesión son positivos, el límite buscado será la otra solución, es decir

$$
l=\dfrac{1+\sqrt{1+4a}}{2}
$$

</div>

## Sucesiones definidas en forma recurrente (5)

<div class="example"> 
**Ejemplo** 

En el enlace siguiente se pueden ver los primeros términos para de la sucesión $a_n$ para $a=2$ usando `Wolfram Alpha`:
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=x%281%29%3Dsqrt%282%29%2C+x%28n%2B1%29%3Dsqrt%282%2Bx%28n%29%29)
observando que el límite de la misma tiende hacia $2$.

En la misma web, se puede cambiar el 2 por otro valor de $a$ para ver lo qué ocurre. Por ejemplo para $a=3$, tendríamos:
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=x%281%29%3Dsqrt%283%29%2C+x%28n%2B1%29%3Dsqrt%283%2Bx%28n%29%29)
</div>

## Sucesiones recurrentes (6)

<div class="example"> **Ejemplo**

Calcular, si existe, el  $\lim_{n \rightarrow \infty} a_n$, donde $a_n$ es la sucesión definida por $a_1=2$, $a_{n+1} = \frac{1}{3-a_n}$.

En primer lugar, la sucesión es decreciente, puesto que $2=a_1 \geq a_2= 1$ y, si $a_{n-1} \geq a_n$, entonces es $3-a_{n-1} \leq 3-a_n$, y por lo tanto $a_n = \frac{1}{3-a_{n-1}} \geq \frac{1}{3-a_n}= a_{n+1}$ y, en consecuencia, por el Principio de Inducción, es $a_n \geq a_{n+1}$, para todo $n \in \mathbb{N}$. 

Todos los términos de la sucesión son positivos, ya que es decreciente y el primero es $2$, por lo tanto está acotada inferiormente, lo que significa que tiene límite, sea este $l$. Aplicando la propiedades aritméticas de los límites tenemos que $\lim a_n = \frac{1}{3-\lim a_{n-1}}$, es decir $l =\dfrac{1}{3-l}$, por lo que 
$$
\lim a_n = \dfrac{3-\sqrt{5}}{2}
$$

dado que la otra solución de la ecuación de segundo grado resultante es mayor que todos los términos de la sucesión, y esta es decreciente.


</div>



## Sucesiones recurrentes (7)

<div class="example"> 
Acabamos de ver que si $a_1=2$, $a_{n+1} = \frac{1}{3-a_n}$, entonces $\lim a_n = \frac{3-\sqrt{5}}{2}$. El gràfico siguiente muestra los $25$ primeros términos de esta sucesión y lo rápida que es la convergencia.

<img src="CorreccionsTema2Arnau_files/figure-html/unnamed-chunk-10-1.png" width="720" />

</div>

## Sucesiones recurrentes (8)


```python
from sympy import * 

import math  
import matplotlib.pyplot as plt

l=((3.-math.sqrt(5.))/2.)

a=[0,2]+list(range(2, 26))

#an=2
for k in range(25):
  a[k+1]=1/(3.-a[k])
  # print(a[k])

#print(l)
fig = plt.figure()
ax = plt.axes()
ax.plot(range(26), a)
```

## Sucesiones recurrentes (8)
<div class="example">
En el enlace siguiente se pueden ver la expresión explícita para $a_n$ usando `Wolfram Alpha`:
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=x%281%29%3D2%2C++x%28n%2B1%29%3D1%2F%283-x%28n%29%29)
observando que el límite de la misma tiende hacia $\frac{3-\sqrt{5}}{2}$.
</div>



## Ejemplo 2 de aplicación del criterio del sandwich

<div class="example"> **Ejemplo**

Calcular el límite: ${\displaystyle \lim_{n \rightarrow \infty} \sum_{k=1}^n \dfrac{1}{ \sqrt {n^2+k}} = \lim_{n \rightarrow \infty} \left(\dfrac{1}{\sqrt{n^2+1}}+ \dfrac{1}{\sqrt{n^2+2}}+ \cdots+\dfrac{1}{\sqrt{n^2+n}}\right)}$

Aplicamos el criterio del sandwich. Puesto que, para todo $k \in \{1,2, \ldots, n\}$, tenemos
$$
\dfrac{1}{\sqrt{n^2+n}} \leq \dfrac{1}{\sqrt{n^2+k}} \leq \dfrac{1}{\sqrt{n^2+1}}
$$
por consiguiente:
$$
\dfrac{n}{\sqrt{n^2+n}} \leq \sum_{k=1}^n \dfrac{1}{\sqrt{n^2+k}} \leq \dfrac{n}{\sqrt{n^2+1}}
$$
Ahora, es fácil comprobar que ${\displaystyle \lim_{n \rightarrow \infty} \dfrac{n}{\sqrt{n^2+n}} =1= \lim_{n \rightarrow \infty} \dfrac{n}{\sqrt{n^2+1}}}$.


</div>

## Ejemplo 2 de aplicación del criterio del sandwich

<div class="example"> 
Por lo tanto
$$
\lim_{n \rightarrow \infty} \sum_{k=1}^n \dfrac{1}{\sqrt{n^2+k}} =1
$$


El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5BSum%5B1%2FSqrt%5Bn%5E2%2Bk%5D%2C%7Bk%2C1%2Cn%7D%5D%2Cn-%3EInfinity%5D)
</l>
</div>



## El criterio de Stolz

<l class="prop">**Proposición. (Criterio de Stolz)**</l>

Sea $\{a_n\}_{n \in \mathbb{N}}$ una sucesión de números reales y sea $\{b_n\}_{n \in \mathbb{N}}$ una sucesión estrictamente creciente y no acotada (es decir que $\lim b_n = \infty$), tales que  
$$
\lim \dfrac{a_{n+1} -a_n}{b_{n+1}-b_n} = l
$$
Entonces existe el $\lim\dfrac{a_n}{b_n}$ y es igual a $l$.

## El criterio de Stolz (Demostración)

<div class="box">
<div class="important">
<i class="fa fa-dizzy"> Contenido muy técnico. </i>
</div>
</div>
<div class="dem">**Demostración**

Dado un $\epsilon >0$ existe un $N(\epsilon)$ tal que para todo $n>N(\epsilon)$ es
$$
l-\epsilon < \dfrac{a_{n+1} - a_n}{b_{n+1}-b_n} <l+\epsilon
$$
es decir, como $b_n$ es creciente, 

$$
(l-\epsilon)(b_{n+1}-b_n) < a_{n+1} - a_n <(l+\epsilon)(b_{n+1}-b_n)
$$

Sea ahora $k>N(\epsilon)$, 
$$
(l-\epsilon) \sum_{n=N(\epsilon)}^k (b_{n+1}-b_n) < \sum_{n=N(\epsilon)}^k (a_{n+1} - a_n) <(l+\epsilon)\sum_{n=N(\epsilon)}^k (b_{n+1}-b_n)
$$

se trata de sumas telescópicas, por lo que se reduciran a 

$$
(l-\epsilon)(b_{k+1}-b_{N(\epsilon)}) < a_{k+1} - a_{N(\epsilon)} <(l+\epsilon)(b_{k+1}-b_{N(\epsilon)})
$$
</div>


## Criterio de Stolz. (Demostración)

<div class="dem">

Dividimos ahora por $b_{k+1}>0$, y obtenemos

$$
(l-\epsilon) \left(1-\dfrac{b_{N(\epsilon)}}{b_{k+1}}\right) < \dfrac{a_{k+1}}{b_{k+1}} - \dfrac{a_{N(\epsilon)}}{b_{k+1}} <(l+\epsilon) \left(1- \dfrac{b_{N(\epsilon)}}{b_{k+1}}\right)
$$

Ahora, dado que $b_{k+1} \rightarrow \infty$, resulta que 
$\lim \dfrac{b_{N(\epsilon)}}{b_{k+1}} = 0 = \lim \dfrac{a_{N(\epsilon)}}{b_{k+1}}$ y, por lo tanto,  existe un $K$ tal que, para todo $k \geq K$, es
$$
l-\epsilon < \dfrac{a_{k+1}}{b_{k+1}} <l+\epsilon
$$

es decir, que 

$$
\lim \dfrac{a_k}{b_k} = l
$$


</div>



## Criterio de Stolz: Ejemplo 4

<div class="example"> 
**Calcular el $\lim_{n \rightarrow \infty} \sqrt[n]{n+2}$**

En primer lugar, tenemos que $\sqrt[n]{n+2} = (n+2)^{\frac{1}{n}}$, dado que las dos sucesiones son de términos positivos, podemos tomar logaritmos, $\log(n+2)^{\frac{1}{n}} = \dfrac{1}{n} \log(n+2)$ con lo cual reducimos el cálculo del limite propuesto al de $\lim \dfrac{\log(n+2)}{n}$, se trata de una indeterminación del tipo $\dfrac{\infty}{\infty}$. 

Al ser $n$ creciente y no acotada, podemos aplicar el criterio de Stolz, para obtener
$$
\lim \dfrac{\log(n+2)}{n} = \lim \dfrac{\log(n+2)- \log(n+1)}{n-(n-1)}= \lim \log \dfrac{n+2}{n+1} =0
$$
Por lo que 
$$
\lim_{n \rightarrow \infty} \sqrt[n]{n+2}= e^0=1
$$


El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%28n%2B2%29%5E%281%2Fn%29%2Cn-%3EInfinity%5D)
</l>
</div>




## Criterio de media aritmética: Ejemplos 

<div class="example"> **Ejemplo 2**

Calcula el límite:
$$
\lim_{n \rightarrow \infty} \dfrac{\log (n!)}{n}
$$

Dado que $\log (n!) = \log (1\cdot 2\cdot 3\cdots n)= \log (1)+ \log (2) + \log(3) + \cdots \log(n)$, la sucesión dada es la sucesión de medias aritméticas de $a_n = \log (n)$, por lo tanto, el límite pedido es
$$
\lim_{n \rightarrow \infty} \dfrac{\log (n!)}{n} =  \lim_{n \rightarrow \infty} \log (n) = + \infty
$$


El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5BLog%5Bn%21%5D%2Fn%2Cn-%3EInfinity%5D)
</l>

</div>

## Criterio de media aritmética: Ejemplos 

<div class="example"> **Ejemplo 3**

Calcula el límite:
$$
\lim_{n \rightarrow \infty} \left(\dfrac{2}{n}+\dfrac{3}{2n}+ \cdots \dfrac{n+1}{n^2} \right) = \lim \sum_{k=2}^{n+1} \dfrac{k}{(k-1)n}
$$

Es suficiente observar que $\dfrac{2}{n}+\dfrac{3}{2n}+ \cdots \dfrac{n+1}{n^2}= \dfrac{1}{n}\left(\dfrac{2}{1}+\dfrac{3}{2}+ \cdots +\dfrac{n+1}{n}\right)$, es decir que se trata de la sucesión de medias aritméticas de la sucesión de término general $a_n = \dfrac{n+1}{n}$, por lo tanto 
$$
\lim_{n \rightarrow \infty} \left(\dfrac{2}{n}+\dfrac{3}{2n}+ \cdots \dfrac{n+1}{n^2} \right) = \lim \sum_{k=2}^{n+1} \dfrac{k}{(k-1)n} = \lim_{n \rightarrow \infty} \dfrac{n+1}{n} = 1.
$$

El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5BSum%5Bk%2F%28%28k-1%29+n%29%2C%7Bk%2C2%2Cn%2B1%7D%5D%2Cn-%3EInfinity%5D)
</l>
</div>


## Criterio de la media geométrica: Ejemplos

<div class="example"> 
**Ejemplo 1**

Calcula el límite:
$$
\lim_{n \rightarrow \infty} \sqrt[n]{\dfrac{3}{2} \cdot \dfrac{6}{8} \cdots \dfrac{n^2+2}{2n^2}}
$$
La sucesión dada es la sucesión de medias geométricas de la sucesión $a_n = \dfrac{n^2+2}{2n^2}$, por lo tanto el límite pedido es
$$
\lim_{n \rightarrow \infty} \sqrt[n]{\dfrac{3}{2} \cdot \dfrac{6}{8} \cdots \dfrac{n^2+2}{2n^2}} = \lim_{n \rightarrow \infty} \dfrac{n^2+2}{2n^2} = \dfrac{1}{2}
$$
El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5B%28Product%5B%28i%5E2%2B2%29%2F%282+i%5E2%29%2C%7Bi%2C1%2Cn%7D%5D%29%5E%281%2Fn%29%2Cn-%3EInfinity%5D)
</l>


</div>


## Criterio de la media geométrica: Ejemplos

<div class="example"> **Ejemplo 2**

Calcula el límite:

$$
\lim_{n \rightarrow \infty} \sqrt[n]{\dfrac{(3+1)(3+2) \cdots (3+n)}{n!}}
$$

La sucesión dada es la sucesión de media geométricas de la sucesión de término general $a_n = \dfrac{3+n}{n}$, por consiguiente, el límite pedido es

$$
\lim_{n \rightarrow \infty} \sqrt[n]{\dfrac{(3+1)(3+2) \cdots (3+n)}{n!}} = \lim_{n \rightarrow \infty} \dfrac{n+3}{n} = 1
$$
El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5B%28Product%5B%28i%2B3%29%2C%7Bi%2C1%2Cn%7D%5D%2Fn%21%29%5E%281%2Fn%29%2Cn-%3EInfinity%5D)
</l>

</div>



## Ejemplos

<div class="example"> **Ejemplo**

**Calcular el $\lim \sqrt[n]{a^n+b^n}$, con $a>b>0$**

Apliquemos el criterio del cociente-raíz a la sucesión $\{a^n+b^n\}$ y dividimos numerador y denominador por $a^{n}$:

$$
\lim \sqrt[n]{a^n+b^n}=\lim_{n \rightarrow \infty} \dfrac{a^{n+1}+b^{n+1}}{a^n+b^n}= \lim_{n \rightarrow \infty} \dfrac{a+\left(\dfrac{b}{a} \right)^n b}{1+\left(\dfrac{b}{a} \right)^n} = a
$$

Puesto que $\lim_{n \rightarrow \infty} \left(\dfrac{b}{a} \right)^n =0$, al ser $a >b$.

El cálculo del límite anterior para $a=2$ y $b=5$ puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5B%282%5En%2B5%5En%29%5E%281%2Fn%29%2Cn-%3EInfinity%5D)
</l>
</div>

## Ejemplos

<div class="example"> **Ejemplo**

**Calcular el $\lim \dfrac{\sqrt[n]{n!}}{n}$.**

Apliquemos el criterio del cociente raiz a la sucesión $a_n=\left\{ \dfrac{n!}{n^n}\right\}$, 

$$
\lim \dfrac{\sqrt[n]{n!}}{n}=\lim \dfrac{a_{n+1}}{a_n} = \lim \dfrac{(n+1)! \cdot n^n}{(n+1)^{n+1} \cdot n!} = \lim  \left(\dfrac{n}{n+1}\right)^n = \dfrac{1}{e}
$$
El cálculo del límite anterior puede verse en el enlace siguiente de `Wolfram Alpha`
<l class="center">
[![](Images/wolfram.png)](https://www.wolframalpha.com/input/?i=Limit%5B%28n%21%29%5E%281%2Fn%29%2Fn%2Cn-%3EInfinity%5D)
</l>

</div>

