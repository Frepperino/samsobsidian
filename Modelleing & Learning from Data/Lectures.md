
**Lecture 4 - **
- **Support Vector Machines (SVM)**
  ![[Pasted image 20250930150032.png]]
	- Good when a lot of features
	- Versatile
		- Can be extended using kernels (linear, polynomial, RBF)
- **Bayesian Learning**
	- Idk about this bro...
- **Gaussian Mixture Models (GMM)**
	- A mix of several models where
	- $p(x|y) = N(x;\mu_{y},\Sigma_{y})$
	- See slides from singapore
	  ![[Pasted image 20250930150728.png]]
	- When predicting output for GMM:
		- Quadratic Discriminant Analysis (QDA)
			- $p(y=m|x_{*})=\frac{1}{c}\hat{\pi}_{m}N(x_{*}|\hat{\mu}_{m}, \hat{\Sigma}_{m})$
			- 1 gaussian distribution per class, individual convariances
			- $c$ is normalization constant so to sum probabilities to 1.
			- Quadratic decision bounday
		- Linear Discriminant Analysis (LDA)
			- $p(y=m|x_{*})=\frac{1}{c}\hat{\pi}N(x_{*}|\hat{\mu}, \hat{\Sigma})$
			- 1 gaussian distribution per class, same convariance
			- Linear decision boundary
	- Unsupervised GMM:
		* EM:
			* We want to find $\hat{\theta}=argmax_{\theta}p( \{x_{i}\}^n_{i=1} | \theta)$
		* K-means clustering
			- Assume uniform $\pi_{k}=\frac{1}{K}$, $\Sigma_{k}=\sigma^2I$
			- Algorithm:
				1. Set cluster centers $\mu_{1}, \mu_{2},\dots$ to some init. vals
				2. Determine which cluster $m$ each $x_{i}$ belongs to by closest distance.
				3. Update cluster centers $\mu_{m}$= average of all its $x_{i}$.
				4.  Repeat until convergence
- **SVD**
  ![[Pasted image 20250930153734.png|400]]
  ![[Pasted image 20250930153936.png|600]]
  Some math...
- **Principal Component Analysis (PCA)**
  ![[Pasted image 20250930154351.png|500]]
	- Calculating PCA from SVD $X=U\Sigma V^T$
		- Principal component variances $\lambda_{i}=\Sigma_{ii}^2$
		- PCA vectors are col $V_{i}$ in $V$.
		- The first $k$ PCA coordinates are obtained by multiplying the first $k$ columns of matrix V $PCA = \tilde{X}V_{:,1:k}$
	- When projecting images on p largest PCA components:
		- Faster training
		- Potentially improved accuracy

**Lecture 7 - Physical Modeling**
- Principles of Physical Modeling
	- Idea: Energy is conserved but can be transformed, e.g. kinetic energy and momentum
	- Many physical laws for dynamical systems stem from conserved quantities
	- Dimensional analysis:
		- e.g. mass $M$, density $ML^{-3}$, force $MLT^{-2}$
	- Buckingham's $\Pi$ theorem: Laws should not depend on the choice of units
		- If a physical equation involves n physical variables, then it can be rwritten in $m=n-r$ dimensionless parameters $\Pi_{1},\dots,\Pi_{m}$ ............................................
- Some Basic Relationships in Physics
- Simplifying models


**Lecture 8 - Object-oriented Modeling**
- Modeling paradigms
	- Block diagram modeling (causal modeling) vs. Equation based modeling (acausal modeling)
	- Block diagram modeling:
		- ![[Pasted image 20251111195110.png]]
		- You know the classic information hiding, abstraction, control theory, input-output models with blocks of state equations
		- NOT for serious large-scale physical modeling
			- Becomes problematic when deducing how sub-components influence other components, like complex physical systems (water tanks n stuff)
			- Equation-based paradigm scales better
	- Equation-based modeling:
		- Can in an easier way change an individual part, like a resistor or conductor, without causing propagating effects in the same way.
		- E.g. industrial robot has 1000 non-trivial algebraic equations, 80 states. Tough to do in block diagram modeling
		- Components
			- Contains component classes which are defined independently of the enironment, making it reusable
			- Component may internally consist of other components, i.e. hierarchical modeling
			- A complex system usually consists of a large number of connected components
			- We want this all to work nicely, thus came Modelica
- Modelica Language:
	- It is a language that many tools use.
	- Declarative: equations and math functions allow acausal modeling, high-level specification
	- Multi-domain modeling: combines electrical, mechanical, biological, control, etc.
	- Everything is a class: Strongly types object-oriented with a general class concept
	- Visual component programming
	- Efficient, non-proprietary
	- The big part is that we skip the need to derive causality which we must do in C, Fortran, etc., code.
	- Connectors:
		- instances of connector class
		- Two kinds of variables in connectors
			- Non-flow: potentrial or energy levels
				- Equality coupling
			- Flow: represent flow
				- Sum-to-zero coupling
				- Positive when the current flows into the component
		- Connections between connectors are realized as equations
- Differential Algebraic Equations (DAEs)
- Modelon Impact