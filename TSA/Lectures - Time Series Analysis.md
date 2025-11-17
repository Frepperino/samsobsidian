

Lecture 3:
- If $z=e^{i\omega}$ then we have the Fourier transform. Z takes the whole imaginary plane into account, Fourier does the same on the unit circle.
- Even though the estimation of the covariance matrix using vector product form is not toeplitz, Levinson-Durbin can still be used to solve $\hat{\theta}=-\hat{R}^{-1}\hat{r}_{p}$ (regarding the AR processes and Yule-Walker equations)
- When observing ACF, ARs have more of a ringing (sinusoidal) form.
- Remember to always remove the first samples after filtering

Lecture 4:
- When comparing models, look at variance of residual. Less is better ofc
	- Make sure to check this regularly. Even if the model choice seems good from pacf and acf. But unless we see how much the variance of the residual reduces our model doesnt explain the data any better.
- be wary of doing transforms based on only a segment of the data were the trend looks simple
- When we do $\nabla_{365}$ we also lose all those data points in between
- we almost always use log to transform the data, try other stuff in the Box-Cox says clearly otherwise.
- even though tails are wrong in a gaussian plot, its still okay, cuz its the middle part thats important. even though it is more correct with a T dist. we like gaussian
	- If the middle part is bad, we may want to transform our data to look gaussian as our methods (dont know which exactly) depend on it.
- Right now our $a$ coefficients are constant, which means we must select a subset of our data, where the coefficient works well. Because well never be able to fit with the whole of it well. At the same time our estimates become worse the less samples we use
	- Later on in the course we will use temporally dependent $a$ to solve this.
- Do cool stuff and get extra points.
- Do something wise and explain why and youll get extra points
- Add some stuff on the AR part, then MA, then AR part, and so on
	- When iterating model selection/extension

Lecture 5:
- Previously we did the WGN input part, now we look at using
- Though basically all polynomials we use are monic $b_0$ in $B(z)$ is not 1 necessarily, as it scales the data, which is needed to have a matching order of magnitude with the WGN model input.
- $x$ and $w$ are only used to plot the correlation stuff to make a choice of smthn, then we throw em away
- Append a poem in the end that he likes and hell add a point.
	- You dont need to write one. He likes dylan thomas, do not go deep into the night. "bad poets mimic, good poets steal"
- If we have 2 inputs as we will in the project, we first use the strongest input and get or B and $A_{2}$ however, before we go to $C,A_{1}$ we'll subtract everything we have explained, and we see if the residual is still correlated with the second strongest input.
- If we apply our first part $y_{t}-\frac{B}{A_{2}}x_{t-d}=\tilde{\epsilon}_{t}$, then the way we model $\tilde{\epsilon}_{t}$ is simply what we do at $\frac{C(z)}{A_{1}(z)}e_{t}$.
- Intermediate variables like $w_{t}$ are only for deciding model order
- One of the most common mistakes is that you don't look at how much the models, e.g. $B,A_{2}$ explains the variance. If it doesn't then it doesn't mean they aren't correlated, we know they are, so change $B,A_{2}$.
- Remember That if roots of B and $A_{2}$ coincide then they cancel, and not necessarily cleanly, so you might get magic errors.
	- So remember to check if the roots are on top of eachother.
- looking at crosscorrelation between input and residual without XXX for several inputs we may already be done even though it isnt perfectly white. this is due to YYY. So it should only be an indicator that there MIGHT be stuff left to do
- There is no such a thing as a true model, does it work or not? Even when it truly is a simulated specific process we won't get the exact same coefficients.

Lecture 6:
- Absent

