Mini 1:

Mini 2:

Mini 3 - Stochastic Variables:
- Stochastic variable definition
- 1D:
	- Probability distribution function definition $F_{X}(x)=P(X \leq x) =\int f_{X}(x) \, dx$
	- Probability density function definition $f_{X}(x)=\frac{d}{dx}F_{X}(x)$
	- Expected value definition $E[X]=\int xf_{X}(x) \, dx=m_{X}$
	- Variance $V[X]=E[(X-m_{X})^{2}]=E[X^{2}]-m_{X}^{2}=\int (x-m_{X})^{2}f_{X}(x) \, dx$
- 2D:
	- $F_{z}(x)=F_{X,Y}(x,y)=P(X\leq x,Y\leq y)=\int \int f_{X,Y}(x,y) \, dx \, dy$
	- $f_{X,Y}(x,y)= \frac{ \partial  }{ \partial x \partial y }F_{X,Y}(x,y)=f_{Z}(z)$
- If X and Y are statistically independent, the pdf is seperable, $f_{X,Y}(x,y)=f_{X}(x)f_{Y}(y)$
	- Very strong assumption
- If uncorrelated, $E[XY]=E[X]E[Y]$
	- Weaker assumption
	- independent => uncorrelated
- Cross-covariance $r_{X,Y}=C[X,Y]=E[(X-m_{X})(Y-m_{Y})^*]=E[XY^*]-m_{X}m_{Y}^*$
	- Uncorrelated => $r_{X,Y}=0$.
- Correlation coefficient $\rho_{X,Y}=\frac{C[X,Y]}{\sqrt{ V[X]V[Y] }}$
	- $0 \leq \rho_{X,Y}\leq 1$

Mini lecture 4 - Stochastic Vectors:
- $x$ is a vector of realizations now
- $F_{x}(a_{1},a_{2},a_{3},\dots)=P(x_{1}\leq a_{1},x_{2}\leq a_{2}\dots)$
- If continuous sample space, $f_{x}(a_{1},\dots)=\frac{\partial^p P(x_{1}\leq a_{1},\dots)}{\partial a_{1},\dots \partial a_{p}}$
- If discrete $f_{x}(a_{1},\dots)=P(x_{1}=a_{1},\dots x_{p}=a_{p})$
- $m_{x}=E[x]=[E[x_{1}],\dots, E[x_{p}]]$
- $E[g(x)]=\int g(x)f(x) \, dx$
- Covariance matrix $R_{x,y}=C[x,y]=E[(x-m_{x})(y-m_{y})^*]=E[xy^*]-m_{x}m_{y}^*$
	- ![[Pasted image 20251106131735.png]]
	- Auto covariance $R_{x,x}=R_{x}$ is always symmetric or hermitian and positive semi-definite => egienvalues are real and non-negative
- Independence $f(x)=\prod f(x_{k})$
- Uncorrelated $E[x]=\prod E[x_{k}]$
- Conditional expectations
	- Conditional density
		- $f_{y|x=x_{0}}(y)=\frac{f_{x,y}(x_{0},y)}{\int f_{x,y}(x_{0},y) \, dy}=\frac{f_{x,y}(x_{0},y)}{f_{x}(x_{0})}$
	- Conditional expectation
		- $E[y|x=x_{0}]=\int yf_{y|x=x_{0}}(y) \, dy$
		- Simplified notation $E[y|x=x_{0}]=E[y|x]$
		- If x and y independent $E[y|x]=E[y]$
	- Conditional covariance matrix $C[y,z|x]=E[(y-m_{y|x})(z-m_{z|x})^*|x]$
	- Theorem gives:
		- $V[y]=E[V[y|x]]+V[E[y|x]]$
			- Good to remove conditional expectation
		- $C[y,z]=E[C[y,z|x]]+C[E[y|x],E[z|x]]$

Mini lecture 5 - Linear projections
- ![[Pasted image 20251106134323.png|500]]
- y is the future were trying to predict and x is the past that we know. Our best guess is $E[y|x]$, so we want to find this projection from y.
- We assume the range space $E[y|x]=a+Bx$ is linear.
	- Dont know what this is supposed to imply...
- We want to minimize the correlation of the the error vector e with our x.
	- $C[y-E[y|x],x]=0$.
- We can construct a concatenated vector $z=[x^T, y^T]^T$
	- $E[z]=[m_{x}^T,m_{y}^T]^T$
	- Covariance matrix ![[Pasted image 20251106134808.png]]
	- The optimal linear projection (i.e. the one that minimizes the prediction error variance among all linear projections):
		- $E[y|x]=m_{y}+R_{y,x}R_{x}^{-1}(x-m_{x})$
		- $V[e|x]=R_{y}-R_{y,x}R_{x}^{-1}R_{y,x}^*=E[V[y|x]]$
	- if x and y are normal distributed => e and x are independent, otherwise, theyre uncrorrelated

Mini Lecture 6 - Stochastic Processes
- Stochastic process definition
- $m_{x}(t)$ is the mean value of the process at $t$.
- $v_{x}(t)$ is the mean variance of the process at $t$.
- $r_{x}(t,s)=C[x_{t},x_{s}]$ is the dependence between realisations at different times
- We only consider WSS processes
	- Mean function $m_{x}(t)$ is constant and finite
	- Autocovariance $r_{x}$ only depends on lag, $r_{x}(k)$
	- The variance is finite $E[\lvert x_{t} \rvert^{2}]<\infty$
