**Code:** https://colab.research.google.com/drive/1nL-nv5IYAqtmfIrNc3neXOKKoGc6atCh?usp=sharing

> [!Interpolation]
> * Data analysis method used to estimate unknown values between known values in a data set
> * Given a set of distinct discrete data points: ($x_0$, $x_0$), ($x_1$, $y_0$), ... , ($x_n$, $y_n$), **interpolation** will construct a **function** (usually a polynomial or smooth function) that:
> 	* Passes through these points
> 	* Estimates values of the function at intermediate points where data is not explicitly provided

**Why use interpolation?**
* Approximate missing data between measured points
* To generate smooth curved from discrete data
* To smooth transitions between points for visualizations

![[Pasted image 20250119103529.png]]

![[Pasted image 20250119103200.png]]

> **Interpolation** estimates the unknown value **within** the range of **given values**
> 	Used to fill in data gaps
> **Extrapolation** estimates the unknown value **outside** of this range
> 	Used to predict trends
## Types of interpolation

* **Linear interpolation** - Connects two points with a straight line. Is not smooth for multiple points
* **Polynomial interpolation** - A single polynomial connects all points
	* Eg: Lagrange and Newton interpolation
* **Spline interpolation** - Avoids oscillations by using multiple piecewise functions. Common in smooth curve fitting
## Polynomial Interpolation

![[Pasted image 20250119104124.png]]
A data set of **n + 1** points has **degree n** for **interpolation**

**Vandermonde matrix** - A matrix with a geometric progression in each row. These are always **invertible**
## Naive Polynomial Interpolation - Example

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
## Extending to n + 1 points

> [!Theorem]
> Given n + 1 distinct data points ($x_0$, $x_0$), ($x_1$, $y_1$), ... , ($x_n$, $y_n$), there exists a unique polynomial of degree n passing through each of these points

**General polynomial form:** $y = a_{0} + a_{1}x + a_{2}x^{2} + ... + a_{n}x^n$
![[Pasted image 20250119110218.png]]

**Rearrange:**
![[Pasted image 20250119110245.png]]
VA = Y    =>    A = V$^{-1}$Y
V is always a Vandermonde Matrix so is always invertible
![[Pasted image 20250119110416.png]]

**Problems:** 
* Finding V$^{-1}$ takes O($n^3$) time
* Once the coefficients of the polynomial have been determined, we need an efficient way to evaluate it to get the value of y at a given x

> [!Horner Method]
> A method of evaluating a polynomial efficiently, by reducing the number of required additions and multiplications
> 
> $a_{0} + a_{1}x + a_{2}x^{2} + ... + a_{n}x^{n}$ 
= $a_{0} + x(a_{1} + x(a_{3} + ... x(a_{n - 1} + xa_n)))$

**Example** $y = 2 + 5x + 4x^{2} +3x^3$ at $x = 8$ 
* **Naive method**: $y(8) = 2 + 5(8) + 4(8)(8) + 3(8)(8)(8)$
	* 3 additions and 6 multiplications
* **Horner method:** $y(8) = 2 + 8(5 + 8(4 + 8(3)))$
	* 3 additions and 3 multiplications

## Polynomial Interpolation Limitations
1) **Costly matrix inversion:** Finding the inverse of the Vandermonde Matrix is O($n^3$)
2) **No support for incremental updates:** When a new data point is found, the computation has to be done from scratch
3) **Must determine coefficients before estimations:** We need to determine coefficients {$a_i$} for the polynomial before evaluating new values at points

**Solutions**
* Lagrange Interpolation: For 1 and 3
* Newton Interpolation: For 2 and 3