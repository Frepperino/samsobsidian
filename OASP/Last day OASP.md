- Pros and cons
- Look at diagrams
- Compare different AR MA reflection coefficient exercises
- LPC
	- Since it is past samples it equates all-pole modeling. how does that relate to speech more exaclty
- Echo canceller
	- ERLE
	- Delay not usually in them in spite of that exam question
- Different assessment criteria
	- Misadjustment
	- Tracking
	- Convergence Rate
	- Robustness
	- Computational complexity
	- Memory requirement
- Fixpoint stuff
	- Exercise 7.1, 7.2
- Selecting delay in equalizer. (amount of z^-i)
- (Fourier filter coefficients, Lab 1)
- Skriva om till egenvärdesform för Jmin och w(n)
	- Skriva tillbaka: $w(n)=Q^T\nu+w_{0}$.
- Slower convergence if $w_{0}$ is at an axis for a low eigenvalue vs high eigenvalue.
- Solve problems with manual convolution
- $r_{u}(-k)=r_{u}(k)$, but $r_{du}(k) \neq r_{du}(-k)$.
- Classic solution for $\sin$ $\cos$ stuff, $\theta$ makes full period.
- $J_{min}=r_{d}(0)-r_{du}^Tw_{opt}=r_{d}(0)-w_{opt}^TR_{u}^Tw_{opt}$
- $P_{v}(e^{jw})=\sigma^2$ for WGN
- $SNR=\frac{power(s)}{power(v)}$
	- $power(y)=E[|y(k)|^2]$
	- $power(y)_{v}=E[|y(k)|^2]|_{s=0}$
	- $power(A\sin)=A^2$
- "Interference canceller" hints at narrowband =>
  narrowband is like a sine tone aka 1 frequency =>
  we only need to match phase and amplitude so p=2 per tone
- Derive sign lms, leaky lms from J
- We can show convergence by either $\nu(inf)$ or $E[w(inf)]$. See exc. 4.7d
- Pole plots x filter type x impulse response 
- Know the FDAF better
- Whenver equalizer is known, assume there is some D but that it could be 0
- CE 1:
	- If we plot $\ln(\nu(n))$ then $\tau$ is given by when it has decreased by 1, from start value.
	- $J-J_{min}=\sum\lambda_{i}v_{i}^2=\sum\lambda v(0)^2|1-\lambda_{i}|^{2n}$ 
	  => $\ln(J-J_{min}) \approx 2n(1-\mu \lambda_{min})$, when n is sufficiently big.
- CE 2:
	- The only diff between SD and LMS is removing E for R,p
	- In the z-plot there are as many zeros in origo as there are zeros before the first value in the FIR filter
- CE 3:
	- Remember for LMS: $\mu < \frac{2}{Mr(0)}=\frac{2}{Mvar(u)}$
- CE 4 (Fast LMS):
	- $\gamma=1$ means no normalization
	- If P(0) very wrong it takes a while for it to reach the right solution, just as with wrong w(0).
	- Normalization in Fast LMS and NLMS is goated for colored noise. This is because white noise is just diag($\sigma^2$), so its a uniform bowl where LMS is okay, but with colored noise it gets elongated, so normalization is more important.
	- **Normalization is more important the more elongated the bowl, aka the bigger the eigenvalue spread**.
	- Fast LMS benefits by independent mode coefficients as it during certain repeat signal state changes (e.g. speech) learns for certain modes and remebers it through silent-modes.
	- Block and Fast LMS have a latency of L-1.
	- With the prediction error filter power from u defintion. just explain that the reminaing power is just from the noise, so P2 = sigma^2 and then do the reverse.
	- det d'r med attt valjsa s1 ,s2 ,s3
- CE 5 (RLS vs LMS):
	- For big eigenvalue sprreads RLS is good because LMS very bad due to half pipe.
	- RLS has no misadjustment only if $\gamma=1$ and stationary signal. 
- Slides:
	- Unconstrained FDAF (gradient estimation based on circular convolution)
		- Fast calculations
		- Larger misadjustment
		- Takes twice as many iterations to reach the same misadjustment, due to poor gradient estimation
		- Does not converge to ward Wiener solution

Todo:
- Read through or redo exercises
- Memorize and repeat whats needed
- Redo exams

compare those matched pair AR, MA, Prediction error filter and stuff, and also with prediction filter

Redo:
- Exam 2015
	- 5b