- We assume all processes are ergodic, i.e. we can estimate the characteristics of the process from a single realization.
- Autocovariance $r_{x}(k)$
	- Variance is $V[x_{t}]=r_{x}(0)$
	- $r_{x}(k)=r_{x}^*(-k)$
	- $r_{x}(0)\geq 0$
	- largest value at 0, $r_{x}(0) \geq \lvert r_{x}(k) \rvert$
- WGN
	- $r_{x}(k)$ is $\sigma^{2}$ if $k=0$, 0 otherwise
	- AWGN = (additive WGN), WGN we add simply
		- Often simply as $r_{y}(k)=r_{x}(k)+\sigma^{2}\delta(k)$

Mini Lecture 7 - Estimating the mean:
- We estimate $m_{x}$ by averaging samples, $\hat{m_{x}}$. Assumes, process is ergodic
	-  Is unbiased since $E[\hat{m}_{x}]=m_{x}$
	- Is consistent <=> asymptotically unbiased: $V[\hat{m}_{x}] \to 0, N \to \infty$
- if it is a Gaussian process with mean $m_{x}$ and ACF $r_{x}(k)$:
	- $\hat{m}_{x}$ is consistent, and $V[\hat{m}_{x}]\approx \frac{1}{N}\sum_{k=-\infty}^{\infty} r_{x}(k)$.
		- And if it is a WGN proccess $V[\hat{m}_{x}] \approx \frac{r_{x}(0)}{N}$
	- We can use this to determine confidence in the stimate. E.g. for a Gaussian process the 95% qunatule is 1.96, and thus, $\hat{m}_{x} \pm \frac{1.96\sigma_{x}}{\sqrt{ N }}$
		- This can be used for hypothesis tests, and also allows us to decide how many samples we need to prove a certain hypothesis

Mini Lecture 8 - Estimating the ACF:
- Unbiased $\hat{r}^u_{y}(k)=\frac{1}{N-k}\sum_{t=k+1}^N(y_{t}-\hat{m}_{y})(y_{t-k}-\hat{m}_{y})^*$
- Biased $\hat{r}^b_{y}(k)=\frac{1}{N}\sum_{t=k+1}^N(y_{t}-\hat{m}_{y})(y_{t-k}-\hat{m}_{y})^*=\frac{1}{N}\psi_{k}$
- Expected values:
	- Unbiased $E[\hat{r}_{y}^u(k)]=\frac{1}{N-k}e[\psi_{k}]=r_{y}(k)-V[\hat{m}_{y}]$
	- Biased $E[\hat{r}^b_{y}(k)]=\frac{1}{N}E[\psi_{k}]=r_{y}(k)-\frac{k}{N}r_{y}(k)-\frac{N-k}{N}V[\hat{m}_{y}]$ 
	- Thus both are biased
	- But in a zero mean process:
		- $E[\psi_{k}]=\sum_{t=k+1}^N=(N-k)r_{y}(k)$. Thus,
		- $E[\hat{r}^u_{y}(k)]=\frac{1}{N-k}E[\psi_{k}]=r_{y(k)}$
		- $E[\hat{r}^b_{y}(k)]=\frac{1}{N}E[\psi_{k}]=\frac{N}{N-k}r_{y}(k)$
		- Where unbiased version is actually unbiased and the biased version is only asymptotically unbiased.
- However the unbiased versions variance grows with the lags as seen by the demoninator shrinking with increasing k, resulting in very big variance for high lags.
- In comparison the biased version is constant, so even though it is less accurate, the actually value is scaled by N so the value and the variance will get smaller and smaller, **SO WE ALWAYS USE THE BIASED**.
- For WGN with variance $\sigma^{2}_{e}$:
	- $\hat{\rho}_{e}(k)=\frac{\hat{r}_{e}(k)}{\hat{r}_{e}(0)}$
	- Where we use the biased estimator for the ACF
	- $E[\hat{\rho}_{e}(k)]=0$
	- $V[\hat{\rho}_{e}(k)]=\frac{1}{N}$
	- $\hat{\rho}_{e}(k)$ is asymptotically Normal distributed. This implies that a 95% confidence interval can be formed as $\hat{\rho}_{e}(k) \approx 0 \pm \frac{2}{\sqrt{ N }}$ where we use 2 instead of 1.96 as it is for asymptotes any way
	- ![[Pasted image 20251106152847.png|500]]
		- This allows us to determine if samples are statiscially different from 0 or not.
		- I.e. if the estimation of our autocorrelation function are within $\pm \frac{2}{\sqrt{ N }}$ then they are not statistically different from 0 and we can conclude the process is white.
			- This assumes the ACF is Gaussian, which we need to investigate, otherwise this method doesnt hold.
		- We can allow one in 20 samples to be a little outside the confidence interval as it is a 95% confidence interval.
		- Rule of thumb: do not estimate correlations for lags over $\frac{N}{4}$. As strange correlations may appear suggesting there are longer dependencies but these are most likely finite data effects and are thus spurious and should be ignored.

Mini Lecture 8 - Estimating the convariance matrix:
- We want to estimate: ![[Pasted image 20251106154040.png|500]]
- This is toeplitz structure
- Two ways to estimate that we learn:
	- Toeplitz-structured estimate
		- We estimate $\hat{r}_{x}(k)$ (using biased) and then fill in the matrix.
		- Gives a toeplitz structure
		- We only estimate at most $\hat{R}_{x}$ of size $\frac{N}{4}$ in accordance with the previous mini lecture
	- Outer-product estimate
		- We split $x$ into M subvectors of length L, that overlap, and t hen we average them
		- $\hat{R}_{x}=\frac{1}{M}\sum_{t=1}^M\bar{x}_{t}\bar{x}_{t}^*$
		- $\bar{x}_{t}=[x_{t},\dots,x_{t+L-1}]^T$, where $t=1,\dots M=N-L+1$
		- The resulting $L\times L$ estimate is typically not Toeplitz.
		- It is the preferable way to estimate as it is the MLE.

