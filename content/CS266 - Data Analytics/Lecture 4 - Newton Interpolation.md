**Limitation of Lagrange Interpolation**
When adding a new point to the data set, all the Lagrange basis need to be recomputed from scratch
	Each $L_{i}(x)$ depends on the entire set of interpolation points

> [!Newton Interpolation]
> * Allows incremental updates without recalculating the entire polynomial
> * The coefficients can be updated using the new point and its divided difference

Given n + 1 distinct data points ($x_0$, $y_0$), ($x_1$, $y_1$), ... , ($x_n$, $y_n$), the **Newton polynomial** is an n-degree polynomial, passing through these points with the form:
> $y = a_{0} + a_{1}(x - x_{0}) + a_{2}(x - x_{0})(x - x_{1}) + ... + a_{n}$$\prod_{i = 0}^{n - 1} (x - x_{i})$ 

Each coefficient $a_i$ is the i-th order divided difference:
$a_{0} = y_{0}$     $a_{1} = [y_{0}, y_{1}]$     $a_{2} = [y_{0}, y_{1}, y_{2}]$     ...     $a_{n} = [y_{0}, y_{1}, y_{2}, ... , y_{n}]$
## Divided difference
Generalise the concept of derivates for discrete data points

**1st order divided difference**
![[Pasted image 20250119143720.png]]
Given ($x_{0}, y_{0}$) and ($x_{1}, y_{1}$), the 1st order divided difference is \[$y_{0}, y_{1}$\] = $\frac{y_{0} - y_{1}}{x_{0} - x_{1}}$ 
	Formula for gradient/slope

**2nd order divided difference**
![[Pasted image 20250119143927.png]]
Given ($x_{0}, y_{0}$), ($x_{1}, y_{1}$) and ($x_{2}, y_{2}$)
* You can calculate the 1st order divided difference between points, then use the result of that to find the 2nd order divided difference

![[Pasted image 20250119144021.png]]

> [!nth order divided difference]
> The nth order divided difference of n + 1 distinct data points is:
> * Denotes as [$y_{0}, y_{1}, ... , y_n$] 
> * Defined recursively as $\frac{[y_{0}, y_{1}, ... , y_{n - 1}] - [y_{1}, y_{2}, ... , y_{n}]}{x_{0} - x_{n}}$

**Base case (0th order)**
\[$y_i$\] = $y_i$     (i = 0, 1, ... , n)

![[Pasted image 20250119144521.png]]
## Divided difference table
![[Pasted image 20250119145040.png]]
* Suppose you have a table with the result of \[$y_{0}, y_{1}, y_{2}$\] 
* If you add a new point ($x_{3}, y_{3}$), you can easily reuse the results of \[$y_{0}, y_{1}, y_{2}$\]  when calculating \[$y_{0}, y_{1}, y_{2}, y_3$\], saving on computation (see red)
	* This allows for efficient incremental evaluation

> [!Divided difference property 1]
> [$y_{0}, y_{1}, ... , y_{n}$] is symmetric (unordered)
> If $\sigma$: {0, 1, ... , n} $\rightarrow$ {0, 1, ... , n} is a permutation then
> * [$y_{0}, y_{1}, ... , y_{n}$] = [$y_{\sigma(0)}, y_{\sigma(1)}, ... , y_{\sigma(n)}$]
> * **Eg:** [$y_{0}, y_{1}, y_{2}$] =  [$y_{0}, y_{2}, y_{1}$] = [$y_{1}, y_{0}, y_{2}$] = [$y_{2}, y_{1}, y_{0}$]

> [!Divided difference property 2]
> [$y_{0}, y_{1}, ... , y_{n}$] can be expressed as the weighted sum of $y_{0}, y_{1}, ... , y_{n}$
> [$y_{0}, y_{1}, ... , y_{n}$] = $\Sigma^{n}_{i = 0}\frac{y_i}{\prod_{i \neq j}(x_{i} - x_j)}$
> **Eg:**
> ![[Pasted image 20250122145612.png]]
# Intuition

**1 distinct data point ($x_{0}, y_{0}$)**
![[Pasted image 20250122151221.png]]
The 0-degree Newton polynomial takes the form:
	$P_{0}(x) = a_{0}$ where $a_{0} = y_{0}$
For n = 0:
	$P_{0}(x)$ passing through ($x_{0}, y_{0}$) creates a horizontal line

