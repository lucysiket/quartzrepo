> [!dimension reduction]
> Reducing the dimension of a data feature set. In time series analysis, dimension can relate to the number of data points
> 
> **Benefits**
> ![[Pasted image 20250124122148.png]]
> * Avoid overfitting, ensuring the training model remains faster
> * Eliminate noise 
> * Compress the data and reduce space required
> 
> **Methods**
> ![[Pasted image 20250124122245.png]]
# Piecewise Aggregate Approximation (PAA)

> [!Piecewise Aggregate Approximation]
> * Dimensionality reduction technique for time series representation
> 1) Split the time series into equal segments
> 2) Take the mean value for each segment
> 
> Transforms a time series $X = (x_{1}, ... , x_n)$ into a reduced vector $Y = (y_{1}, ... , y_{N})$
> If n is dividable by N, each $y_{i} = (i = 1, 2, ... , N)$ is computed as:
> ![[Pasted image 20250124122514.png]]

**Example**
![[Pasted image 20250124122656.png]]

> [!Efficiency]
> Takes O(n) for a series of length n
> 
> Number of segments N affects space reduction and approximation accuracy:
> * **N = 1** - PAA reduces to the mean of the original time series
> 	* Highest space reduction but lowest accuracy
> * **N = n** - PAA is identical to original time series
> 	* No space reduction, but no accuracy lost

**n is not divisible by N**
* Means that n Mod N > 0
* Suppose n divided by N has quotient l = $\lfloor$ n/N $\rfloor$ and a remainder of R = n mod N
* The length of each segment:
 ![[Pasted image 20250124123747.png]]
 So the last R (remainder) segment are 1 bigger

![[Pasted image 20250124123609.png]]

> [!Limitations]
> ![[Pasted image 20250124123302.png]]
> * Uses a 0-order polynomial for each segment (average value) so could lose the trend information for each segment
> 	* Use a 1-order polynomial instead (PLA - Piecewise Linear Approximation)
> 	* ![[Pasted image 20250124123339.png]]
> * The segments are equal sized, and PAA is unable to identify segments of variable length
> 	* Use an adaptive version of PAA (APCA - Adaptive Piecewise Constant Approximation)
> 	* ![[Pasted image 20250124123441.png]]