Mini Lecture 10 - Power Spectral Density
- Is the fourier transform of the autocovariance function
	- $\phi_{y}(\omega)=\sum_{-\infty}^{\infty}r_{y}(k)e^{-i\omega k}$, $-\pi \leq \omega \leq \pi$
- Inverse transform recovers $r_{y}(k)$
	- $r_{y}(k)=\frac{1}{2\pi}\int _{-\pi}^{\pi}\phi_{y}(\omega)e^{i\omega k} \, d\omega$
		- $r_y(0)=\frac{1}{2\pi}\int _{-\pi}^{\pi}\phi_{y}(\omega) \, d\omega$
			- Integral over the full spectrum, i.e. the variance of the process $r_{y}(0)=E[\lvert y_{t} \rvert^{2}]$
- PSD is the density, it gives the spectral mass at that frequency
- PSD is real-valued and non-negative. For a real-valued process, the PSD is symmetric, and non-symmetric for complex-valued process.
- Examples:
	- The PSD of WGN is simply $\phi_{x}(\omega)=\sigma_{x}^{2}$
	- The PSD of $A\cos(\omega_{0}t+\phi)+w_{t}$ where $w_{t}$ is WGN.
		- ACF is $r(k)=\frac{A^{2}}{2}\cos(\omega_{0}k)+\sigma_{w}^{2}\delta _K(k)$
		- PSD using eulers formula is, $\phi(k)=\frac{A^{2}}{4}\delta_{D}(\omega-\omega_{0})+\frac{A^{2}}{4}\delta_{D}(\omega+\omega_{0})+\sigma_{w}^{2}$
			- $\delta_{D}$ is Dirac delta, the integral one.
		- Thus our PSD will have two spikes symmetrically at $w_{0}$ and a flat PSD from the WGN.
- If we have some weak assumption, then we can do a number of approximations and get the two natural estimators,
	- Periodogram, $\hat{\phi}_{y}^{p}(\omega)=\frac{1}{N}\left\lvert  \sum_{t=1}^N y_{t}e^{-i\omega t} \right\rvert^{2}$
	- Correlogram $\hat{\phi}_{y}^c(\omega)=\sum_{k=-N+1}^{N-1}\hat{r}_{y}(k)e^{-i\omega k}$
		- Once again biased estimator
		- This is basically truncated PSD, if we do not have the ACF estimator up until infinity.
	- Both are equivalent.
	- They are asymptotically unbiased, but not consistent.
		- The variance of the estimator depends on the PSD squared. => low variance where there is low power and vice versa.
		- Thus if we look at WGN periodogram it doesnt look flat.
			- To account for this we usually plot it in dB to make it more clear.
			- We also typically zero pad (append zeros at the end).
				- This doesn't add information, but it interpolates the estimate, and thus makes the PSD on a finer grid, which may reveal features that are not otherwise visible in the estimate.![[Pasted image 20251106163804.png|450]]
			- Windowing
				- Definition:
					- Periodogram, $\hat{\phi}_{y}^{p}(\omega)=\frac{1}{N}\left\lvert  \sum_{t=1}^N y_{t}e^{-i\omega t} \right\rvert^{2}=\frac{1}{N}\left\lvert  \sum_{t=-\infty}^{\infty}v_{t}y_{t}e^{-i\omega t}  \right\rvert$
					- Correlogram $\hat{\phi}_{y}^c(\omega)=\sum_{k=-N+1}^{N-1}\hat{r}_{y}(k)e^{-i\omega k}=\sum_{k=-\infty}^{\infty}w_{k}\hat{r}_{y}(k)e^{-i\omega k}$
					- In this case $v_{t}$, $w_{k}$ take the value 1 simply in the right frame. But we have moved it to sum over infinity and now we can adjust our windows as we want.
					- Multiplication in frequency domain means our windows are convolutions.
					- Different windows may widen the main lobe at the expense of removing the sidelobes.
					- ![[Pasted image 20251106164927.png|450]]
- Spectrogram:
	- Take the spectrum over time.

Mini lecture 11 - Filtering a process:
- Unfinished vs finished model error: ![[Pasted image 20251106194454.png|600]]
- Background: say we have a some data that is correlated to what were trying to predict, e.g. air temperature for heat consumption. How can we turn the air temperature as input into the head consumption as output, using a filter?
- We use linear, stable, causal, time-invariant filters.
	- linear: $\alpha x_{1}(t)+\beta x_{2}(t) \to \alpha y_{1}(t) + \beta y_{2}(t)$
	- stable: limited input -> limited output, wont explode
	- causal: will net generate output, before input is given
	- time-invariant: if input is delayed simply means output is delayed the same amount
	- If input is WSS / Gaussian, so is output
	- These filters can be expressed as a linear convolution, i.e. $y_{t}=\sum_{k=-\infty}^{\infty}h_{t-k}x_{k}=\sum_{k=-\infty}^{\infty}h_{k}x_{t-k}$
		- $m_{y}=E[\sum_{k=-\infty}^{\infty}h_{t-k}x_{k}]=m_{x}\sum_{k=-\infty}^{\infty}h_{k}=m_{x}H(0)$
		- Where $H(\omega)=\sum_{k=-\infty}^{\infty}h_{k}e^{-i\omega k}$ (Fourier Transform)
		- $H(0)$ is the gain of the filter
		- Thus the ACF may be expressed as, $y_{y}(k)=\sum_{m=-\infty}^{\infty}\sum_{l=-\infty}^{\infty}h^*_{m}h_{l}r_{x}(m+k-l)=r_{x}(k)*h_{k}*h^*_{-k}$
			- In the frequency domain this gives the PSD $\phi_{y}(\omega)=\lvert H(\omega) \rvert^{2}\phi_{x}(\omega)$
			- If we instead do this with the cross PSD using the cross covariance, we get: $\phi_{x,y}(\omega)=\sum^{\infty}_{k=-\infty}r_{x,y}(k)e^{-i\omega k}$, which equals $\phi_{x,y}(\omega)=H(\omega)\phi_{x}(\omega)$, which is equivalent to the Wiener-Hopf equations.
				- Theretically we could thus estimate the transfer function by $\hat{H}=\frac{\hat{\phi}_{x,y}}{\hat{\phi}_{x}}$, but in reality we can't estimate these spectral densities accurately enough for this to be usable.