Lecture 7:
- Fisher information matrix:
	- $V[\hat{\theta}]\geq I_{\theta}^{-1}$, bounded by the Fisher information matrix
	- $[I_{\theta}]_{k,l}=-E\left[ \frac{ \partial^{2} \ln(f(y|\theta)) }{ \partial \theta_{k} \partial \theta_{l} } \right]$
		- We know this e.g. for Gaussian distributions.
	- If $V[\hat{\theta}]=I_{\theta}^{-1}$ => statistically efficient aka we've used all that we can from the data
		- The ML estimator is statistically efficient, $\hat{\theta}_{ML}\in \mathcal{N}(\theta,I_{\theta}^{-1})$
	- We can use this to design an experiment, as we can use the matrix to see how many N to theoretically get a certain variance. Or if a certain variance is possible for a given sample amount N.
- Model order estimation problem:
	- Which order, how many parameters?
	- $S_{\theta}=\sum_{t}\lvert \epsilon_{t+1|t}(\theta) \rvert^{2}$
	- Plotting $S_{\theta_{l}}$ against $l$, shows how the prediction error varies with a $\theta$ representing a further back $t-l$.
	- We can use this to select model order,
		- For the noiseless case we can see it become 0 and stay there for a certain $l$.
		- For the noise case we need to set a threshold to decide this.
			- Now we can add a penalty for having a lot of parameters, sum those values and find the minimum, that will be our $n_{\theta}$
			- Aka $\hat{l}=\arg\min_{l}(S_{\theta_{l}}+\text{penalty}(l))$
		- Some setups:
			- Bayesian, $BIC(l)=N\ln \hat{\sigma}_{k,l}^{2}+l \ln(N)$
				- Best because consistent
				- $S_{\theta}=\hat{\sigma}_{k,l}^{2}$
			- Akaike, $AIC(l)= -| |- +2l$
			- These only work with enough data! We do not trust these methods, we don't use them unless with copious amounts of data
- Residual analysis:
	- How do we know something is white?
	- So far we've done this by looking at the ACF and the PACF to see if all coefficients are below the significant level.
		- However, we may have some peaks that are sliiightly outside...
	- Statistical test
		- Ljung-Box_Pierce test:
			- $Q^*=N(N+2)\sum_{l=1}^K\frac{\hat{\rho}_{e}^{2}(l)}{N-l}$
			- $ACF \sim N\implies Q^* \sim \chi^{2}(K)$
			- $Q^*> \chi^{2}_{1-\alpha}(K)$ IF $\hat{\rho}$ is Normal
		- McLeod-Li test:
			- $Q^*=N(N+2)\sum_{l=1}^K\frac{\hat{\rho}_{e^{2}}^{2}(l)}{N-l} \sim \chi^{2}(K)$
				- Note the square of the residual e.
				- Almost always bad, never use it. Only works when the data is perfectly normal distributed, very sensitive to this assumption.
		- Monti test:
			- $Q_{M}=N(N+2)\sum_{l=1}^K \frac{\phi_{l,l}^{2}}{N-l} \sim \chi^{2}(K)$
				- He always uses this.
		- We only ever pick a test and then use that, otherwise we need to account for using several tests.
		- Kolmogorov Smirnov test:
			- Very forgiving. This may look good during development, but during prediction the model will not end up working very well.
		- Even if do not technically pass our Monti test, but almost then we say good enough and look at the validation set. Because overfitting is not necessarily a good course of action, especially as a good model also works further ahead from the validation set.
		- Sign changes test:
			- If it is white, it should change signs approx. for every sample, so we get $\#\text{sign changes} \in B\left( N-1, \frac{1}{2} \right)$
		- D'Agostino-Pearson's K$^{2}$ is good for when we have less data, comapred to ...
	- Be aware when running PEM that it doesn't exclude some coefficients, otherwise use PEB(?)
	- Look at Ex. 5.18, it is the entire story so far of modeling.
		- Also at 5.22
- Linear prediction:
	- $\hat{y}_{t+l|t}(\theta)$
	- For a normal process $\hat{y}_{t+l|t}(\theta)=\sum_{k=0}^nw_{k}y_{t-k}+c$, how do