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
	This only processes periodic time series - these are data points that repeat at regular intervals.
	![[Pasted image 20250129141520.png]]
	**Fourier transform** extends **Fourier series** to handle **aperiodic** data - this does not exhibit a repeating pattern