Mini Lecture 12 - MA Processes
- $y_{t}=e_{t}+c_{1}e_{t-1}+\dots+c_{q}e_{t-q}=C(z)e_{t}$
	- $C(z)$ is a monic polynomials of order q, i.e. $C(z)=1+c_{1}z^{-1}+\dots+c_{q}z^{-q}$
	- $e_{t}$ is zero-mean WGN
- $m_{y}=E[C(z)e_{t}]=0$
- $r_{y}(k)=\sigma_{e}^{2}(c_{k}+c_{1}c_{k+1}+\dots+c_{q-k}c_{q})$ if $\lvert k \rvert \leq q$, $0$ otherwise
	- This makes us able to deduce the order and that it is an MA(1) process
- $\phi_{y}(\omega)=\sigma_{e}^{2}\lvert C(\omega) \rvert^{2}$
	- This comes from using the frequency domain PSD shown in the above mini lecture.
	- $C(\omega)$ means we replace each z with $e^{i\omega}$
	- The roots of $C(z)$ determine the locations of dips in the PSD. I.e., if our zeros are at some $\omega$ then we will have dips at that $\omega$ in the PSD, close to the unit circle, the deeper the dip
		- When we look at these plots it is usually from some absolut frequency between 0 and 0.5 which is the nyquist frequency, so if the dip is at 0.3, then that means $0.3*2\pi \approx1.9$
- For large N:
	- $E[\hat{\rho}_{y}(k)]=0$
	- $V[\hat{\rho}_{y}(k)]=\frac{1}{N}(1+2(\hat{\rho}_{y}^{2}(1)+\dots+\hat{\rho}_{y}^{2}(q)))$
		- $\hat{\rho}_{y}(k)$ for $\lvert k \rvert>q$ is asymptotically Normal distributed
	- The approximative 95% confidence interval for a MA(q) process, $\hat{\rho}_{e}(k) \approx 0 \pm 2\sqrt{\frac{1}{N}(1+2(\hat{\rho}_{y}^{2}(1)+\dots+\hat{\rho}_{y}^{2}(q)))}$, for $\lvert k \rvert\geq q + 1$
		- For white noise (q=0), this simplifies to $\hat{\rho}_{e}(k) \approx \frac{2}{\sqrt{ N }}$
	- Thus if we plot our ACF and we draw the lines $\frac{2}{\sqrt{ N }}$, then if we have only at $k=0$ a significant point (of course disregarding that 1 in every 20 from 95% interval) we have WGN, but if we see say 2 more at $k=1,2$ then it looks like a MA(2) process.
	- ![[Pasted image 20251110133554.png|850]]
	- In the image above we see that we have 4 statistically significant ACF peaks. Plotted in complex plane we see which frequencies they correspond to. We also see that the bigger frequency is close to the unit circle and thus creates a deeper dip.
		- Note we only see two dips as he only plots half the circle, otherwise we would see the other two dips on the other side of the symmetry.
	- A note on the plotted theoretical PSD. In general a parametric spectral estimate will be much better if the parameters are well estimated, compared to a non-parametric estimate. However, vice versa. So the best idea is to use a non-parametric estimate to start with and then examine it, to thereafter to build the parametric model when you're more sure about what you have.

Mini Lecture 13 - AR/ARMA
- AR: $A(z)y_{t}=y(t)+a_{1}y_{t-1}+\dots+a_{p}y_{t-p}=e_{t}$
	- $A(z)=1+a_{1}z^{-1}+\dots+a_{p}z^{-p}$
	- $e_{t}$ is zero-mean white process with $\sigma_{e}^{2}$ that drives the innovation
	- All zeros of the generating polynomial $A(z)$ are always within the unit circle for the AR process to be stable. Otherwise, it would amplify the output every time, exploding the output.
	- Note that an AR-process is a white nosie passed through a linear filter, i.e.,
	  $A(z)y_{t}=e_{t} \implies y_{t}=\frac{1}{A(z)}e_{t}$
	  Thus the spectrum may be expressed as, $\phi_{y}(\omega)=\frac{\sigma_{e}^{2}}{\lvert A(\omega) \rvert^{2}}$
	- The mean of an AR-process is zero: $E[y_{t}+\dots+a_{p}y_{t-p}]=E[e_{t}]=0$
	- Taking the auto-covariance of the process gives $r_{y}(k)+a_{1}r_{y}(k-1)+\dots+a_{p} r_{y}(k-p)=\sigma_{e}^{2}\delta_{K}(k)$
		- Called Yule-Walker equations
		- In matrix form with the first row and column of $R$ excluded, we get, $\hat{\theta}=-\hat{R}_{n}^{-1}\hat{r}_{n}$, $\hat{\theta}=[a_{1},\dots,a_{n}]^T$,
			- note that this excludes the first $a_{0}=1$
		- Levinson-Durbin might be looked at here but we skip it.
	- At the zeros of the polynomial and thus the zeros in the plane we will have peaks at those frequencies in the PSD, and the peak is higher the closer the zero is to the unit circle.
	- Compared to MA the ACF has a ringing behavior.
