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

**Frequency Domain**
![[Pasted image 20250129144123.png]]
The **Fourier transform** maps the **time series** to the **frequency domain**

![[Pasted image 20250129145052.png]]
**Square wave** = $1 \times sin(x) + 0 \times sin(2x) + \frac{1}{3} \times sin(3x) + 0 \times sin(4x) + \frac{1}{5} \times sin(5x) + ...$
This specifies:
* **Frequency** - This is the **term number**, so frequency 3 represents $sin(3t)$ because this is the third term.
* **Amplitude** - This represents the term's **coefficient** (so amplitude $\frac{1}{3}$ would cause $sin(3t)$ to become $\frac{1}{3}sin(3t)$).

**But how do we find the coefficients for each sine or cosine components?**

> [!Fourier transform]
> (Time $\rightarrow$ Frequency)
> ## F($\omega$) = $\int^{+\infty}_{-\infty}X(t) \times e^{-i\omega t}dt$
> ## = F($\omega$) = $\int^{+\infty}_{-\infty}X(t) \times cos(\omega t) dt$ - $i \int^{+\infty}_{-\infty} X(t) \times sin(\omega t) dt$
> The **first term** is how X correlates to **cosine waves**. 
> The **second term** is how X correlates to **sine waves**.
> * F($\omega$) - This is the **frequency** against **amplitude** representation.
> 	
> 	![[Pasted image 20250129150130.png]]
> * $X(t)$ - This is the **time series** function we want to transform. Such as the square wave function.
>   
> 	![[Pasted image 20250129150053.png]]
> * $e^{-i\omega t}$ - This is the representation of **cosine** and **sine**, using the **exponential form** of complex numbers.
>   
> 	![[Pasted image 20250129150314.png]]

**Example**
