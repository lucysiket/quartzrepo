**Recap:** PAA uses a 0-order polynomial for each segment which may lose trend information, whereas PLA uses 1-order polynomials for each segment

> [!Piecewise linear approximation]
> A dimensionality reduction method used to approximate a time series with line segments.
> 
> Given **N segments** and **time series X** = $X_{1}, ... , x_{n}$ the PLA representation splits X into **N equisized segments: Y** = ($y_{1}, ... , y_{N}$)
> 
> Each **ith segment** ($y_{i} = (a_{i}, b_{i})$) has coefficients $a_{i}$ and $b_{i}$, representing the **best-fit line** in the ith segment:
> $\hat{y}_{t} = a_{i}(t - (i - 1)l) + b_{i}$     ($t \in [(i - 1)l + 1, il]$)
> where $l = \frac{n}{N}$ is the length of each segment

When n is divisible by N, $a_{i}$ and $b_{i}$ can be obtained using:
![[Pasted image 20250128174133.png]]

**When n is not divisible by N**
* When n is not divisible by N, PLA uses the same method as PAA to split X into N segments
* Let l = $\lfloor$ n/N $\rfloor$ and R = n Mod N
![[Pasted image 20250128180645.png]]

**Comparisons between PLA and PAA**
* For fairness in comparison, we keep the total number of coefficients the same, and compare N-segment PLA with 2N-segment PAA
* Because, for each segment representation, PLA requires two coefficients (a, b) whereas PAA requires only one (the mean)

![[Pasted image 20250128180922.png]]

**Example**
![[Pasted image 20250128174452.png]]

Find the best-fit line for the 1st segment
**Points:** (1, 2), (2, 2) and (3, 3) 

Let $a_{1}t + b_{1} = x$ be the equation for the 1st line segment	
![[Pasted image 20250128175305.png]]

 ![[Pasted image 20250128175658.png]]
 ![[Pasted image 20250128175717.png]]

Find the best-fit line for the 2nd segment
**Points:** (4, 7), (5, 9) and (6, 8)

Let $a_{2}(t - l) + b_{2} = x$ (l = 3) be equations for the 2nd segment:
![[Pasted image 20250128180252.png]]

![[Pasted image 20250128180258.png]]

![[Pasted image 20250128180313.png]]

Find the best-fit line for the 3rd segment
**Points:** (7, 7), (8, 6) and (9, 6)

Let $a_{3}(t - 2l) + b_{3} = x$ (l = 3) be the equation for the 3rd segment:
![[Pasted image 20250128180423.png]]

![[Pasted image 20250128180432.png]]

![[Pasted image 20250128180443.png]]

Find the best-fit line for the 4th segment
**Points:** (10, 4), (11, 5) and (12, 4)

Let $a_{4}(t - 3l) + b_{4} = x$ (l = 3) be the equation for the 4th segment:
![[Pasted image 20250128180535.png]]

![[Pasted image 20250128180541.png]]

![[Pasted image 20250128180548.png]]

**Final**
![[Pasted image 20250128175844.png]]