- ARMA: $A(z)y_{t}=C(z)e_{t}$
	- Any process can be approximated with an ARMA of sufficient size
	- The process is stationary if the roots of $A(z)=0$ lie within the unit circle
	- $m_{y}=0$
	- $\phi_{y}(\omega)=\frac{\lvert C(\omega) \rvert^{2}}{\lvert A(\omega) \rvert^{2}}\sigma_{e}^{2}$
	- $r_{y}(k)+\sum_{l=1}^{p} a_{l}r_{y}(k-l)=0$ for $\lvert k \rvert>q$
		- Note that this is the AR ACF as soon as the ACF of the MA has zeroed out. It is a bit more complicated for smaller k
	- Complicated to estimate the coefficients compared to AR due to the MA components.


Mini Lecture 14 - PACF (Partial ACF)
- ACF for MA will simply be 0 beyond the process order.
- For AR we use PACF:
	- $y_{t}=\phi_{k,1}y_{t-1}+\dots+\phi_{k,k}y_{t-k}+e_{t}$
		- $\phi_{k,l}$ is the lth (negative) AR coefficient of the kth order AR model.
		- PACF(k)=$\phi_{k,k}$
		- I.e. PACF at lag k is the least coefficient in a linear regression of $y_{t}$ on its previous k lags.
			- Equally $\text{PACF}(k)=\text{Corr}(e_{t},e_{t-k})$
	- If it is an AR(p) process then $\phi_{k,l}$ should be non-zero for $k\leq p$ and otherwise 0.
	- Asymptotically (for large N):
		- $E[\hat{\phi}_{k,k}]=0$
		- $V[\hat{\phi}_{k,k}]=\frac{1}{N}$
		- $\hat{\phi}_{k,k}$ is asymptotically Normal distributed (k > p)
		- The approximative 95% confidene interval for an AR(p) process can be expressed as, $\hat{\phi}_{k,k} \approx 0 \pm \frac{2}{\sqrt{ N }}$
	- Comparing PACF and ACF:
		- ![[Pasted image 20251111152936.png|450]]
		- Examples:
			- ![[Pasted image 20251111153410.png|500]]
				- ACF ringing => AR(2) suitable
			- ![[Pasted image 20251111153450.png|500]]
				- MA(3) is suitable
				- But one could also say AR(4) or AR(6)
				- In reality we're not looking the "truth", we want to decide what to work with.
					- AR models is better if we can get away with it. Easier to estimate coefficients. AR are more reliable. Even if it is truly a MA process, we can first try AR and see if that works.
						- In this case try AR(4), if not good enough, try AR(6), if not good enough, try MA(3)
						- Always start with small models. If we can get away with it, it is more robust, easier to estimate coefficients, and more reliable. If not good enough, we change the structure.
				- Even if we look at the 6th coefficient being significant we should not take the insignificant 3rd and 5th coefficient. This is because adding coefficients reduces other coefficients quality. 
			- ![[Pasted image 20251111154219.png|500]]
				- ACF ringing => Good starting point would be AR(7) with 5 coefficients. Maybe add MA coefficients later to see if ARMA.
			- ![[Pasted image 20251111154335.png|500]]
				- ACF is ringing => AR(4) suitable
			- ![[Pasted image 20251111154407.png|500]]
				- ACF is ringing => AR(3)
					- Truth is ARMA(2,1), but that doesn't mean we want to use that when modeling.
			- ![[Pasted image 20251111154615.png|500]]
				- ACF ringing => AR(2)

