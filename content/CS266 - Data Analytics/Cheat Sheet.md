**Naive Polynomial Interpolation**

![[Pasted image 20250119104017.png]]

**Determine the polynomial degree**
* We are given 3 data points so the polynomial is **degree 2** for **interpolation**
* $y = a_{0} + a_{1}x + a_{2}x^2$

**Using existing points**
$a_{0} + a_{1}(1) + a_{2}(1)^{2} = 2$          $a_{0} + a_{1}(3) + a_{2}(3)^{2} = 4$          $a_{0} + a_{1}(5) + a_{2}(5)^{2} = 8$

x values $\times$ unknown coefficients = y values
$\begin{bmatrix}  1 & 1 & 1^{2}\\  1 & 3 & 3^{2}\\ 1 & 5 & 5^2  \end{bmatrix}$ $\begin{bmatrix}  a_0 \\  a_1 \\ a_2   \end{bmatrix}$ = $\begin{bmatrix}  2 \\  4 \\ 8   \end{bmatrix}$
* The matrix of x values is a **Vandermonde matrix** so is invertible

coefficients = inverse(x values) $\times$ y values
$\begin{bmatrix}  a_0 \\  a_1 \\ a_2   \end{bmatrix}$ = $\begin{bmatrix}  1 & 1 & 1^{2}\\  1 & 3 & 3^{2}\\ 1 & 5 & 5^2  \end{bmatrix}^{-1}$ $\times$ $\begin{bmatrix}  2 \\  4 \\ 8   \end{bmatrix}$ = $\begin{bmatrix}  1.75 \\  0 \\ 0.25   \end{bmatrix}$

**Resulting polynomial:** $y = 1.75 + 0.25x^2$
**Answer:** $y = 1.75 + 0.25(4)^{2}= 5.75$

> [!Horner Method]
> $a_{0} + a_{1}x + a_{2}x^{2} + ... + a_{n}x^{n}$ 
= $a_{0} + x(a_{1} + x(a_{3} + ... x(a_{n - 1} + xa_n)))$

**Lagrange Interpolation**

> [!Lagrange Polynomial Basis]
> Each $L_{i}(x) = \prod^{n}_{j = 0, j \neq i}\frac{x - x_j}{x_{i} - x_{j}}$ and (i = 0, 1, ..., n)

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

**Newton Interpolation**

Given n + 1 distinct data points ($x_0$, $y_0$), ($x_1$, $y_1$), ... , ($x_n$, $y_n$), the **Newton polynomial** is an n-degree polynomial, passing through these points with the form:
> $y = a_{0} + a_{1}(x - x_{0}) + a_{2}(x - x_{0})(x - x_{1}) + ... + a_{n}$$\prod_{i = 0}^{n - 1} (x - x_{i})$ 

Each coefficient $a_i$ is the i-th order divided difference:
$a_{0} = y_{0}$     $a_{1} = [y_{0}, y_{1}]$     $a_{2} = [y_{0}, y_{1}, y_{2}]$     ...     $a_{n} = [y_{0}, y_{1}, y_{2}, ... , y_{n}]$

**Divided Difference**
![[Pasted image 20250119145040.png]]

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


![[Pasted image 20250122150148.png]]

$y = a_{0} + a_{1}(x - 1) + a_{2}(x - 1)(x - 3)$
with $a_{0} = y_{0}$, $a_{1} = [y_{0}, y_{1}]$, $a_{2} = [y_{0}, y_{1}, y_2]$ 

![[Pasted image 20250122150533.png]]

**Newton Forward Difference Formula**
Equally spaced points

> [!Equally spaced points]
> When points {$x_{0}, x_{1}, x_{2}, ...$} are equally spaced we have:
> * $x_{i} = x_{0} + i \times h$ where (i = 0, 1, 2, ...)
> 
> ![[Pasted image 20250122155004.png]]
> 
> We can replace i with **any real number** 
> * $x = x_{0} + t \times h$ where ($t \in \mathbb{R}+$)
> 
> Then we get:
> * $x - x_{i} = (x_{0} + t \times h) - (x_{0} + i \times h)$
> * $\Rightarrow t \times h - i \times h$
> 
> $x - x_{i} = (t - i)h$ ($\forall i$)

> [!Newton Forward Divided Difference Formula]
> $y = a_{0} + a_{1}(t \times h) + a_{2}(t(t - 1)h^{2}) + ... + a_{n}(t(t - 1) ... (t - n + 1)h^n)$
> Where $a_{0} = [y_{0}], a_{1} = [y_{0}, y_{1}], a_{2} = [y_{0}, y_{1}, y_{2}], ... , a_{n}= [y_{0}, y_{1}, y_{2}, ... , y_{n}]$

**Binomial coefficients**
![[Pasted image 20250122155720.png]]

![[Pasted image 20250122155732.png]]

> [!Newton Forward Divided Difference Formula]
> ![[Pasted image 20250122155840.png]]