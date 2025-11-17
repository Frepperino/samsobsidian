**Lecture 1 - Kriging 1**
- Expectation, Variance, Covariance definition
	- For vectors too
	- $V(Y)=V(AX+b)=AV(X)A^T=A\Sigma_{X}A^T$
	- Covariance matrices are:
		- Square
		- Symmetric
		- Positive definite
- Stochastic Processes:
	- Mean of the process is given by an expectation function $\mu_{Y}(t)=E(Y(t))$
	- Covariance function: $r(t,s)=C(Y(t),Y(s))=E[(Y(t)-\mu_{Y}(t))(Y(s)-\mu_{Y}(s))]$
	- For modelling a SP is often divided into $Y(t)=\mu(t)+\eta(t)+\epsilon(t)$
		- mean component: $\mu(t)$
		- zero mean stochastic process $\eta(t)$
		- uncorrelated eerrors, or nugget effects $\epsilon(t)$
		- $\eta(t)+\epsilon(t)=e(t)$
- Estimating the covariance function:
	- $\hat{r}(h)=\frac{1}{n-h}\sum_{t}e(t)e(t+h) \approx E[e(t)e(t+h)]$
- Example:
	- $y(t)=\mu(t)+\eta(t)$
	- $\eta(t)=\beta_{1}+\beta_{2}\sin(2\pi t)+\beta_{3}\cos(2\pi t)=X(t)\beta$
	- $\eta(t)=\alpha \eta(t-1)+\nu(t)$
		- $\nu(t) \in N(0, \sigma_{\nu}^{2})$, i.e. innovations are WGN
	- One-step-ahead mean prediction is now given by, $E[y(t+1)|Y_{1:t},\beta]=E[X(t+1)\beta+\eta(t+1)|Y_{1:t},\beta]=X(t+1)\beta+E[\alpha \eta(t)+\nu(t+1)|Y_{1:t,\beta}]=X(t+1)\beta+\alpha \eta(t)$
		- For further prediction ahead use the tower property, $E[y(t+2)|Y_{1:t}]=E[E[y(t+2)|y(t+1),Y_{1:t}]|Y_{1:t}]$
	- One-step-ahead variance predition is, $V[y(t+1)|Y_{1:t},\beta]=V[X(t+1)\beta+\eta(t+1)|Y_{1:t},\beta]=V[\alpha \eta(t)+\nu(t+1)|Y_{1:t},\beta]=\sigma_{\eta}^{2}$
		- For prediction further in time, try to write $y(t+n)$ as a linear combination of independent variables plus $Y_{1:t}$
			- Don't know exactly what this means

**Lecture 2 - Kriging 2**
- Stochastic fields:
	- Spatial interpolation:
		- Given observations at some locations (pixels), $y(s_{i}), i=1,\dots,n$ we want to make statements about the value at unobserved location(s) $y(s_{0})$
		- The typical model consists of a stochastic field.
	- Stochastic field: $Y(s)=\mu(s)+\eta(s)+\epsilon(s)$ observed at $s_{i}, i=1,\dots,n$
		- Coordinates are not restriced to time or space!
	- Stochastic field $Y(s), s \in D$ is a random function defined on some index set $D$.
		- In image analysis $D\subseteq \mathbb{R}^{2}$
	- Properties:
		- The expectation function $\mu_{Y}(s)=E[Y(s)]$ collects the point-wise expectation of the field.
		- The convariance is written as $r(s_{1},s_{2})=C(Y(s_{1}),Y(s_{2}))=E[(Y(s_{1})-\mu_{Y}(s_{1}))(Y(s_{2})-\mu_{Y}(s_{2}))]$, as usual
			- It acts the exact same as the usual covariance matrix, $\Sigma=\Sigma^T$ <=> $r(s,t)=r(t,s)$
			- $a^T\Sigma a>0$ <=> $\int _{\mathbb{R}^{2}}r(s,t)f(s)f(t) \, dsdt>0$
	- 2nd order (weak) stationarity:
		- A field is said to be 2nd order stationary if the expectation and covariance are unchanged under translation
		- $\mu_{Y}(s)=\mu_{Y}(s+h)=\text{const}$
		  $r(s_{1},s_{2}) \to r(h)$
		- A stationary field is sometimes said to be homogeneous
	- Isotropic and Anisotropic fields
		- Isotropic:
			- If a stationary covariance depends only on the distance between points $r(h)=r(\lVert h \rVert)$
		- Anisotropic:
			- Fields can be constructed from isotropic covariances by a linear transformation of the coordinates
			  $r(h)=r(d(h))$, $d(h)=\sqrt{ h^TAh }$
			- A is pos. def.
			- Note, $\lVert h \rVert=\sqrt{ h^TIh }$
		- Axis-anisotropy:
			- If A is diagonal the field is anistropic along the axis.
		- ![[Pasted image 20251110090001.png|400]]
