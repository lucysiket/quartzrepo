![[Pasted image 20250122154844.png]]

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

**Using this rule** 
![[Pasted image 20250122155437.png]]

> [!Newton Forward Divided Difference Formula]
> $y = a_{0} + a_{1}(t \times h) + a_{2}(t(t - 1)h^{2}) + ... + a_{n}(t(t - 1) ... (t - n + 1)h^n)$
> Where $a_{0} = [y_{0}], a_{1} = [y_{0}, y_{1}], a_{2} = [y_{0}, y_{1}, y_{2}], ... , a_{n}= [y_{0}, y_{1}, y_{2}, ... , y_{n}]$

**Binomial coefficients**
![[Pasted image 20250122155720.png]]

![[Pasted image 20250122155732.png]]

> [!Newton Forward Divided Difference Formula]
> ![[Pasted image 20250122155840.png]]
## Forward difference
$\Delta^{n}(*)$ is the forward difference operator of order n

**1st order:** $\Delta y_{i} = y_{i + 1} - y_i$
**2nd order:** $\Delta^{2}y_{i} = \Delta y_{i+1} - \Delta y_i$
...
**nth order:** $\Delta^{n}y_{i} = \Delta^{n - 1}y_{i + 1} - \Delta^{n - 1}y_i$

![[Pasted image 20250122160258.png]]
When the points {$x_{0}, x_{1}, x_{2}, ...$} are equally spaced, the **Divided Difference** and **Forward Difference** have the following relationship:
![[Pasted image 20250122160402.png]]

## Newton Forward Difference Formula

> [!Newton Forward Divided Difference Formula]
> ![[Pasted image 20250122160448.png]]
> ![[Pasted image 20250122160454.png]]

## Example

![[Pasted image 20250122160515.png]]

$x = x_{0} + h \times t$    
$\Rightarrow 4 = 1 + 2t$
$\Rightarrow t = 1.5$

For **three points** the Newton forward difference formula has the form:
$y = y_{0} + \Delta y_{0}C^{1}_{t} + \Delta ^{2}y_{0}C^{2}_t$
![[Pasted image 20250122160918.png]]

## Summary

![[Pasted image 20250122161001.png]]



