Lecture 1:
TODO

Lecture 2:
- Pole model is one step prediction is Yule Walker
- This pole modeling stuff is when u = v(n)=WGN
- Prediction error filter:
- To do pole modeling we can start with one-step prediction. then we get the a coefficients which correspond to -w, and we get $\frac{1}{A(z)}$. Cuz the thing is that were w removes peaks we thus add peaks if we invert it.
- When talking prediction error filter $P_{M}=J_{min}$.
- Prediction $A(z)$ all-zero FIR removes spikes
  All-pole $\frac{1}{A(z)}$ IIr generates spikes, v WGN is input

Lecture 3:
- Steepest Descent leads to Wiener-Hopf. Purpsoe is to avoid inversion of R to save computation.
- For convergence analysis we do $\nu(n)=Q^T(w(n)-w_{0})$ on $J(n)=J_{min}+(w(n)-w_{0})^TR(w(n)-w_{0})=J_{min}+\sum_{k}\lambda_{k}|\nu_{k}(n)|^2$
  $-w_{0}$ centers it and $Q^T$ orients it.
- If we use the same substitution but instead with $w(n)=Q\nu(n)+w_{0}$ into the update equation we get,
  $\nu(n+1)=\nu(n)-\mu Q^TRQ\nu(n)=(I-\mu \Lambda)\nu(n)\to \nu_{k}(n+1)=(1-\mu \lambda_{k})^n\nu_{k}(0)$
  this gives us the stability criterion
- Time constant $\tau$ is how many iterations to decrease error by factor $e^{-1}$.
	- Time constant for eigenmode k is $(1-\mu \lambda_{k})^{\tau_{k}}=-1\to \tau_{k}=-\frac{1}{\ln(1-\mu \lambda_{k})}\approx \frac{1}{\mu \lambda_{k}}$.
	- The entire convergence is thus limited by $\lambda_{max}$ and $\lambda_{min}$, $\tau_{a}$