- AR(1) process, $y(t)=\alpha y(t-1)+\nu(t)$
	- $E(y(t))=0$
	- $r(h)=C(y(t),y(t+h))=\frac{\sigma^{2}}{1-\alpha^{2}}\alpha^{\lvert h \rvert}$
	- $V[y(t)]=r(0)=\frac{\sigma^{2}}{1-\alpha^{2}}$
- Spectral Density:
	- For a stochastic process in time $x(t)$ with stationary covariance function $r(h)$, the spectral density and covariance function form a Fourier transform pair
		- $f(\omega)=\frac{1}{2\pi}\int _{-\infty}^\infty r(h)e^{-i\omega t} \, dh=\mathcal{F}r$, $r(h)=\int _{\infty}^\infty f(\omega)e^{i\omega h}\, d\omega=\mathcal{F}^{-1}f$
	- For a stochastic field $x(s)$ in $\mathbb{R}^d$ with stationary covariance function $r(h)$ the result is
		- $f(\omega)=\frac{1}{(2\pi)^d}\int _{\mathbb{R}^d}r(h)e^{-i\omega^Th} \, dh$
		  $r(h)=\int _{\mathbb{R}^d}f(\omega)e^{i\omega^Th} \, d\omega$
	- Bochner's Theorem:
		- A real valued continuous function is pos. def. iff it is the Fourier transformation of a symmetric, non-negative measure on $\mathbb{R}^d$
- Spectral representation:
	- In $\mathbb{R}^2$:
		- For a stationary isotropic covariance function we have, $r(h)=\int _{\mathbb{R}^2}f(\omega)e^{i\omega^Th} \, d\omega$.
		- Since an isotropic process $r(h)$ depends only on the distance $r(h)=r(\lvert h \rvert)$, a transformation to polar coordinates for $h$ and $\omega$ gives:
		  $\omega^Th=\omega_{1}h_{1}+\omega_{2}h_{2}=s_{\omega}s_{h}\cos(\theta)$
		  $d\omega=s_{\omega}d\theta ds_{\omega}$
		  $s_{h}=\lvert h \rvert$, $s_{\omega}=\lvert \omega \rvert$
		- Thus,
		- ![[Pasted image 20251110092108.png]]
	- Bessel functions:
		- ![[Pasted image 20251110092153.png|450]]
	- In $\mathbb{R}^d$:
		- Generalizing the results for $\mathbb{R}^2$, by using the same polar coordinate transformation and integrating over the angles, $r(h)=\int _{0}^\infty (2\pi)^{d/2}\omega^{d-1} \frac{J_{(d-2)/2}(\omega h)}{(\omega h)^{(d-2)/2}} \, d\omega$
		  $\omega=\lvert \omega \rvert$, $h=\lvert h \rvert$, $\sigma(\theta)$ is general angle Jacobian
- In summary, for a stochastic field $x(s)$ in $\mathbb{R}^d$ with isotropic stationary covariance function $r(h)$, the spectral density is,
	- $r(h)=(2\pi)^{d/2}\int _{0}^\infty f(\omega)\omega^{d-1} \frac{J_{(d-2)/2}(\omega h)}{(\omega h)^{(d-2)/2}} \, d\omega$
	  $f(\omega)=\frac{1}{(2\pi)^{d/2}} \int _{0}^\infty r(h)h^{d-1} \frac{J_{(d-2)/2}(\omega h)}{(\omega h)^{(d-2)/2}} \, dh$
	- $J_{\alpha}$ being a Bessel function of the first kind