Mini Lecture 15 - Trends
- Two ways to handle trends:
	- Deterministic:
		- We assume the trend is a deterministic function
		- E.g. polynomial, periodic, or several periodicities
			- $y_{t}=\alpha+\alpha_{1}t+\dots \alpha_{k}t^k+x_{t}$
			- $y_{t}=\alpha_{0}+\alpha_{1}\cos (\omega t+\theta)+x_{t}$
		- Usually we would use prior knowledge here from e.g physics or chemistry.
		- Then we decide parameters.
		- And then we subtract it from $y_{t}$ to then model $x_{t}$
	- Stochastic:
		- We instead use an ARIMA (AR integrated MA) process of order (p,d,q)
			- $A(z)(1-z^{-1})^dy_{t}=C(z)e_{t}$
				- This differentiates $y_{t}$ recursively d times (usually 1 or 2)
				- Usually denoted $(1-z^{-1})y_{t}=\nabla y_{t}=y_{t}-y_{t-1}$
		- For more general cases we use SARIMA (Seasonal ARIMA)
			- $A(z)\mathcal{A}(z^s)\nabla ^d\nabla ^D_{s}y_{t}=C(z)\mathcal{C}(z^s)e_{t}$.
				- where $\nabla_{s} y_{t}=y_{t}-y_{t-s}$
				- s is the seasonal period, instead of $1$ as in ARIMA, and thus differentiates across s samples.
				- as we can see, we can have cycles both in the AR, $\mathcal{A}$, and MA, $\mathcal{C}$, part.
	- Example:
		- Increasing example:
		  ![[Pasted image 20251111160911.png]]
			- ![[Pasted image 20251111160802.png|550]]
				- A slowly decreasing ACF is an indicator that we should differentiate, or do something equivalent.
				- We can also seee however that it looks like an AR(3). In fact the AR(3) might incorporate this differentiation.
			- ![[Pasted image 20251111161420.png|550]]
				- If we do a one step ARIMA, we'll remove the trend and get a more ordinarily looking ACF. Here PACF gives an obvious AR(2).
				- So we would model this as $w_{t}=\nabla y_{t}$, where $w_{t}$ is AR(2). What we thus see is that we can write this together as an AR(3), which we observed above. I.e. ARIMA is just a way to get structure into the AR part.
				- At this point we have a ARIMA(2,1,0) 
		- Periodic example:
		  ![[Pasted image 20251111161931.png|550]]
			- Here we see a periodicity at lags 7 in ACF and a bit in PACF.
				- If we plotted the spectrum we'd see a peak correponding to periodicity of 7.
			- So we differentiate with a seasonal 7
			- ![[Pasted image 20251111162159.png|550]]
				- This looks better.
				- PACF ringing => Looks like an MA(3)
				- We would model this as a $\text{SARIMA}(0,0,3)_{7}$
		- Periodic example II:
		  ![[Pasted image 20251111162504.png]]
			- ![[Pasted image 20251111162535.png|500]]
				- Strong periodicity in 4 and 7
					- Suggests it won't be enough with 1 seasonal periodicity.
			- ![[Pasted image 20251111162635.png|450]]
				- We start with a fourth order,
				- Looks better, but we still have ringing behavior in both.
					- But now the strong periodicity is in 3. Which is because we removed the first 4 during this differentiation.
						- Once again one can do this by differentiation or by modelling with an AR(7) from the start including coefficients for 3 and 7
							- Hmmm why those numbers?
- Transforms:
	- Transforms instead solve the issue with stabilizing variance.
		- e.g. growing variability here ![[Pasted image 20251111163655.png]]
	- To solve this we maximize the log-likelihood, which gives us a transformation at its max.
		- The plot of it is called the Box-Cox plot
		- Most of the time we want log, and it is our first choice, it is only as a second alternative that we may look at other transforms.
	- ![[Pasted image 20251111164020.png|500]]
		- In this example we successfully reduced the variability, and then we used a seasonality of 12 to remove the trend.
		- In the end though the mean is still slightly above 0, so we subtract that. In the end we end up with the following $w_{t}$ to model,
		  $w_{t}=\nabla_{12}\sqrt{ y_{t} }-0.0681$
	- However, looking at the new ACF and PACF:
	  ![[Pasted image 20251111164404.png|500]]
		- We still see a strong dependence at lag 12 in the MA part (ACF) and the AR part (PACF).
			- This is very common!
		- Usually we will want some $c_{12}$ coefficient for the MA part and an a coefficient in the AR part, 
			- That these dependencies are left shows that my models is probably not that stable.
				- Thus maybe we may not want to use some $\nabla_{12}\sqrt{ y_{t} }=(1-y_{t-1})^{12}\sqrt{ y_{t} }$, but rather an $(1+a_{12}z^{-12})\sqrt{ y_{t} }$, where the $a_{12}$ component, that needs to be estimated, would probably be less than 1 to reduce these correlations

Mini Lecture 16 - Box-Jenkins Modeling
- Here we want to use related data in our prediction e.g. temperature outside to predict energy use
- Our first model to do this is the ARMAX processes: $A(z)y_{t}=B(z)x_{t-d}+C(z)e_{t}$
	- Note how we allow a delay d, so that the other processes can affect ours after some time has passed.
	- A and C are same as usual with ARMA
	- Note how the same A affects both x and e, this is a strong assumption. We relax this with Box-Jenkins model
