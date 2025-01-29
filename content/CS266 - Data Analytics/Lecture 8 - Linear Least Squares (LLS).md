> [!Linear least square]
> Used to find the **best-fitting line** (or hyperplane) for a given set of data points
> 
> ![[Pasted image 20250126161533.png]]
> **Aim:** Minimise the sum of the squared differences (residuals) between the **observed data** ($y_{i}$) and **predicted** values ($\hat{y}_i$)  
> 
> Residual($\epsilon_i$) = Observed ($y_i$) - Predicted ($\hat{y}_i$)
> 
> **Common use:** Regression analysis
> For estimating parameters describing the relationship between **dependent** variables (observed data, $y_{i}$) and **independent** variables (predictors, $x_i$)

> [!Formulation]
> Residual($\epsilon_i$) = Observed ($y_i$) - Predicted ($\hat{y}_i$)
> 
> **Goal:** Minimise the sum of the squared residuals (L) - find the (a, b) to do so
> ![[Pasted image 20250126161837.png]]
> 
> Assume the best-fitting line has the form $\hat{y} = a + bx$ and each predicted point ($x_{i}, y_{i}$) is on the line $\hat{y}_{i} = a + bx_{i}$

By taking the derivate of L with respect to b and a:
![[Pasted image 20250126162505.png]]
![[Pasted image 20250126162523.png]]
We can rearrange to get in terms of a and b

**Example**
![[Pasted image 20250126161912.png]]

**Assume the form:** $\hat{y} = a + bx$ where 
![[Pasted image 20250126162123.png]]

![[Pasted image 20250126162152.png]]
* Use the data points to find the averages needed for a and b

![[Pasted image 20250126162216.png]]
Substitute back into a and b to get the best-fitting line
## Linear algebra interpretation

![[Pasted image 20250126162825.png]]

![[Pasted image 20250126162821.png]] ![[Pasted image 20250126162942.png]]
Here we have y $\approx$ X $\times$ c = $\hat{y}$, meaning our best-fitting line should be roughly the same as the true **observed** y values
* We want to find c

**Consider X $\times$ c**
![[Pasted image 20250126163207.png]]
All linear combinations of the vectors 1 and x span the plane: span{1, x}:
![[Pasted image 20250126163305.png]]

**Consider X $\times$ c = $\hat{y}$**
Given $\hat{y}$, 1 and x, if there exists such a c where X $\times$ c = $\hat{y}$ then $\hat{y} \in$ span{1, x} (see above)
![[Pasted image 20250126163449.png]]

**Consider y $\approx$ X $\times$ c**
![[Pasted image 20250126163554.png]]
* e is the vector pushing the true y away from the vector plane
* Our goal is to minimise this vector e, so that our estimator $\hat{y}$ is **more accurate**

> We can **minimise** e by making it perpendicular to the plane, meaning we have to change the $\hat{y}$ vector accordingly

![[Pasted image 20250126163847.png]]
We can decompose y into y = $\hat{y}$ + e s.t. ||e|| is minimised

> The **dot product** of two **perpendicular** vectors is 0

![[Pasted image 20250126164229.png]]

**To make e perpendicular to the plane:**
Where ![[Pasted image 20250126164306.png]]

![[Pasted image 20250126164132.png]]
![[Pasted image 20250126164144.png]] ![[Pasted image 20250126164148.png]] ![[Pasted image 20250126164214.png]]

$X^{T}t = X^{T}Xc$
$c = (X^{T}X)^{-1}X^{T}y$
$\hat{y} = Xc = X(X^{T}X)^{-1}X^{T}y$

![[Pasted image 20250126164607.png]]

**Projection matrix**
$\hat{y} = X(X^{T}X)^{-1}X^{T}y = \hat{y} = Py$
Where $P := X(X^{T}X)^{-1}X^{T}$ is the projection matrix
* This matrix projects the **observed** y to an **estimator** $\hat{y}$ which minimises e by making it perpendicular to the plane

> [!Properties of projection matrix]
> **Symmetric**
> $P = P^{T}$
> 
> **Idempotent**
> * Means it is a square matrix that is unchanged when multiplied by itself
>   $P^{2} = P$
>   ![[Pasted image 20250126164955.png]]

**Example**
![[Pasted image 20250126165009.png]]

**Form of line:** $\hat{y} = X \times c \approx y$
where c = $(X^{T}X)^{-1}X^{T}y$

Using the data points:
![[Pasted image 20250126165056.png]]

c = $(X^{T}X)^{-1}X^{T}y = \begin{bmatrix}  1.68\\  0.95  \end{bmatrix}$
$\hat{y} = 1.68 + 0.95x$