- A model for Spatial Data:
	- From last lecture, we usually modela stochastic process by dividing it into, $y(s)=\mu(s)+\eta(s)+\epsilon(s)$
	- $\eta(s)$ is assumed to be stationary with some covariance function.
	- $\epsilon(s)$ is the nugger and represents small scale variability and measurement noise
	- The resulting covariance for Y is, $r_{y}(h)=r_{\eta}(h)+\mathbb{I}(\lVert h \rVert=0)\sigma_{\epsilon}^{2}$
		- $\mathbb{I}$ is basically delta function
		- This simplifies to $\sigma^{2}+\sigma_{\epsilon}^{2}$ if $\lVert h \rVert=0$ and $r_{\eta}(h)$ otherwise
	- Discrete representation
		- We need some discretization from $\mathbb{R}^2$ for practical computations.
		- For a given set of points $\{ s_{1},\dots,s_{n} \}$, we represent the full field by the random variables $Y(s_{i}), i=1,\dots,n$
	- Multivariate Normal distribution
		- We will use these extensively. Some recap:
		- $Y \in N(\mu, \Sigma)$
		- $E[Y]=\mu$, $\mu_{i}=E[Y(s_{i})]=E[Y_{i}]$
		- $\Sigma_{i,j}=C[Y_{i},Y_{j}]$, $\Sigma=C[Y,Y]=E[(Y-\mu)(Y-\mu)^T]$
		- The pdf is given by, $p(Y)=\frac{1}{(2\pi)^{N/2}\lvert \Sigma \rvert^{1/2}}\exp\left( -\frac{1}{2}(Y-\mu)^T\Sigma^{-1}(Y-\mu) \right)$
		- $Y$ and $\mu$ are column vectors of length $N$ and $\Sigma$ is NxN
- Covariance functions
	- We'll often need to estimate the NxN covariance matrix based on one sample (N observations) of the field.
	- This implies estimating N(N+1)/2 unknowns from N observations...
	- Further, the requirements of pos. def. on $\Sigma$ implies restrictions on the estimation
	- The covariance matrix is often assumed to come from a parametric family of covariance functions. This reduces the problem to estimation of covariance parameters
	- The resulting estimation problem does not have a closed form solution, leading to numerical optimisation
	- Thus, Kernel functions from Gaussian process literature $k(x_{1},x_{2})$
	- Some different forms:
		- ![[Pasted image 20251110100122.png|450]]
		- ![[Pasted image 20251110100606.png|400]]
		- The Gaussian can be simplified in the,
			- period case, period p: $r(h)=\sigma^{2}\exp\left( -\frac{2}{l^{2}}\sin ^{2}\left( \frac{\pi \lVert h \rVert}{p} \right) \right)$
			- linear case, non-stationary, often used to replace a mean function, $r(h_{1},h_{2})=\sigma_{b}^{2}+\sigma_{v}^{2}(h_{1}-c)^T(h_{2}-c)$
	- We can combine several covariance functions. If $r_{i}(h)$ are valid covariance functions, then so are:
		- Sums $r(h)=\sum r_{i}(h)$
		- Products $r(h)=\prod r_{i}(h)$
		- Sums across coordinates $r(h)=\sum r(h_{i})$
		- Products across coordinates (called separable covariances) $r(h)=\prod r(h_{i})$ 
	- The smoothness of the process is determined by our $r(t)$ as $t \to 0$
	  ![[Pasted image 20251110100750.png|400]]
	  ![[Pasted image 20251110100805.png|400]]
	- A last form is the Matern covariance, ![[Pasted image 20251110101710.png|350]]
		- Parameters are,
			- Variance $\sigma^{2}$
			- scale $x$
			- shape $\nu$
			- A measure of the range is given by $\rho=\frac{\sqrt{ 8\nu }}{x}$
			- Special cases if $\nu=k+\frac{1}{2}, k \in \mathbb{Z}$, then $r_{M}(h) \propto \text{poly}(\lVert h \rVert, k)\exp(-x\lVert h \rVert)$
			- It allows us to easily control both smoothness and range
	- Semi-variogram:
		- For a stationary, isotropic field the semi-variogram is defined as,
		  $\gamma(\lVert h \rVert)= \frac{1}{2}V[Y(s+h)-Y(s)]=r(0)-r(\lVert h \rVert)$
		- Measures how different two values at distance $\lVert h \rVert$ are.
		- Neat link between variogram and covariance function,
			- $\gamma(h)=\sigma^{2}+\sigma_{\epsilon^{2}}-r_{\eta}(\lVert h \rVert) \to \sigma^{2}+\sigma_{\epsilon}^{2}$, as $\lVert h \rVert \to \infty$
			- $r(h)=r_{\eta}(h)+\mathbb{I}(\lVert h \rVert=0)\sigma_{\epsilon}^{2} \to \sigma^{2}+\sigma_{\epsilon}^{2}$ as $\lVert h \rVert \to 0$
			- nugget $\sigma_{\epsilon}^{2}$, partial sill $\sigma^{2}$, sill $\sigma^{2} + \sigma_{\epsilon}^{2}$
			- ![[Pasted image 20251110102844.png|400]]
			  ![[Pasted image 20251110102904.png|350]]

