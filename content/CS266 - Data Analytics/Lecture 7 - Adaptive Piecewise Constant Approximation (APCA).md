> [!Adaptive piecewise constant approximation]
> ![[Pasted image 20250126153410.png]]
> * An adaption of PAA, allowing segments to be of variable length
> 
> Given N segments, time series X = ($x_{1}, ... ,  x_{n}$), its APCA is represented as Y = ($y_{1}, ... , y_{N}$), with each ith segment $y_{i}$ (i = 1, ... , N) defines as **$y_{i} = [v_{i}, r_{i}]$** where:
> * $v_{i}$ = **Mean** value of data points in the ith segment
> * $r_{i}$ = the **right endpoint** of the ith segment
## APCA algorithm

> [!Algorithm]
> **Input:** X = time series, N = number of segments
> **Output:** APCA representation of X
> ![[Pasted image 20250126153545.png]]

**1 - If length of the time series is not a power of two, pad with zeros**
![[Pasted image 20250126153621.png]]

**2 - Perform the Haar Discrete Wavelet Transform (DWT) on X**
![[Pasted image 20250126153915.png]]
* This is why the length of time series needs to be a power of 2
* Pair of elements of the time series, and take the mean of the pairs
* Keep doing this until you only have one element
	* Make a note of the **difference** of each element between its parents (for which it is the mean of)
* **The coefficients are:** the final mean, then the **differences** on each level of the tree, from left to right

**3 - Keep top-N (N is number of segments) Haar coefficients with the largest normalised magnitude, and zero out the remaining ones**

![[Pasted image 20250126154212.png]]
* We scale each **difference** by $\sqrt{2}$ - this can be any value but its convention to use $\sqrt{2}$
* Each layer is scaled by a power of $\sqrt{2}$ - the bottom layer is scaled by a power of 0, and the power increases as you go up
	* This is because the root is the **most important** value, and as you go up, the values become less important
* We keep 4.5, 1, -1, because they are the top 3 normalised values: 4.5, $\frac{1}{\sqrt{2}}$ and $\frac{-1}{\sqrt{2}}$ becomes 4.5, $\frac{1}{\sqrt{2}}$ and $\frac{1}{\sqrt{2}}$ when you take the **absolute** value of them 
* We zero out the rest of the terms

**4 - Reconstruct approximation of X from the top-N (N is number of segments) Haar coefficients**

![[Pasted image 20250126155314.png]]
* Create this tree using C', where the root is C'[0] next to C'[1] (4.5 and 0). The rest of the tree is the rest of elements in C', add them from left to right as you go up the levels of the tree
* Start at the bottom: 4.5 $\pm$ 0 is 4.5 - so that is the value in the layer above
* On layer 1 to the left, 4.5 $\pm$ 1 is 5.5 and 3.5. To the right, 4.5 $\pm$ -1 is 3.5 and 5.5.
* At layer 2, do the same progress to get the resulting X'

**Overview**
![[Pasted image 20250126160117.png]]

**5 - If X' was padded with zeros, truncate it to the original length**

**6 - Replace approximate segment mean values with exact mean values**
![[Pasted image 20250126160311.png]]

**7 - While the number of segments > N, merge two adjacent segments with the least derivation in values**

![[Pasted image 20250126160439.png]]

![[Pasted image 20250126160451.png]]



