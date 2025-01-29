**Code:** https://colab.research.google.com/drive/14z1YjNlncKjPREOFbBaxJwkROOwGlb2S?usp=sharing 

> [!Lagrange Interpolation]
> * Avoids computing the Vandermonde matrix's inverse (which is costly: O($n_3$)) 
> * Allows us to get point estimations without computing polynomial coefficients first

Given n + 1 distinct points ($x_0$, $y_0$), ($x_1$, $y_1$), ... , ($x_n$, $y_n$)
$y = y_{0}L_{0}(x) + y_{1}L_{1}(x) + ... + y_{n}L_{n}(x)$

**Lagrange Polynomial Basis**
Each $L_{i}(x) = \prod^{n}_{j = 0, j \neq i}\frac{x - x_j}{x_{i} - x_{j}}$ and (i = 0, 1, ..., n)

> **Property:** $L_{i}(x_{i})= 1$ and $L_{i}(x_{j})= 0$ ($\forall j \neq i$)

**Proof**
$L_{i}(x_{i}) = \prod^{n}_{k = 0, k \neq i}\frac{x_{i} - x_{k}}{x_{i} - x_k}$ = $\prod^{n}_{k = 0, k \neq i}1 = 1$
$L_{i}(x_{j)}= \prod^{n}_{k = 0, k \neq i}\frac{x_{j} - x_{k}}{x_{i} - x_{k}} = 0 (\forall j \neq i)$ 
* Since k goes from 0 to n, the numerator in at least one fraction is 0, making the entire product 0
## Intuition

![[Pasted image 20250119133552.png]]
Vectors can be thought of as multiplying each bases vector by a certain factor

The same idea follows for Lagrange polynomial bases, where each $L_{i}(a)$ represents the case where $L_{i}(a) = 1$ at x = a, and $L_{i}(a)$ is 0 elsewhere...

Suppose you are given ($x_0$, $y_0$), ($x_1$, $y_1$), ($x_2$, $y_2$), the polynomial can be **decomposed** in this way:
![[Pasted image 20250119134031.png]]

> [!Lagrange Polynomial Base]
> Given n + 1 distinct data points ($x_0$, $y_0$), ($x_1$, $y_1$), ... , ($x_n$, $y_n$) a n-degree polynomial $L_{i}(x)$ is called a Lagrange basis whenever:
> 
$L_{i}(x_{i})= 1$ and $L_{i}(x_{j})= 0$ ($\forall j \neq i$)
## Example: Warm-up

> Construct a 3-degree polynomial function f(x) such that:
> f(x) = 0 at x = 1, 2, 4, and f(x) = 1 at x = 3

P(x) = (x - 1)(x - 2)(x - 4)
* To ensure that f(3) = 1 we normalise P(x) by dividing by P(3)

$f(x) = \frac{P(x)}{P(3)} = \frac{(x - 1)(x - 2)(x - 4)}{(3 - 1)(3 - 2)(3 - 4)} = \frac{-1}{2}(x - 1)(x - 2)(x - 4)$ 

## Lagrange Polynomial Basis construction

**Define a polynomial P(x) that is 0 at $x_0$, ... , $x_n$**
$P(x) = (x - x_{0)(x}- x_{1)...(x}- x_{i - 1})(x - x^{i + 2})...(x - x_{n)} = \prod^{n}_{j = 0, i \neq i}(x - x_j)$

**Ensure that $L_{i}(x_{i)} = i$ by normalising P(x), dividing by P($x_i$):**
![[Pasted image 20250119140040.png]]
## Lagrange Interpolation
* Finding the Lagrange Polynomial Basis is a product
* Obtaining and evaluating the Lagrange Polynomial (using the bases) is a sum

$y = \sum^{n}_{i = 0} y_{i} \prod^{n}_{j = 0, j \neq i} \frac{x - x_j}{x_{i} - x_{j}}$
* Two nested loops is only O($n^2$) time
## Example 
![[Pasted image 20250119130317.png]]

**Lagrange polynomial:** $y = 2L_{0} + 4L_{1} + 8L_{2}$
* $L_{0}(x)$ is a polynomial, which is 1 at x = 1 and 0 elsewhere
	* = $\frac{(x - 3)(x - 5)}{(1 - 3)(1 - 5)}$
* $L_1(x)$ is a polynomial, which is 1 at x = 3 and 0 elsewhere
	* = $\frac{(x - 1)(x - 5)}{(3 - 1)(3 - 5)}$
* $L_2(x)$ is a polynomial, which is 1 at x = 5 and 0 elsewhere
	* = $\frac{(x - 1)(x - 3)}{(5 - 1)(5 - 3)}$

$L_{0}(4)= \frac{-1}{8}$         $L_{1}(4) = \frac{3}{4}$          $L_{2}(4) = \frac{3}{8}$
$y(x) = 2L_{0}(x) + 4L_{1}(x) + 8L_{2}(x)$
$y(4) = 2\left(\frac{-1}{8}\right)+ 4\left(\frac{3}{4}\right)+ 8\left(\frac{3}{8}\right) = 5.75$

**Interpreting results**
![[Pasted image 20250119131434.png]]
The final result is the **linear combination** of the graphs produced by each bases

> [!Two-point form]
> When there are only two data points, Lagrange Polynomial reduces to "two-point form" of a straight line

**Points ($x_0$, $y_0$) and ($x_1$, $y_1$)**
![[Pasted image 20250119131908.png]] ![[Pasted image 20250119131916.png]]
1-degree Lagrange polynomial: $y = y_{0}L_{0} + y_{1}L_{1}$
$L_{0}(x) = \frac{x - x_1}{x_{0} - x_{1}}$ and $L_{1}(x) = \frac{x - x_0}{x_{1} - x_0}$

$y = \frac{x - x_1}{x_{0} - x_1}y_{0} + \frac{x - x_0}{x_{1} - x_0}y_{1}$ $= \frac{(x - x_1)y_{0} - (x - x_{1} + x_{1} - x_0)y_1}{x_{0} - x_1}$ $= \frac{(x - x_1)(y_{0} - y_1)}{x_{0} - x_{1}}+ y_1$
$\Rightarrow y - y_{1} = \frac{y_{0} - y_1}{x_{0} - x_{1}(x}- x_1)$ which is "two-point form" of a straight line