**2 distinct data points ($x_{0}, y_{0}$) and ($x_{1}, y_{1}$)**
![[Pasted image 20250122151410.png]]
The 1-degree Newton polynomial takes the form:
	$P_{1}(x) = a_{0} + a_{1}(x - x_{0})$ where $a_{0} = y_{0}$ and $a_{1} = [y_{0}, y_{1}]$
**For n = 1:** Define $P_{1}(x)$ on top of the previous $P_{0}(x)$ as: $P_{1}(x) = P_{0}(x) + N_{1}(x)$
Determine form of $N_{1}(x)$:
	$P_{1}(x_{0}) = 0$ and $P_{0}(x_{0}) = 0$ so
	$P_{1}(x) = P_{0}(x) + N_{1}(x)$ $\Rightarrow$ 0 = 0 + $N_{1}(x_0)$ 
	$\Rightarrow$ $N_{1}(x_0)$ = 0 meaning $N_{1}(x)$ has a zero root $x_{0}$
	$\Rightarrow$ $N_{1}(x) = a_{1}(x - x_{0})$
Determine $a_{1}$
	We know $N_1$ so $P_{1}(x) = P_{0}(x) + a_{1}(x - x_{0})$
	Using $(x_{1}, y_{1}):$ $P_{1}(x_{1}) = P_{0}(x_{1}) + a_{1}(x_{1} - x_{0})$ 
	$\Rightarrow$ $y_{1} = y_{0} + a_{1}(x_{1} - x_{0})$
	$\Rightarrow$ $a_{1} = \frac{y_{1} - y_{0}}{x_{1} - x_{0}} = [y_{0}, y_{1}]$

**3 distinct data points ($x_{0}, y_{0}$) and ($x_{1}, y_{1}$) and $(x_{2}, y_{2})$**
![[Pasted image 20250122152334.png]]
The 2-degree Newton polynomial takes the form:
	$P_{2}(x) = a_{0} + a_{1}(x - x_{0}) + a_{2}(x - x_{0})(x - x_{1})$
For n = 2: Define $P_{2}(x)$ on top of the previous $P_{1}(x)$ as: $P_{2}(x) = P_{1}(x) + N_{2}(x)$
Determine form of $N_{2}(x):$
	Using ($x_{0}, y_{0}$): $P_{2}(x_{0}) = P_{1}(x_{0}) + N_{2}(x_{0})$
	$\Rightarrow y_{0} = y_{0} + N_{2}(x_{0})$
	$\Rightarrow N_{2}(x_{0}) = 0$
	Using ($x_{1}, y_{1}$): $P_{2}(x_{1}) = P_{1}(x_{1}) + N_{2}(x_{1})$
	$\Rightarrow y_{1} = y_{1} + N_{2}(x_{1})$
	$\Rightarrow N_{2}(x_{1}) = 0$
	$N_{2}(x)$ has two zero roots $x_0$ and $x_1$ so $N_{2}(x) = a_{2}(x - x_{0})(x - x_{1})$
Determine $a_{2}$:
	$P_{2}(x) = P_{1}(x) + a_{2}(x - x_{0})(x - x_{1})$
	Using ($x_{2}, y_{2}$):
	![[Pasted image 20250122152935.png]]

![[Pasted image 20250122152836.png]]
# Example

![[Pasted image 20250122150148.png]]
$y = a_{0} + a_{1}(x - 1) + a_{2}(x - 1)(x - 3)$
with $a_{0} = y_{0}$, $a_{1} = [y_{0}, y_{1}]$, $a_{2} = [y_{0}, y_{1}, y_2]$ 
![[Pasted image 20250122150533.png]]
# Taylor series

**Taylor Series** - Approximates a function y(x) near a single point x = z, using the high-order derivatives at the point z:
![[Pasted image 20250122150645.png]]

**Newton Interpolation** constructs a polynomial y(x) that passes through a **set of given points**, using high-order divided differences
![[Pasted image 20250122150735.png]]

**Taylor Series** is a *special case* of the **Newton Polynomial**. 
When all interpolation points {$x_{0}, x_{1}, x_{2}, ...$} are concentrated around a single point z, the **divided difference** in the Newton polynomial reduces to the derivates used in the Taylor series:
![[Pasted image 20250122151058.png]]

In this case, the Newton polynomial becomes:
![[Pasted image 20250122151120.png]]