**Lecture 3 - Kriging**
+ $\Sigma=\Sigma_{\eta}+I\sigma_{\epsilon}^{2}$
+ Gaussian Random Fields:
	+ $\mu_{i}=E[Y_{i}]$
	+ $\Sigma_{i,j}=r(s_{i},s_{j})$
	+ $Y \in N(\mu,\Sigma)$
	+ ![[Pasted image 20251113103352.png]]
	+ Since $Cov(A^Tx)=A^TCov(x)A$, we can simulate from the GRF using $x=\mu+R^T\epsilon, \epsilon \in N(0,I),R=\text{chol}(\Sigma)$
		+ As this gives $E[x]=\mu,Cov[x]=\Sigma$ 
	+ We have known, $Y_{k}$, and unknown, $Y_{u}$, data. $\mu_{k},\mu_{u}, \Sigma_{kk},\Sigma_{uk},\Sigma_{ku},\Sigma_{uu}$
+ Kriging:
	+ Given known (estimated) parameters we aim to reconstruct $y_{u}=y(s^{(u)})$
	+ It should be:
		+ Linear $\hat{y}_{u}=\sum_{i}\lambda_{i}y(s_{i})$
			+ It will be a linear sum of our observed $y$
		+ Unbiased $E[\hat{y}_{u}]=E[y_{u}]$
		+ Minimum prediction variance $\min V[\hat{y}_{u}-y_{u}]$
	+ Three types of Kriging:
		+ Simple kriging: $\mu$ known
		+ Ordinary Kriging: $\mu$ unknown, but constant
		+ Universal Kriging: $\mu=X\beta$, with $\beta$ unknown
			+ Here X is like a vandermonde matrix and $\beta$ are the coefficients.
	+ Proof for simple Kriging:
		+  using estimator $\lambda^TY$ gives that the optimal linear predictor is given by $E[Y_{u}|Y_{k}]$
	+ We start with simple kriging:
		+ The optimal prediction are thus, $E[Y_{u}|Y_{k}]=\mu_{u}+\Sigma_{uk}\Sigma_{kk}^{-1}(Y_{k}-\mu_{k})$
			+ But these are only optimal for known $\mu_{k},\mu_{u}$ (simple Kriging), in practice we need to estimate $\hat{\beta}$ to obtain $\mu_{k}=X_{k}\hat{\beta},\mu_{u}=X_{u}\hat{\beta}$
			+ So that is what we'll do now, for Universal Kriging
	+ Short sidenote:
		+ ![[Pasted image 20251113111702.png]]
		+ How sharp our covariance function is at $t\to 0$ decides how smoothly we feet to data.
	+ Sidenote on notation:
		+ In the GRF model we have $Y(s)=\mu(s)+\eta(s)+\epsilon(s)$, while in Kriging we approach it from an LS perspective where $\mu(s)$ becomes $X\beta$ and $\eta(s)+\epsilon(s)$ get pulled together into $\epsilon$. This makes total sense as $\text{C}[\eta] + \text{C}[\epsilon] = C[h]+\sigma_{\epsilon}^{2}I=\Sigma_{GLS}$.
	+ Starting with Ordinary Least Squares:
		+ To solve $\hat{\beta}$ we use LS. Now if we assume $\epsilon \in N(0,\sigma_{\epsilon}^{2}I)$, with $n$ observations and $p$ explanatory variables in $X$, then,
		  ![[Pasted image 20251113113109.png]]
		+ The prediction variances become
		  ![[Pasted image 20251113113210.png]]
		+ Matlab trick: Given multiple prediction locations with covariate matrix X0, then $V(\hat{\mu}_{0})$ is given by Vmu=sum((X0\*Vbeta).\*X0,2)
			+ Note that $\epsilon \in N(0,\sigma_{e}^{2}I)$ assumes that $\eta(s)+\epsilon(s)$ is independent, which is a very strong assumption. To address this we switch to generalized least squares
	+ Generalized Least Squares:
		+ Now we say $\epsilon \in N(0, \Sigma)$ allowing cross covariances. We assume we know $\Sigma$! (or have it estimated)
		+ We get, $\hat{\beta}=(X^T\Sigma^{-1}X)^{-1}X^T\Sigma^{-1}Y$, as the best estimate.
			+ We will later see this is the same as the ML estimate
		+ For our unknown, known system, the Gauss-Markow theorem gives us the best linear unbiased predictor,
		  $\hat{y}_{u}=X_{u}\beta \hat{h}+\Sigma_{uk}\Sigma_{kk}^{-1}(Y_{k}-X_{k}\hat{\beta})=E[y_{u}|Y_{k},\theta]$,
		  $\hat{\beta}=(X_{k}^T\Sigma_{kk}^{-1}X_{k})^{-1}X_{k}^T\Sigma_{kk}^{-1}Y_{k}$
			+ Sidenote on computation:
				+ To compute $\Sigma_{uk}\Sigma_{kk}^{-1}(Y_{k}-X_{k}\hat{\beta})$ we should use t he matlab blackslash operator or cholesky on $\Sigma_{kk}$, with the backslash. Never inv(...)
				+ Same for regression $\hat{\beta}=(X^TX)^{-1}X^TY$
		+ ![[Pasted image 20251113141215.png]]
		+ ![[Pasted image 20251113141239.png]]
		+ ![[Pasted image 20251113141853.png]]
			+ The red part contributes the best, and then the cyan, blue the least (USUALLY)
	+ Validating predictions:
		+ To asses quality of predictions we need to study expectation and variance
			+ 1.) Compute predictions for hold out data and check errors (RMSE, MAE, bias)
			+ 2.) Compute residuals and compare to covariates
			+ 3.) Compute standardised residuals $Z=\frac{Y_{v}-E[Y_{v}|Y_{k}]}{\sqrt{ V(Y_{v}|Y_{k}) }}$
				+ These should be roughly Gaussian
			+ 4.) Compute prediction intervals for the validation data at different $\alpha$-levels and chec that the corresponding number of validation points are inside the intervals.
				+ If the mean and variances are estimated accurately then the confidence interval of x% should contain x% of hold out samples. And so if you plot actual % contained vs theoretical % contained, it should be on a straight line (usually it isn't perfectly straight in a good situation though).



Assume zero mean field for the first lab



**Lecture 4** 
- We want to be able to do a non-parametric covariance estimation.
	- Estimation of the mean $\mu=X\beta$
	- Let $e=y-\mu$
	- Because $E[e_{i}e_{j}]=C[y_{i},y_{j}]$, since $e_{i}$ is zero-mean, we can make the following estimations
		- $\hat{\sigma^{2}+\sigma_{\epsilon}^{2}}=\frac{1}{n}\sum_{i}e_{i}^{2}$
		- $\hat{r}(kh)=\frac{1}{m_{k}}\sum_{H_{k}}e_{i}e_{j}$ 
			- $H_{k}=\{ (i,j): i\neq j,kh \leq \lVert s_{j}-s_{i} \rVert \}$
				- This just says we sum over all residuals of positions within a distance away where h is our step size. These are the bins I suppose
		- Both of these are those estimations we did in OASP
		- Assessing these estimations:
			- To do this we can either:
				- Permutation test essentially
					- 1.) Permute the observations among the locations
					- 2.) Compute the binned estimate for each permutation
					-  3.) Compute quantiles for each bin
				- Parametric boostrap essentially
				- 1.) Simulate data from the estimated model
				- 2.) Compute the binned estimate for each simulation.
				- 3.) Compute quantiles for each bin
			- Example algorithm (I assume this is alt. 1 above):
				- 1. Compute regression residuals $e=Y-X\hat{\beta}$
				- 2. Compute non-parametric estimate of variogram/covariance function
				- 3. Randomize residuals across locations, e.g. permute so that $e_{10}$ belongs to $s_{1}$, $e_{1}$ belongs to $s_{2}$
				- 4. Repeat and compute multiple variogram/covariance estimates under **$H_{0}$ of spatial independence.**
