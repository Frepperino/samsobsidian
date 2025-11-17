
Chapter 0:
- Wiener solution is the solution to a stationary problem for MSE
- Sampling theorem=Sampling rate needs to be twice of the greatest frequency component
- Filters with finite memory:
	- FIR filter
		- Inherently stable compared to IIR
	- Lattice predictor
		- $f_{m}$ is the mth forward prediction error based on the m past values
		- $b_{m}$ is the mth backward prediction error based on the m future values
		- $f_{0}(n)=b_{0}(n)=u(n)$
- IIR
	- has also feedback paths -> infinite memory
- Two families of linear adaptive filtering algorithms:
	- LMS-based. Model independent
	- RLS-based. Model dependent - assume multivariate Gaussian model.
- Classes of applications:
	- Identficiation
	- Inverse modeling (=equalization)
		- If XXX: filter is inverse of channel
	- Prediction
		- If y is our system output -> predictor
		- If e is our system output -> prediction error filter
	- Noise cancellation (this can be split or smthn, renamed)
		- Primary signal (d) -> signal + noise
		- Reference signal (u) -> noise
		- system output -> e

Chapter 1:
- Stochastic models:
	- AR: present u + sum past u = present v
		- <=>: u(n) = u(n-1) + ... + v(n)
		- predicts itself
		- $w*u=v$
		- $H_{A}(z)=Z[\{a_{n}\}]=\sum a_{n}z^{-n}$
		  $U(z)=Z[\{u(n)\}]=\sum u(n)z^{-n}$
		  $V(z)=Z[\{v(n)\}]=\sum v(n)z^{-n}$
		  $H(z)U(z)=V(z)$
		- AR analyzer = all-zero filter
		- AR Generator = all-pole filter
		  $H_{G}(z)=\frac{1}{H_{A}(z)}$
		  For all-pole to be stable, all the roots of the poles must be within the unit circle in the z-plane
	- MA: present u = present v = sum past v
	- ARMA: everything
- Yule-Walker
- PSD

Chapter 2:
- We minimize MSE of all things cuz parabola is nice.
- e = d + y. geometrically e is orthogonal to y.
- Wiener-Hopf equations: $Rw_{0}=p$
	- comes from: $E[u(n)e(n)]=0$. Expand e and you get $p-Rw=0$
-  Error surface:
	- We get it by expanding cost function $J=E[e(n)e(n)]$
	- The expression for J and Jmin.
	- canonical form (eigenvalues). vector v becomes principal axes 