- Box-Jenkins:
	- $y_{t}=\frac{B(z)}{A_{2}(z)}x_{t-d}+\frac{C_{1}(z)}{A_{1}(z)}e_{t}$
		- $A_{1}(z)=1+a_{1}^{(1)}z^{-1}+\dots+a_{p}^{(1)}z^{-p}$
		- $A_{2}(z)=1+a_{1}^{(2)}z^{-1}+\dots+a_{p}^{(2)}z^{-r}$ : external part
		- C order is q
		- $B(z)=b_{0}+b_{1}+z^{-1}+\dots+b_{s}^{-s}$
	- We want know how to determine (p,q,d,r,s):
		- We start with determining it for the external part, $B,A_{2}$. We do this by ignoring $A_{1},C_{1}$, so we have, $y_{t}=\frac{B(z)}{A_{2}(z)}x_{t-d}+\tilde{e}_{t}=H(z)x_{t-d}+\tilde{e}_{t}$.
			- $H(z)=\sum_{k=-\infty}^\infty h_{k}z^{-k}$
		- If we ignore the noise entirely we can rewrite $A_{2}(z)H(z)=B(z)z^{-d}$
			- Thus $h_{k}=0$ for $k<d$, so we can determine d!
			- We assume $r=0,1,2$ as it is very uncommon to have anything else.
				- r = 0: Then $A_{2}(z)=1$ and we will have a finite number of non-zero weights, so s is how many non-zero weights $h_{k}$ we have.
				- r=1: We have 1 pole. We get a decaying behavior starting at $d+s$, so we just look at where that happens.
				- r=2: The 2 poles will cause a damped exponential (roots are real) or sinusoidal behavior (complex roots), starting from $h_{d+s}$
		- Assuming $m_{y}=m_{x}=0$ and $x_{t}$ uncorrelated with $\tilde{e}_{t}$, and further if $x_{t}$ is a white process $\rho_{y,x}(k)=\frac{\sigma_{x}}{\sigma_{y}}h_{k}$
			- Thus for a white input, the impulse response can be estimated using the cross-correlation function directly.
			- Example: simple example ends up with exponentially decay at 0 for the cross-correlation function, so d=0 and r=1
		- But we can't assume that in general, however we can be smart, and make our input white anyway, with some cleverly placed extra transfer functions.
			- We form,
			  $\epsilon_{t}=\frac{A_{3}(z)}{C_{3}(z)}y_{t}=\frac{B(z)z^{-d}}{A_{2}(z)}w_{t}+\frac{A_{3}(z)}{C_{3}(z)} \frac{C_{1}(z)}{A_{1}(z)}e_{t}=H(z)w_{t}+v_{t}$
			  $\epsilon_{t}=\frac{A_{3}(z)}{C_{3}(z)}y_{t}$
			  $w_{t}=\frac{A_{3}(z)}{C_{3}(z)}x_{t}$
			- This allows us to estimate $H_{k}$ as $\rho_{\epsilon,w}(k)$, using the same rules as above to determine $r,d,s$
			- With the model orders "known", we form initial estimates of $B(z),A_{2}(z)$, by treating $\tilde{e}_{t}$ as white noise (this is not correct but it will give us an estimate).
			- Now to determine $\tilde{e}_{t}$ we use our now known functions, to calculate $\tilde{e}_{t}=y_{t}-\frac{B(z)z^{-d}}{A_{2}(z)}$, which we can then model as an ARMA model, which allows us to identify the model order of $A_{1}(z),C_{1}(z)$
			- We now have all the model orders, so we rerun the estimation of all the coefficients for all polynomials jointly
			- Lastly, see if the model has white residual as usual!
				- Also note that we can check that if we calculate the $\tilde{e}_{t}$ estimate according to above and look at the cross correlation between it and $x_{t}$, $\rho_{\tilde{e}_{t},x_{t}}$ it should be low as they are not supposed to be independent.
			- Example (in use):
				- We form $A_{3}(z)x_{t}=C_{3}(z)w_{t}$.
				- We look at ACF and PACF of $x_{t}$ to construct. PACF gives $A_{3}$, ACF gives $C_{3}$.
				- Look at residual, if it is white, continue, otherwise try different $A_{3},C_{3}$.
				- Compute $w_{t}=\frac{A_{3}(z)}{C_{3}(z)}x_{t},\epsilon_{t}=\frac{A_{3}(z)}{C_{3}(z)}y_{t}$
				- Estimate transfer function from $w_{t}$ to $\epsilon_{t}$ as $h_{k}=\frac{\sigma_{\epsilon}}{\sigma_{w}}\rho_{\epsilon,w}(k)$
					- As before delay = d, ring => r=2, 4 dominant components => s=3.
					- We never care about negative lags
				- We pretend the additive noise is white  and esimate the parameters for $y_{t}=\frac{B(z)z^{-d}}{A_{2}(z)}x_{t}+\tilde{e}_{t}$
					- Remember, B is order s and $A_{2}$ is order r
				- Calculate ACF and PACF of $\tilde{e}_{t}$, and use them to guess orders of $A_{1},C_{1}$
				- Estimate coefficients of just those two functions and see if that residual is white. Reiterate until white.
				- Now we estimate all coefficients jointly!

Mini Lecture 17 - Outliers
- Outliers corrupt the ACF severely.
- Outliers can be handled either by:
	- Detecting and removing outliers, possibly replacing with interpolated data.
	- Using Robust estimators that can handle the presence of outliers.
- Ways to remove outliers:
	- Trimmed ACF:
		- Simple, sort the data by size and remove the tail values on both sides, before resorting. Of course this will remove some true data.
		- The a-trimmed autocorrelation estimate removes the a largest and smallest values before recomputing the ACF, called TACF (tacf in MatLab).
			- We can use this to also see if we've been influenced by outliers simply by looking if ACF and TACF a very different.
	- Median filter. Simple, try it, might be enough.
- Outlier example: Not reporting death during christmas and then reporting it all the day after. Median filter is suitable for this.
- Example: Some arbitrary data with a PACF correlation at 52. However when we add a 52 lag for the AR we still see correlations at lag 52 (and around 52), in both ACF and PACF. However, when we add the first 1 lag for the MA part and reestimate both coefficients, all becomes white.
	- Remember! We need to reestimate all coefficients when we add stuff to the model as otherwise we will get corrupted results, because even if a 52 lag is correct, it might not be correctly estimated until we've added some other lag.

Mini Lecture 18 - Least squares
- Just chatting about $y=X\theta+e$
- Solution is $X^{\dagger}=(X^*X)^{-1}X^*$ (pseudoinverse)
- $\Pi_{X}=XX^{\dagger}=X(X^*X)^{-1}X^*$  projection matrix onto range space of X
- $e$ is orthogonal to $\mathcal{R}(X)$, i.e. $e=y-X\hat{\theta}=(I-\Pi_{X})y \implies \hat{\sigma}_{e}^{2}=\frac{1}{N-n_{\theta}}(y-X\hat{\theta})(y-X\hat{\theta})$.
	- If $e\in\mathcal{N}(0,\sigma_{e}^{2}I)$ then $\hat{\theta}$ is normal distributed with mean $E[\hat{\theta}]=\theta$, with variance $V[\hat{\theta}]=\sigma_{e}^{2}(X^*X)^{-1}$
		- $\hat{\theta}$ is the best linear unbiased estimate (BLUE) of $\theta$, i.e. the estimate with the lowest variance among all possible linear unbiased estimators