- Given some model $\pi(x;\theta)$ we want to estimate the parameter(s) $\theta$.
	- Common methods are LS and ML, however traditional ML assumes independent probabilities, which we obviously don't have.
	- Quick sidenote:
		- Remember we have essnentially rewritten our spatial model as $Y \in N(X\beta,\Sigma(\theta,\sigma_{\epsilon}^{2}))$, $\Sigma(\theta,\sigma_{\epsilon}^{2})=\Sigma_{m}(\theta)+I\sigma_{\epsilon}^{2}$
		- ![[Pasted image 20251113144838.png]]
	- Taking log-likelihood of Y:  ![[Pasted image 20251113144903.png]]
	- Parameter estimates are given by: ![[Pasted image 20251113144933.png]]
	- Note on computational details:
		- Fast and stabile computation tricks
		- Do cholesky of $\Sigma=R^TR$
			- Thus, $\log|\Sigma|=2\sum_{i=1}^n\log R_{ii}$
			- Regression becomes, $\beta=(\tilde{X}^T\tilde{X})^{-1}\tilde{X}^T\tilde{Y}$
				- $\tilde{X}=R^{-T}X$
				- $\tilde{Y}=R^{-T}Y$
			- Quadratic forms become $Y^T\Sigma^{-1}Y=\lVert \tilde{Y} \rVert^{2}_{2}$
	- To solve our log-likelihood we start with assuming $\Psi$ is known, which gives optimal $\beta(\Psi)$ as ![[Pasted image 20251113145633.png|400]]
	- Thus, replacing $\beta$ with $\beta(\Psi)$ we get the reduced problem of estimating $\Psi$. Profile likelihood:
		- ![[Pasted image 20251113145728.png|400]]
		- Replacing $\beta(\Psi)$ with its expression in this gives,
		- ![[Pasted image 20251113145821.png|250]]
			- where, ![[Pasted image 20251113145841.png|450]]
		- Note: in normal regression
			- ![[Pasted image 20251113145944.png|450]]
	- However $\Psi$ in profile-likelihood is biased, just as with estimates of $\sigma^{2}$ in normal Gaussian distributions. Thus we use,
	- Restricted maximum likelihood (REML) estimator:
		-  We want to remove the unknown mean by construction of "a contrast".
		- For our regression mean the siotable contrast is the orthogonal projection as inted at above. $(I-X(X^TX)^{-1}X^T)Y$, and from this we estimate $\Psi$ is based on $n-p$ (due to reduction of dimensionality) linearly independent elements in that projection.
		- We get, ![[Pasted image 20251113150457.png|450]]
			- P is the same as before
		- REML can be seen as the marginal likelihood when we integrate out $\beta$ from the likelihood $\int p(Y,\beta|\Psi) \, d\beta$. In comparison, in profile likelihood we substitute $\beta$ with it's ML estiamte $\beta(\Psi)$ instead.