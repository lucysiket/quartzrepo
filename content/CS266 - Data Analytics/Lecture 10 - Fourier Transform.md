 **Video:** https://youtu.be/spUNpyF58BY?si=2tDHFK4T-opb6P_p
 
 Originally introduced as a tool to **transform a waveform** (signal) between time (spatial) domain and frequency domain.
 This now has many **real-world applications**:
* JPEG image compressions - Discards high-frequency components.
* MP3 audio compression - Discards inaudible frequencies.

> [!Fourier transform]
> Fourier Transform (FT) decomposes a **time series** into the weighted sum of **sine** and **cosine** components
> 
> ![[Pasted image 20250129141030.png]] ![[Pasted image 20250129141037.png]]
> 
> FT determines the **coefficient** for each sine/cosine wave by converting a time series from time domain to frequency domain.

**Fourier series** - An expansion of a periodic function $f(x)$ in terms of an infinite sum of sines and cosines. 
	This only processes **periodic time series** - these are data points that repeat at regular intervals:
	![[Pasted image 20250129141520.png]]
	**Fourier transform** extends **Fourier series** to handle **aperiodic** data - this does not exhibit a repeating pattern.

**Square wave Fourier transform**
![[Pasted image 20250129143040.png]]
We can represent this **square wave** as an infinite series in terms of sines.
	**Square wave** = $sin(x) + \frac{1}{3}sin(3x) + \frac{1}{5}sin(5x) + \frac{1}{7}sin(7x) + ...$
	![[Pasted image 20250129143531.png]]
	You can see how adding more terms to the series brings it closer to looking like the square wave here: [Desmos Link](https://www.desmos.com/calculator/fsphlxe3c1) 
## Frequency Domain

![[Pasted image 20250129144123.png]]
The **Fourier transform** maps the **time series** to the **frequency domain**

![[Pasted image 20250129145052.png]]
**Square wave** = $1 \times sin(x) + 0 \times sin(2x) + \frac{1}{3} \times sin(3x) + 0 \times sin(4x) + \frac{1}{5} \times sin(5x) + ...$
This specifies:
* **Frequency** - This is the **term number**, so frequency 3 represents $sin(3t)$ because this is the third term.
* **Amplitude** - This represents the term's **coefficient** (so amplitude $\frac{1}{3}$ would cause $sin(3t)$ to become $\frac{1}{3}sin(3t)$).

## How do we find the coefficients for each sine or cosine components?

> [!Fourier transform]
> (Time $\rightarrow$ Frequency)
> ## F($\omega$) = $\int^{+\infty}_{-\infty}X(t) \times e^{-i\omega t}dt$
> ## = F($\omega$) = $\int^{+\infty}_{-\infty}X(t) \times cos(\omega t) dt$ - $i \int^{+\infty}_{-\infty} X(t) \times sin(\omega t) dt$
> The **first term** is how X correlates to **cosine waves**. 
> The **second term** is how X correlates to **sine waves**.
> * F($\omega$) - This is the **amplitude** at a given **frequency** (or term).
> 	
> 	![[Pasted image 20250129150130.png]]
> * $X(t)$ - This is the **time series** function we want to transform. Such as the square wave function.
>   
> 	![[Pasted image 20250129150053.png]]
> * $e^{-i\omega t}$ - This is the representation of **cosine** and **sine**, using the **exponential form** of complex numbers.
>   
> 	![[Pasted image 20250129150314.png]]
## Example

**How does a sine wave with frequency $\omega$ contribute to the square wave?**

![[Pasted image 20250129153111.png]]

Consider when **$\omega$ is even** (the even number terms, which are zeroed out): 2, 4, 6...

![[Pasted image 20250129153243.png]]

F($2$) = $\int^{+\infty}_{-\infty}X(t) \times sin(2t) dt$
F($4$) = $\int^{+\infty}_{-\infty}X(t) \times sin(4t) dt$

In $sin(2x)$ and $sin(4x)$, the **positively** correlated humps are coloured green, and the **negatively** correlated humps are coloured red. They are **equal** over each period.
	So, F($\omega$) = 0 for all even $\omega$

Consider when $\omega$ is odd
The number of **green humps** is 2 more than the number of **red humps** over each period. So, F($\omega$) > 0 for all odd $\omega$.
![[Pasted image 20250129160316.png]]
F($1$) = $\int^{+\infty}_{-\infty}X(t) \times sin(t) dt$ = $1$
F($3$) = $\int^{+\infty}_{-\infty}X(t) \times sin(3t) dt$ = $\frac{1}{3}$
F($5$) = $\int^{+\infty}_{-\infty}X(t) \times sin(5t) dt$ = $\frac{1}{5}$
## Time series decomposition

**Vector Space**
Given vector $v$ = $\begin{bmatrix} 2  \\ 4  \end{bmatrix}$, we can decompose it using the basis vectors $e_{1} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ and $e_{2} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$
	$v$ = $2 \cdot e_{1} + 4 \cdot e_{2}$ 
	Let $2$ (the coefficient of $e_{1}$) be denoted as <$v, e_{1}$>
	Let $4$ (the coefficient of $e_{2}$) be denoted as <$v, e_{2}$>

**Hilbert Space**

Given time series $X(t)$ with basis $1, sin(t), sin(2t), sin(3t), ... , cos(t), cos(2t), cos(3t), ...$

![[Pasted image 20250130115809.png]]

![[Pasted image 20250130115842.png]]
$X(t)$ is the sum of the basis $\times$ weights.
	FT changes the basis of time series in an infinite dimensional space (Hilbert)

> [!Inverse Fourier transform]
> (Frequency $\rightarrow$ Time)
> Denoted with $F = IFT(X)$ or $F = FT^{-1}(X)$
> 
> ## $X(t) = \frac{1}{2 \pi}\int^{+\infty}_{-\infty}F(\omega)e^{i \omega t}dt$

> [!Discrete Fourier transform]
> (Time $\rightarrow$ Frequency)
> Denoted with $F = DFT(X)$ 
> 	Takes $O(n^2)$
> 
> ## $F_{\omega} = \sum^{N - 1}_{t = 0}X_{t} e^{-i \frac{2 \pi \omega}{N}t}$ ($\omega = 0, 1, ... , N - 1$)
> 
> $F = FFT(X)$ - Fast Fourier Transform
> 	$O(n log n)$

> [!Inverse Fourier transform]
> (Frequency $\rightarrow$ Time)
> 
> ## $X_{t} = \frac{1}{N}\sum^{N - 1}_{\omega = 0}F_{\omega}e^{i \frac{2 \pi \omega}{N}t}$ ($t = 0, 1, ... , N - 1$)
> 
> $F = IDFT(X)$ or $F = DFT^{-1}(X)$
> $F = IFFT(X)$ or $F = FFT^{-1}(X)$

![[Pasted image 20250130121040.png]]
## Example

![[Pasted image 20250130121106.png]]

![[Pasted image 20250130121307.png]]
This uses the **Discrete Fourier Transform** formula: $F_{\omega} = \sum^{N - 1}_{t = 0}X_{t} e^{-i \frac{2 \pi \omega}{N}t}$
Now we will consider each t value, let t = $\omega$ 
	For $\omega = 0$, the power becomes 0, so it is the sum of each $X_t$ in the data set
	For $\omega = 1$, it becomes a weighted sum

![[Pasted image 20250130121713.png]]
Work out the values for the rest of the t (or $\omega$) values 

![[Pasted image 20250130121753.png]]
Take the magnitudes of these values - there are 4 values and the smallest magnitude is 2 (generated by $F_2$) so set this to 0, and keep the others (which are the 3 most significant)

![[Pasted image 20250130121918.png]]
![[Pasted image 20250130122033.png]]
Using the **Inverse Discrete Fourier Transform**, reconstruct the time series: $X_{t} = \frac{1}{N}\sum^{N - 1}_{\omega = 0}F_{\omega}e^{i \frac{2 \pi \omega}{N}t}$
	Using each t value from the data points, and the reduced Fourier coefficients
	The resulting list is the reconstructed time series
## Extension
**One feature for time series representation**
![[Pasted image 20250130122258.png]]

**Multi-feature representation**
![[Pasted image 20250130122327.png]]
	Less coefficients: (5) or (8) $\rightarrow$ (1) + (3)
	Lower bounding

![[Pasted image 20250130122455.png]]
![[Pasted image 20250130122506.png]]