- Example: AR(p) process, $y_{t}+a_{1}y_{t-1}+\dots a_{p}y_{t-p}=e_{t}$. $e_{t}$ is zero-mean white process with variance $\sigma_{e}^{2}$.
	- We can express this as $e_{t}=y_{t}+[y_{t-1} \dots y_{t-p}][a_{1} \dots a_{p}]^T=y_{t}+x_{t}^T\theta$
	- Expand into $y=[y_{p+1}\dots y_{N}],X=[x_{p+1}\dots x_{N}],e=[e_{p+1}\dots e_{N}]$. Yielding, $e=y+X\theta$, and thus $\hat{\theta}=-(X^*X)^{-1}X^*y$
- However, what is the noise is colored? Weigthed Least Squares:
	-  $R_{e}=E[ee^{*}]$ is the covariance matrix of the additive noise, and let $W$ denote the matrix square root of $R_{e}^{-1}=W^*W$
	- We get the weighted least squares (WLS) estiamte, $\theta_{WLS}=\arg\min_{\theta}\lVert y-X\theta \rVert^{2}_{R_{e}}$
		- $\lVert a \rVert_{R_{e}}^{2}=a^*R^{-1}a$
	- Letting $\tilde{y}=Wy, \tilde{X}=WX,\tilde{e}=We$
	- Then $\hat{\theta}_{WLS}=\tilde{X}^{\dagger}\tilde{y}=(X^*R_{e}^{-1}X)^{-1}X^*R_{e}^{-1}y$
		- $V[\hat{\theta}_{WLS}]=(X^*R_{e}^{-1}X)^{-1}$

Mini Lecture 19 - Landmines
- ... Only some example

Mini Lecture 20 - Prediction Error Method (PEM)
- We assume we already have formed an estimate of the signal model. We may then form the prediction error from the one-step prediction, $\epsilon_{t+1|t}(\Theta)=y_{t+1}-\hat{y}_{t+1|t}(\Theta)$, given a collection of measurements up to time t.
- $\Theta=[\theta, Y_{t}]$ where $\theta$ is the parameter vector and $Y_{t}$ the collection of all available measurements up to time t.
- PEM:
	- We want to choose $\theta_{PEM}$ such that the variance of the prediction error is minimzed.
	- We estimate the variance of the prediction error as $\sum_{t}\lvert \epsilon_{t+1|t}(\Theta) \rvert^{2}$. Where we sum over available prediction errors.
		- We thus seek $\hat{\theta}_{PEM}=\arg\min_{\theta}\sum_{t}\lvert \epsilon_{t+1|t}(\Theta) \rvert^{2}$
	- Example: ARMA(p,q) process
		- $y_{t}=\sum_{l=0}^qc_{l}e_{t-l}-\sum_{l=1}^pa_{l}y_{t-l}=[-y_{t-l}\dots-y_{t-p}, e_{t-1}\dots e_{t-q}]\theta + e_{t}$,
		  with $c_{0}=1$, $\theta=[a_{1}\dots a_{p},c_{1}\dots c_{p}]^T$
			- Thus this is a p+q dimensional optimization problem
		- For the correct model our prediction error is simply our $e_i$ values which makes sense, but for an incorrect model it becomes something else, non convex problem.
		- However, we observe that our prediction error estimate is autoregressive as $E[y_{t+1}|\Theta]=\sum_{l=0}^qc_{l}\epsilon_{t+1-l|t-l}(\Theta)-\sum_{l=1}^qa_{l}y_{t+1-l}$
			- We need initial values for the prediction error, which we typically set to 0.
	- Initial values impact a lot so if you get bad values try different initial values.
		- It does not depend if it is an AR process (which doesn't depend on data) where PEM concides with LS, however when we add the MA part (which does depend on data).
- Maximum likelihood:
	- If we know the probability density function of our data.
	- Here we pick $\theta$ to maximize the probability density function, $\hat{\theta}_{ML}=\arg\max_{\theta}f(y;\theta)$, $f$ is the pdf of $y$.
	- We assume a multidimensional Gaussian distribution INPUT THE EXPRESSION
	- Taking the log we get $\hat{\theta}_{ML}=\arg\min_{\theta}(\log \det(R_{e})+(y-X\theta)^TR_{e}^{-1}(y-X\theta))$.
		- If we assume that $R_{e}$ which is not a realistic assumption this becomes $\hat{\theta}_{ML}=\arg\min_{\theta}((y-X\theta)^TR_{e}^{-1}(y-X\theta))$, which coincides with the WLS
			- $\hat{\theta}_{ML}=\hat{\theta}_{WLS}$ if we know $R_{e}$
		- For an ARMA model $R_{e}$ only depends on the noise power so we can rewrite the problem, yielding,
		  $\hat{\sigma}_{e}^{2}=\frac{1}{N-p}\sum_{t=p+1}^N\epsilon_{t}^{2}(\theta,\sigma_{e}^{2})$
		  $\hat{\theta}_{ML}=\arg\min_{\theta}=\sum_{t=p+1}^N\epsilon_{t}^{2}(\theta,\sigma_{e}^{2})$, which coincides with the PEM estimate
			- Simply. $\hat{\theta}_{ML}=\hat{\theta}_{PEM}$ if it is an ARMA process.
	- ML estimator generally gives the best performance, as it gives the lowest possible variance of any unbiased estimator. However, in many practical application it is not feasible to estimate. 