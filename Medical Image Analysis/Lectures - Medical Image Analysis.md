
**Lecture 1 - Landmark-Based Registration**
- Image registration = determining a geomtrical transformation that aligns corresponding points in a sequence of images
- Spatial mappings (linear)
	- Translation
	  ![[Pasted image 20251107143835.png]]
		- $y(x;t)=x+t$
	- Rigid (translation + rotation)
	  ![[Pasted image 20251107143931.png]]
		- Definition: $\lVert \phi(x)-\phi(y) \rVert=\lVert x-y \rVert$
		- $y(x;R,t)=Rx+t$
		- $R^TR=RR^T=I$
			- $R$ is just the classical rotation matrix
			- $\det(R)=1$. Could be -1 but we set it as 1.
		- Par. in 2d = 1+2 = ($\theta$ + $t_{x} + t_{y}$)
	- Similarity transformation
	  ![[Pasted image 20251107144215.png]]
		- $y(x;s,R,t)=sRx+t$
			- $s\in\mathbb{R}^+$ i scale 
			- $sR$ = [[a, -b][b,a]]
		- Par in 2d = 2 + 2 = ($t_{x}+t_{y}+a+b$)
			- In 3d: 7
	- Affine Transformation
	  ![[Pasted image 20251107144513.png]]
		- $y(x;A,t)=Ax+t$
			- We can scale x and y differently
		- A is any 2x2 matrix
		- Par in 2d = $2+4=(t_{x}+t_{y}+4\text{ elements in matrix})$.
			- In 3d: 12
	- When to use which?
		- Rigid transform:
			- global patient repositioning (intra-subject)
		- Similarity transform:
			- shapy analysis
		- Affine transform
			- first step in non-linear registration
- Spatial mappings (non-linear)
  ![[Pasted image 20251107144817.png]]
	- Models:
		- Control points (e.g. interpolating thin plate spline)
		- Basis functions (e.g. sines/cosines, B-spline basis functions)
	- When to use non-linear:
		- Tissue motion (cardiac cycle/pulmonary cycle)
		- Deformation compensation (intra-operative, soft tissue)
		- Longitudinal tissue changes (e.g tumor growth)
		- Inter-subject registration
	- Parameters = control point coordinates or basis function coefficients etc. => 20-1,000,000 dof
- Landmark based registration
	- We use some geometrical transformation (above) $y(x;w)$
	- Then as similarity measure $D(w)=\sum_{i=1}^N \lVert y(x_{i};w)-y_{i} \rVert^{2}$, how well the transformed image location matches the target location
	- Regularization Term S(w) enforces smoothness of the transformation by penalizing extreme deformations, non-smooth warps or unrealistic motion.
	- Optimization objective $J(w)=D(w)+\alpha S(w)$, cost function we want to minimize.
	- Types of landmarks
		- Anatomical landmark = assigned by an expert; anatomically meaningful
		- Mathematical landmark = computed based on mathematical/geometrical principles (e.g. max curvature)
		- Pseudo landmark = computed based on anatomical or mathematical landmarks (e.g. curve length)
	- Affine landmark based registration
		- We use affine transformation
		- No regularization
		- This leads to:
			- $\min\sum^N_{i=1}\lVert y(x_{i};A,t)-y_{i} \rVert^{2}=\min \sum^N \lVert Ax_{i}+t-y_{i} \rVert^{2}=\min \sum^N_{i=1}\sum^P_{j=1}\left( y_{i}^j-t_{j}-\sum^P_{k=1}a_{jk}x_{i}^k \right)^{2}$
			- Which is standard linear regression with :
			  ![[Pasted image 20251107151704.png|600]]
	- Rigid landmark based registration
		- We use rigid transformation
		- Rotation constraints $R^TR=I$ and $\det(R)=1$ makes life much more difficult as it introduces constraints on our selection of R during optimization.
- Image registration (the four basic steps):
	- A geometrical transformation $y(x;w)$
	- A similarity measure $D(w)$ and a regularization term $S(w)$
	- Define "energy": $E(w) :=\lambda S(w)+D(w)$, where $\lambda$ is a nonnegative weight
	- Solve the minimzation problem $w_{*}=\arg_{w}\min E(w)$
	- Profit: The registration map is thus $y=y(x;w_{*})$
- For rigid registration (Euclidean transformation)
	- Given corresponding landmarks $x_{i},y_{i}$, we seek rotation $R_{*}$ and translation $t_{*}$ from $\min \sum_{i=1}^N \lVert y_{i}-t-Rx_{i} \rVert^{2}$
		- Same as we did with Affine! Just insert the geometrical transformation in the LS problem
	- The algorithm:
		- Set $\bar{x}=\frac{1}{N} \sum x_{i}$ and $\bar{y}=\frac{1}{N} \sum y_{i}$ we call these averages centroids.
		- Define the displacement as $\tilde{x}_{i}=x_{i}-\bar{x}$ and $\tilde{y}_{i}=y_{i}-\bar{y}$
		- Define outer product matrix $H=\sum^N_{i=1}\tilde{y}_{i}\tilde{x_{i}}^T$ and take SVD, $H=UDV^T$. 
		- Then, $R_{*}=Udiag(1,1,\det(UV^T))V^T$; $t_{*}=\bar{y}-R_{*}\bar{x}$
			- In 2D use $diag(1,\det(UV^T))$
	- In greater detail (this tackles some of the reasoning but not explicitly why it works):
		- Step 0: Centroids as solution of a quadratic minimzation
			- In a generic problem where we seek $\arg_{t}\min \frac{1}{N}\sum_{i=1}^N \lVert t-z_{i} \rVert^{2}$, the solution is simply the centroid of $z_{i}$, $t_{*}=\bar{z}=\frac{1}{N}\sum_{i=1}^N z_{i}$
			- Proof:
				- See slide 8 lecture 1
		- Step 1: Elimination of the translation
			- I assume this simply implies that we use step 0 to remove t from the minimization problem by setting $t_{*}=\bar{y}-R_{*}\bar{x}$ as that is simply the distance. And thus, we treat the optimization problem of $t$ and $R$ as independent. 
		- Step 2: Some properties of the trace of a matrix
			- $tr(yx^T)=x^Ty$
			- $tr(A+B)=tr(A)+tr(B)$
			- $tr(A^TB)=tr(BA^T)$
			- $tr(ABCD)=tr(BCDA)$
		- Step 3: Reformulation of the problem
			- We assume that we've already solved for $t$, thus we only need to solve the remainder $\min_{R}D(R)=\sum_{i=1}^N \lVert y_{i}-Rx_{i} \rVert^{2}$, where $R$ must be a rotation matrix.
			- Using Step 2 we can rewrite $\lVert y_{i}-Rx_{i} \rVert^{2}=\lVert y_{i} \rVert^{2}-2tr((R^Ty_{i})x_{i}^T)+\lVert x_{i}^{2} \rVert$,
			- From here we define $H:=\sum y_{i}x_{i}^T$
			- This leaves the maximization problem, $max_{R}tr(R^TH)$
			- We slve this using SVD of $H$.
- For Similarity Transforms (Procrustes):
	- $\min\sum_{i=1}^N \lVert y_{i}-t-sRx_{i} \rVert^{2}$
	- Algorithm:
		- Set $\bar{x}=\frac{1}{N} \sum x_{i}$ and $\bar{y}=\frac{1}{N} \sum y_{i}$ we call these averages centroids.
		- Define the displacement as $\tilde{x}_{i}=x_{i}-\bar{x}$ and $\tilde{y}_{i}=y_{i}-\bar{y}$
		- Define outer product matrix $H=\sum^N_{i=1}\tilde{y}_{i}\tilde{x_{i}}^T$ and take SVD, $H=UDV^T$. 
		- Then, $R_{*}=Udiag(1,1,\det(UV^T))V^T$; $t_{*}=\bar{y}-R_{*}\bar{x}$
		- This is where we at first differ from rigid transformation:
			- $s_{*}=\frac{\sum_{i=1}^N\tilde{y}_{i}^TR_{*}\tilde{x}_{i}}{\sum_{i=1}^N \lVert \tilde{x}_{i} \rVert^{2}}$
			- $t_{*}=\bar{y}-s_{*}R_{*}\bar{x}$
- Image transformation by pullback:
	- I dont understand

**Lecture 2 - Intensity-Based Registration**
- Three different registration problems
	- Intra-modality (same subject, different modalities)
	- Intra-subject (same modality, different subjects)
	- Intra-times??? (same subject, different times)
- RANSAC = RANdom Sampling Consensus
	- Input:
		- S = data points
		- n = sample size (model complexity or dof)
		- k = number of iterations
		- t = theshold for goodness of fit
	- Loop:
		- Pick sample of size n at random from S
		- Fit model to chosen sample
		- Count number of inliers (Elements in S fitting the estimated within the threshold t)
		- Store chosen sample and inliers if better than previous one
	- Finalization
		- Fit model to the inliers of the best sample
	- I.e., for k iterations we fit our model to n samples from S. How good this fit is is determined by how many data points fit this model within threshold t. In the end our we fit all model to ALL the inliers of the best sample.
- Intra-modality registration:
	- ![[Pasted image 20251109143311.png|500]]
	- To measure the difference we use sum of squared differences (SSD), $D_{SSD}(w)=\frac{1}{2}\sum_{i \in \Omega}(T(y(x_{i};w))-R(x_{i}))^{2}$
		- ![[Pasted image 20251109143502.png|400]]
		- ![[Pasted image 20251109143538.png|400]]
		- The problem with this is if we have miscalibration of intensities, resulting in different brightnesses, which means minimization will be influenced just by the absolute brightness at different spots. To combat this we use correlation coefficient which is invariant to the global gain/offset
	- Correlation coefficient (CC) $D_{CC}(w)=\frac{\sum_{i \in \Omega}(T(y(x_{i};w))-\bar{T})(R(x_{i})-\bar{R})}{\sqrt{ \sum_{i \in \Omega}(T(y(x_{i};w))-\bar{T})^{2}\sum_{i\in\Omega}(R(x_{i})-\bar{R})^{2} }}$
		- $\bar{T}=\frac{1}{\lvert \Omega \rvert}\sum_{i\in\Omega}T(y(x_{i};w))$
		- $\bar{R}=\frac{1}{\lvert \Omega \rvert}\sum_{i \in \Omega}R(x_{i})$
	- We can model the contrast resp. brightness difference as, $y \approx ax+be$
		- Where $x$ is the original image value with some contrast difference $a$, and $e=[1,1,1,1,\dots]^T$ gives overall added brightness $b$.
		- Solving for $a$ and $b$ to minimize, $\lVert y-(ax+be) \rVert^{2}$ gives:
			- $b^*=\frac{(y-ax)^Te}{\lVert e \rVert^{2}}=\bar{y}-a\bar{x}$
			- $a^*=\frac{\hat{y}^T\hat{x}}{\lVert \hat{x} \rVert^{2}}$; $\hat{x}=x-\bar{x}e;\hat{y}=y-\bar{y}e$
			- Minimum of residual $\lVert \hat{y} \rVert^{2}\left( 1-\frac{(\hat{y}^T\hat{x})^{2}}{\lVert \hat{x} \rVert^{2}\lVert \hat{y} \rVert^{2}} \right)$
			- We can see the minimal residual is achieved when the CC is maximized
	- A similar problem to give the same result of using CC is the application: matching using cross-corelation.
		- Which of image $x_{i}$ looks most like $y$? $y \approx a_{i}x_{i}+b_{i}e$ 
		- Same minimization problem as before however, we minimize over which $i$.
		- Using the same minization as above we get $\min_{i=1,\dots n}\lVert \hat{y} \rVert^{2}\left( 1-\frac{(\hat{y}^T\hat{x}_{i})^{2}}{\lVert \hat{x}_{i} \rVert^{2}\lVert \hat{y} \rVert^{2}} \right)$
		- Which again reduces to maximization of cross-correlation.
- Inter-modality registration:
	- Joint entropy $D_{JE}(w)=H(T(y(x_{i};w)),R(x_{i}))$
	- $H(T(y(x_{i};w)),R(x_{i}))=-\sum_{j,k}PDF(j,k)\log(PDF(j,k))$
	- $PDF(j,k)=\frac{HIST(j,k)}{\sum_{j,k}HIST(j,k)}$
		- This simply uses the standard entropy definition but our probability density function is just histogram based.
		- Some entropy properties:
			- $H(p)$ assumes $p$ is a probability distribution $(p_{1},p_{2},\dots,p_{n})$ on $\{1,2,\dots n\}$. Where of course $0\leq p_{i}\leq 1$, $\sum p_{i}=1$
				- This is why use the historgram PDF as input for our images 
			- $H(x)\geq 0$ for all $x$
			- $H(p)=0$ iff $x_{i}=1$ for some $i$ (and thus $x_{j}=0$ for all other)
			- $H(p)$ is maximal if $p=\frac{(1,1,\dots,1)}{n}$, with maximal value $\log(n)$
	- The problem is that we have parts outside our subject that may be completely black in an MRI e.g. To account for this we create a new metric that accounts for this, Mutual Information
	- Mutual information, $D_{MI}=H(T(y_{i}(x_{i};w)),R(x_{i}))-H(T(y(x_{i};w)))-H(R(x_{i}))$
		- Entropy of joint and marginal probability distributions:
			- We now look at the two-dimensional discrete probability distribution for the image $0\leq p_{ij}\leq 1$, $i=1,\dots,n$; $j=1,\dots,m$. $\sum_{i,j}p_{ij}=1$
			- The two-dimensional entropy definition is, $H(P)=-\sum_{i=1}^N\sum_{j=1}^Mp_{ij}\log p_{ij}$
			- We define the marginal probablity distributions $q$ and $r$ as vectors with the elements $q_{i}=\sum_{j=1}^mp_{ij}$, $r_{j}=\sum_{i=1}^n p_{ij}$
			- We also define $\tilde{P}=q\otimes r$ by $\tilde{p}_{ij}=q_{i}r_{j}$
				- Lemma: $H(q \otimes r)=H(q)+H(r)$
			- Problem: Find $P^*$ that maximizes the entropy $H(P)$ among all probability distributions $P$, with prescribed (given) marginal distributions $q$ and $r$.
				- Theorem: The solutions is $P^*=q \otimes r$
				- Corollary: $H(P)\leq H(q\otimes r)$ for all $P$ with marginal distributions $q$ and $r$
					- It follows that the mutual information $MI(P):=H(P)-H(q\otimes r)=H(P)-H(q)-H(r)$, is non-positive.
						- Moreover if $H(P)=0$, then $P=q\otimes r$ 
- A bit of summary from above:
	- We learn which Similarity Measurement to use
	- Intra-modality:
		- Same calibration? => SSD is okay
		- Differen calibration? => Use CC
	- Inter-modality:
		- Use MI
- Initial transformation:
	- We use the principal axes to align.
	- Start with setup:
	- ![[Pasted image 20251109161226.png|500]]
	- Computing principale axes:
		- $I(X)$ is the grey scale value of the image at position $X$ ($[0,255]$ or $[0, 1]$)
		- $X=(x,y) \in D\subset \mathbb{R}^2$ is a pixel in the image domain $D$.  
		- We consider the image as a mass-density.
			- There is (in principle) no mass in the background
		- Center of mass $\bar{X}=\frac{1}{m}\int _{D}I(X)X \, dX$; $m=\int _{D}I(X) \, dX$
			- Equally: $\bar{x}=\frac{1}{m}\int \int _{D}xI(x,y) \, dx \, dy$;  $\frac{1}{m}\int \int _{D} yI(x,y) \, dx \, dy$
		- We normalize the coordinates: $\hat{X}=(\hat{x},\hat{y})^T:=X-\hat{X}$
		- Compute the tensor of inertia, $M=\frac{1}{m}\int _{D}\hat{X}\hat{X}^TI(X) \, dX=\frac{1}{m}\int \int _{D} \begin{bmatrix} \hat{x}^{2}&\hat{x}\hat{y} \\ \hat{y}\hat{x} & \hat{y}^{2} \\ \end{bmatrix} \, dx \, dy$
		- By spectral theorem we get the decomposition, $Q\Sigma Q^T=M$
			- $Q=[q_{1},q_{2}]$ is an orthogonal matrix and $\Sigma=diag(\sigma_{1}^{2},\sigma_{2}^{2})$ is diagonal.
			- We assume $\sigma_{1}^{2}\geq \sigma_{2}^{2}$ and $\det Q=1$ (no mirroring)
		- Now aligning the two images $I$ and $\tilde{I}$
			- $\bar{X}$, $M=Q\Sigma Q^T$, and $\bar{Y},\tilde{M}=\tilde{Q}\tilde{\Sigma}\tilde{Q}^T$, respectively.
			- The aligning transformation $Y=T(X)$ is given by $Y=\bar{Y}+\tilde{Q}Q^T(X-\bar{X})$ 


**Lecture 3 - Clustering & Segmentation**
- Non-rigid registration
	- We use thin-plate splines for this,
	- The thin-plate spline $u=u(x,y)$ is the minimizer of the functional, $E[f]=\int \int _{\mathbb{R}^{2}}\left\{ \left( (\frac{ \partial^{2} f }{ \partial x^{2} })^{2}+2(\frac{ \partial^{2} f }{ \partial x \partial y })^{2}+\left( \frac{ \partial^{2} f }{ \partial y^{2} } \right)^{2} \right) \right\} \, dx \, dy$
		- among all functions satisfying $f(x_{i},y_{i})=\alpha_{i}$ at nodes $(x_{i},y_{i})$, $i=1,\dots,N$ (i.e. we consider interpolation)
		- The solution can be written as a linear (affine) term plus a linear combination of translates of the "basis function"
			- $U(x,y):=-r^{2}\log (r^{2})$, $r=\sqrt{ r^{2}+y^{2} }$
			- The basis function satisfies $-\Delta^{2}U=\text{const} \delta_{0,0}$ (Dirac's delta)
				- I.e. U is a Green's function of the operator $-\Delta^{2}$ (the bi-Laplacian)
		- Be careful with large deformations as they might end up not being bijective,
	  ![[Pasted image 20251109164437.png]]
- Segmentation:
	- Clustering methods:
		- Using K-means:
			- We find K clusters of N d-dimensional data points
			- Lloyd's algorithm:
				- Initialization: Choose cluster centers $\mu_{1},\mu_{2},\dots ,\mu_{K}$ in some way, e.g. as a subset of the data points
				- Class assignment (E): The classes are defined by $S_{k}=\{x_{i}|x_{i} \text{ has } \mu_{K} \text{ as closest cluster center}\}$
				- Class updates (M): $\mu_{K}=\frac{1}{\lvert S_{k} \rvert}\sum_{x \in S_{k}}x$
				- Repeat
			- Gray scale images using clustering,
			  ![[Pasted image 20251109164958.png|400]]
			- Color images using clustering,
			  ![[Pasted image 20251109165019.png|400]]
		- Using Gaussian Mixture Models:
			- Goal is to achieve better clustering by modelling the data statistically
				- We do this by using cluster covariances in addition to cluster means
			- We have $N$ voxels
			- $d=(d_{1},d_{2},\dots,d_{N})^T$ are the intensities of voxels $d_{i}$
			- We want to get K classes, $l=(l_{1},l_{2},\dots,l_{N})^T$, $l_{n} \in \{1,\dots,K\}$
			- ![[Pasted image 20251109165507.png|150]]
			- Thus we use a statistical model, to find the most likely label $\hat{l}=\arg\max_{l}p(l|d,\hat{\theta})$
			- We assume that each pixel is the realization of one of the K Gaussian distributions, thus a GMM!
			- $p(l|d,\hat{\theta})=\frac{p(d|l,\hat{\theta}_{d})p(l|\hat{\theta}_{l})}{p(d|\hat{\theta})}$
				- ![[Pasted image 20251109170704.png|450]]
				- The denominator is not needed as we only need to maximize, and otherwise $p(d|\hat{\theta})=\sum_{l}p(d|l,\hat{\theta}_{d})p(l|\hat{\theta}_{l})$
				- The model depends on some parameters $\theta=(\theta_{l}^T,\theta_{d}^T)^T$
					- $\theta_{l}$ is for labeling model
					- $\theta_{d}$ is for image model
					- The exact values are assumed to be known for now...
				- $p(l|\theta_{l})$ is our "labeling model"
					- We model each label probability categorically, $p(l, \theta_{l})=\prod_{n}\pi_{l_{n}}$, where $\theta_{l}=(\pi_{1},\dots,\pi_{K})^T$
					- So our  $\theta_{l}$ parameter is our categorical probability distribution.
				- $p(d|l,\theta_{d})$ is our "imaging model"
					- Here we use our GMM part. The intensity is assumed to be Gaussian distributed, $p(d|l,\theta_{d})=\prod_{n}N(d_{n}|\mu_{l_{n}}, \sigma_{l_{n}}^{2})$
					- $\theta_{d}=(\mu_{1},\dots,\mu_{K},\sigma_{1}^{2},\dots,\sigma_{K}^{2})^T$
					- Remember, $N(d|\mu,\sigma^{2})=\frac{1}{\sqrt{ 2\pi \sigma^{2} }}\exp\left( -\frac{(d-\mu)^{2}}{2\sigma^{2}} \right)$
				- I don't understand where they get this from the earlier expression for the same probability but, $p(d|\theta)=\prod_{n}\left( \sum_{k}N(d_{n}|\mu_{k},\sigma_{k}^{2}) \pi_{k} \right)$
					- $\theta=(\mu_{1},\dots,\mu_{K},\sigma_{1}^{2},\dots,\sigma_{K}^{2},\pi_{1},\dots,\pi_{K})^T$
				- All together we get, $p(l|d,\hat{\theta})=\frac{\prod_{n} N(d_{n}|\mu_{k},\sigma_{k}^{2}) \prod_{n} \pi_{k})}{\prod_{n} \sum_{k}N(d_{n}|\mu_{k},\sigma_{k}^{2}) \pi_{k}}$
					- Note, we can also thus rewrite it as $p(l|d,\hat{\theta})=\prod_{n}p(l_{n}|d_{n},\hat{\theta})$
					- And further, $p(l_{n}|d_{n},\hat{\theta})=\frac{N(d_{n}|\mu_{l_{n}},\hat{\sigma}_{l_{n}}^{2})\hat{\pi}_{l_{n}}}{\sum_{k} N(d_{n}|\mu_{k},\hat{\sigma}_{k}^{2})\hat{\pi}_{k}}$
				- And thus, $\hat{l}=\arg\max_{l}p(l|d,\hat{\theta})=\arg\max_{l_{1},\dots,l_{K}}p(l_{n}|d_{n},\hat{\theta})$.
				- GMM seems better given than K-means given the right params,
				  ![[Pasted image 20251109211643.png|350]]
	- Graph Cuts segmentation:
		- On the blackboard apparently.

**Lecture 4 - Segmentation I (Traditional segmentation models)*
- Segmentation:
	- Divide image into e.g. different organs or anatomical features
	- Can either be represented as contours that encloses different parts, or masks.
	- The first step before classification
	- Vital to segment organs in different image modalities, or cells in different smears and sections
	- 3 methods:
		- Contour-based:
			- Find perimeter of the object
			- Watershed:
				- Mathematical morphology:
					- translation, reflection, complement, difference
					- dilation: $A\oplus B$ extendend A with B
					  ![[Pasted image 20251112173648.png|150]]
					- erosion: $A\ominus B$ eroding A with B
					  ![[Pasted image 20251112173740.png|150]]
					- opening: $A\circ B=(A\ominus B)\oplus B$ first erosion then dilation
						- gives smoother contours, removes narrow structures (splits up objects), eliminates thin parts
						  ![[Pasted image 20251112173919.png|150]]
					- closing: $A\cdot B=(A\oplus B)\ominus B$
						- gives smoother contours, fills up small parts, fills up holes
						  ![[Pasted image 20251112174041.png|150]]
				- We can combine thresholding with mathematical morphology => watershed segmentation
					- morphology helps fix the small holes, irregular contours, over-segmentation and spurious objects
				- Efficient and exact
				- Analogy to where water flows in a landscape
					- See gradient as 3D-landscape
					- Each object starts from a local minimum in the gradient
					- It starts to rain, each minimum builds up 
				- Walls are built when two catchment bases connect, by identifying pixels on the boundary between different objects, which is efficiently computed using morphological operators
				- Practical aspects:
					- Low-pass-filter the image
					- Find "significant" local minima
					- Compute gradient image
					- Apply Watershed
					- Improve the results (e.g. by morphology)
				- ![[Pasted image 20251112174518.png]]
				- If over-segmenting, we can use several internal markers to collect seveal local minima to a bigger collection, and/or(?) use external markers to define the background
		- Voxel/pixel-based:
			- Classify pixels as inside or outside
				- Thresholding:
					- Given a grayscale input image, construct a binary image according to grayscale being over or under some threshold.
					- Advantages:
						- Simple to use and implement
					- Problems:
						- Threshold T has to be chosen
						- The resulting segmentation might not be connected
						- Classification of one pixel independent of neighbors
						- Can produce irregular boundaries
						- Acceptable results only when object has a significantly different gray-level than the background.
					- How to select the threshold:
						- Look at the histogram of the image
						- Assume that the intensities in the background and object are Gaussian distributed.
						- Estimate the two means and variances. $I_{object} \in N(m_{f},\sigma_{f})$, $I_{background} \in N(m_{b}, \sigma_{b})$
						- Select the threshold according to equal error rate, i.e. $\mathcal{P}(\text{misclassifying background pixel})=\mathcal{P}(\text{misclassifying object pixel})$
						- Or select threshold according to $G_{m_{b},\sigma_{b}}(T)=G_{m_{f},\sigma_{f}}(T)$
						  ![[Pasted image 20251112162909.png]]
						- Otsus method: minimize inter-class variance
							- $w_{f}$ = relative frequence for object pixels
							- $w_{b}$ = relative frequence for background pixels
							- $\mu_{f}$ = estimated mean value for object pixel intensities
							- $\mu_{b}$ = estimated mean value for background pixel intensities
							- $\sigma_{f}^{2}$ = estimated variance for object pixel intensities
							- $\sigma_{b}^{2}$ = estimated variance for background pixel intensities
							- We minimize intra-class variance: $\sigma_{w}=w_{f}\sigma_{f}^{2}+w_{b}\sigma_{b}^{2}$
							- Equivalently maximize the inter-class variance: $\sigma_{e}^{2}=\sigma_{t}^{2}-\sigma_{w}^{2}=\dots=w_{b}w_{f}(\mu_{b}-\mu_{f})^{2}$
							- ![[Pasted image 20251112170034.png|550]]
							- Thresholding color images:
								- Select one threshold for each RGB channel
								- Select a plane in RGB space and define object pixels according to $k_{R}R+k_{G}G+k_{B}B\leq T$.
								- Both threshold T and normal to the plane have to be selected
								- select a reference color and a distance and define object pixels according to $(R-R_{\mathrm{Re}f})^{2}+(G-G_{Ref})^{2}+(B-B_{Ref})^{2} \leq d^{2}$
								- Could also use another color-space like HSV (Hue, Saturation, Value)
									- Hue: Color (rainbow)
									- Saturation: Whiteness (white balance)
									- Value: inteensity (=(R+G+B)/3)
								- Select threshold based on e.g. value or hue
				- Split and merge:
					- Region growing:
						- Goal: Divide image R into regions $R_{1},\dots,R_{n}$
						- Means: Use some criterion, e.g. if pixel intensities are similar.
							- $R=R_{1}\cup R_{2}\cup\dots \cup R_{n}$
							- $R_{i}$ connected
							- $R_{i},R_{j}$ disjoint
							- $P(R_{i})= \text{TRUE}$
							- $P(R_{i}\cup R_{j})=\text{FALSE}$
						- Algorithm:
							- Start with a number of "seed pixels", usually pixels that are known to lie within the objects of interest
							- Add neighboring pixels as long as $P(p_{1},p_{2})=\text{TRUE}$.
							- Repeat until no more pixels
							- Continue with new seed pixels if needed, e.g. if the object is not covered or if a new object needs segmentation
						- Selecting criterion P:
							- Depends on images and application
							- The difference between darkest and brightest pixels within a region should be less than T
							- The intensity of each pixel should not be more different than d from a pre-defined intensity m.
						- Very sensitive to selected parameters:
						  ![[Pasted image 20251112171653.png]]
					- Split and merge algorithm:
						- Start with the whole image as one initial region
						- In each step:
							- Iterate over all regions
								- If $P(R_{i})=\text{FALSE}$, then it is not similar, so we split into four smaller regions (2D)
								- If $P(R_{i}+R_{j})=\text{TRUE}$ for two neighboring regions, then they are similar, merge them to one.
						- Similarity can be measured according to critera P, in the same way as for region growing
						- We have to decide whether we have 4-connectivity (direct neighbors only) or 8-connectivity (include diagonal neighbors)
							- Thus a 4-connected path is a path through 4-connected neighbors, and vice versa for 8-connected paths
								- Further a 4-connected region is a collection of pixels where every pair of pixels have a 4-connected path, vice versa for 8-connected region.
		- Deep learning based.
			- Needs a lot of training data
	- The chosen method may or may not take neighboring pixels into account (independent classification or not), and it may or may not use prior information about the object e.g. shape, size, texture.
	- Critera for complete segmentation
		- Every pixel belongs to one region, and one region only
		- Every region is a connected collection of pixels
		- Each region is uniform (according to soem criterium)
		- Each pair of neighboring regions is non-uniform.
	- Distance transformation:
		- Important, can be used to extract skeletons
		- Compact representation
		- Introduce a metric in the image: $d(p,q),p=(x,y),q=(s,t)$
			- It should fulfill:
				- $d(p,q)>0, p\neq q$
				- $d(p,q)=d(q,p)$
				- $d(p,r)\leq d(p,q)+d(q,r)$
		- Examples:
			- Euclidean (2-norm)
			- Manhattan $d^4(p,q)=\lvert x-s \rvert + \lvert y-t \rvert$
			- Chessboard $d^8(p,q)=\max(\lvert x-s \rvert,\lvert y-t \rvert)$
			- Many more exist...
		- Definitions:
			- Distance for a path is the sum of the distances between consecutive pixels
			- Distance between two points is the shortest path
			- Distance between a region and a pixel is the shortest distance between the pixel and any pixel in the region.
			- Distance transform is the distance from each pixel in the image to a pre-defined set.
		- Shortest path segmentation:
			- Define the length between two neighboring pixels (usually short if intensities are similar and longer otherwise)
			- Define starting and end point
			- Find shortest path
			- Can be solved using Dijkstras

**Lecture 5 - Segmentation II (Active Shape Models)**
- Active Contours
	- We define a contour that moves over time (iterations) and is driven by external and internal forces
	- It aims to minimize a critera with external energy (fit to interesting structures) vs internal energy (regularizes the contour)
	- We parameterise the contour $V(s)=[x(s),y(s)]$
	- Minimization criterion $E[v(s)]=\int _{S} \frac{1}{2}(\alpha \lvert v'(s) \rvert^{2}+ \beta \lvert v''(s) \rvert^{2}) + E_{ext}(v(s)) \, dx$
		- Examples of external energies,
			- $E_{ext} = - \lvert \nabla I(x,y) \rvert^{2}$
			- $E_{ext}=-\lvert \nabla G_{\sigma}(x,y)*I(x,y) \rvert^{2}$
	- Practical aspects:
		- Need to specify $\alpha,\beta$
			- They determine the trade-off between internal and external energy as well as the weighting between first and second order derivatives (obviously)
		- The problem is variational since we minize an expression that depends on a function $v(s)$
	- Solution:
		- Euler-Langrage equations gives, $\alpha v''(s)-\beta v^{(4)}(s)-\nabla E_{ext}(v(s))=0$
		- Hard to solve, so we use trick, Dynamic snaker - Active contour
		  $v_{t}(s,t)=\alpha v''(s,t)-\beta v^{4}(s,t)-\nabla E_{ext}(v(s,t))$
			- If we find a stationary solution i.e. LHS=0 then we have a solution!
		- NOTE: we say $v_{t}$ is time derivative and $v'$ is spatial derivative.
		- Numerically we solve this by discretization:
			- $\delta =\frac{1}{\Delta T}$, $v_{t}=\frac{x_{k}^{n+1}-x_{k}^n}{\Delta t}$,$v'=\frac{x_{k+1}^n-x_{k}^n}{h}$
			- Discretization gives, ![[Pasted image 20251119164105.png]]
			- With the linear system of equations in x,
			  $A+\delta Ix^n=x^{n-1}-f_{x}(x^{n-1},y^{n-1})$
				- $x$ is a vector with all spatial coordinates
		- Pseudo Algorithm:
			- Start with an initial contour (inside or outside the object)
			- Calculate the parameterization using arclength
			- Propagate the contour one step basd on solving the linear systems of equations
			- Re-parameterize if needed
			- Continue until convergence
		- ![[Pasted image 20251119164415.png]]
		- Initialization from inside and outside can yield different results depending on how the structures look.
		- The issue with active contours is that they may get stuck with concave/indented shapes, we can solve this with Gradient Vector Flows:
			- The GVF makes edges influence the whole image with force, compared to the standrad which only influences with force.
- Contour evolution:
	- We have a moving curve, that moves according to some rule to minimize an energy or similar.
	- It has:
		- L = local properties
		- G = global properties
		- I = independent properties
		- F = speed function
			- Depends on image intensities, image derivatives, local curvature, etc.
			- It has to be carefully selected and adapted to the application
	- Fast marching methods:
		- Assume F>0 (contour only moves outwards)
		- We introduce a new image T(x,y) where T denotes the arrival time of the contour
		- The contour at time T is the collection of points with arrival time = T
		- We start with distance = rate * time in one dimension:
		  $dx=FdT\to 1=FT'(x)$
		- In several dimensions we use the Eikonal equation,
		  $\lvert \nabla T \rvert F=1$, $T=0$ at initial location
		- Pseudo algortihm:
			1. Start with initial contour (known points)
			2. Compute T for all neighbours to the contour (trial points)
			3. Add the point in trial with the smallest T to known
			4. Update T for all neighbors not in known and add to trial
			5. Repeat 3-4 until all points are in known
	- Level Set Methods:
		- Model the contour as the level set to a 3D-function $\Psi$, i.e $\Psi(x(t),t)=c$ (usually $c=0$), $\mathbf{x}(t)=(x(t),y(t))$
		- We differentiate with respect to t,
		  $\Psi_{t}+\nabla \Psi(x(t),t)x'(t)=0$
		- Outward normal is $n= \frac{\nabla \Psi}{\lvert \nabla \Psi \rvert}$
		- We assume that the speed is normal to the level set $F=x'(t)n$
		- Allowing a rewrite $\Psi_{t}+F\lvert \nabla \Psi \rvert=0$
		- Practical aspects:
			- $\Psi$ only needs to be known close to the level-set
			- $\Psi$ is usually chosen as a signed distance function:
			  $-d(x,\Gamma)$, inside $\Gamma$; $d(x,\Gamma)$ outside $\Gamma$
			- $\Psi$ can be constructed using distance transform or fast marching
			- narrow band algorithm (update $\Psi$ in each step)
			- numerical scheme: fixed grid, multigrid
	- Variational methods:
		1. Define the best segmentation of an image as the local minima to an energy functional, $E[\Omega]=\int _{\Omega} f(\Omega) \, dx$
		2. Write down the Euler-Lagrange equations, giving $dE[\Omega]=0$
		3. Introduce a dummy variable t (time) and solve $\Phi_{t}=dE(\Phi)$
			- $\Phi$ is a level set function corresponding to $\Omega$
		- Classical Chan-Vese Model:
			- Divide the image I(x) into two subsets $D_{0},D_{1}$ such that the following segmentation functional is minimized, ![[Pasted image 20251119171219.png|400]]
				- $\mu_{0},\mu_{1}$ are constant image intensities on $D_{0},D_{1}$
			- If the subsets are fixed, then the optimal parameter values are given by $\mu_{i}^*=\mu_{i}^*(D_{i})=\frac{\int D_{i} I(x) \, dx}{\int_{D_{i}} \, dx}$
			- May be sensitive to outliers.
		- Reduced functional:
			- $\hat{J}(\Gamma)=J(\Gamma,\mu^*(\Gamma))$
			- Solutions is found by gradient descent,
			  ![[Pasted image 20251119171513.png|300]]
		- Together:
			- Minimize a functional of the Chan-Vese form,![[Pasted image 20251119171629.png]]
				- Where we match $c_{1},c_{2}$ to the constant image intensities inside and outside the curve, and the last term denotes a measure on the curve.
			- ![[Pasted image 20251119171734.png|400]]
				- ...?
- Conclusion:
	- Toolbox of different segmentation algorithms
	- Each algorithm has to be adapted to the specific problem
	- Usually critical parameters have to be selected or estimated
	- Usually several different methods have to be tested
- Fast marching
- Level-set methods
- Variational methods
- Chan-Vese-segmentation
- Discussion

**Lecture 6 - Segmentation III (Modern segmentation methods)**
- Representing shapes:
	- A continous curve representing the contour of the object,
		- Result from segmentation algorithm
		- Needs to be represented in some way, e.g. Fourier series, splines, interpolation
	- A sampled set of points along the contour
		- Compact and simple
		- A continuous curve can be obtained by interpolation
		- Suitable for shape models
		- Needs to be evenly distributed
		- Advantageous if adapted to the shape
- Building a shape model:
	- We have a set of M examples of shapes
		- E.g. a number of pre-segmented shapes
	- We select N landmark points along the shape boundary $\mathbf{X}=(\mathbf{x_{1}},\dots,\mathbf{x_{N}})$
		- Each point contains the coordinates $\mathbf{x_{j}}=(x_{j},y_{j})$
	- We assume we know the correspondence between the different points in the different shapes
	- Comment on notation: The order of points in $\mathbf{x}$ are not important as long as one is consistent when transfering between the vector $\mathbf{x}$ and coordinates $(x_{j}, y_{j})$
		- Both $\mathbf{X}=[x_{1},y_{1},x_{2},y_{2},\dots]$ and $\mathbf{X}=[x_{1}x_{2},\dots x_{N},y_{1},y_{2},\dots,y_{N}]$ work.
	- Aligning the data:
		- The data needs to be aligned and evenly distributed
			- Evenly distributed is handled in Image Analaysis course
		- Alignment can be made by finding the best similarity transformation.
			- Done!
		- Algorithm for alignment:
			1. Align each shape to the first
			2. Calculate the mean of the t ransformed shapes (the mean value for each point)
			3. Align the mean shape to the first (to guarantee convergence)
			4. Align each shape to the mean shape
			5. Update the mean shape
			6. Iterate 3 to 5 until convergence (aka mean shape doesn't change significantly from previous iteration)
			- Mean shape is $\mathbf{\bar{x}}_{j}=\frac{1}{M}\sum_{i=1}^M \mathbf{x}^i_{j}$
	- The calculate the covariance matrix of the displacements from the mean shape,
	  $\mathbf{dX}^i=\mathbf{X}^i-\mathbf{\bar{X}}$
	  Covariance matrix = $S=\frac{1}{M}\sum_{i=1}^M\mathbf{dX}^i(\mathbf{dX}^i)^T$
	- Take the eigenvectors and values of S, $S\mathbf{P}^i=\lambda_{i}\mathbf{P}^i$
		- Eigenvectors are modes of variation
			- The eigenvector corresponding to the highest eigenvalue describes the most likely variation in the training data
			- Note that we have 2N eigen vectors due to 2 coordinates per point
		- Eigenvalues are significance of variation
			- We assume they are ordered decreasingly
	- We express the shapes with the eigenvectors,
	  $\mathbf{X}=\mathbf{\bar{X}}+\mathbf{Pb}$
		- $\mathbf{b}$ are the coordinates in the eigenvector basis $\mathbf{P}$
		- Coordinates in $\mathbf{b}$ can be interpreted as the amount of variation in the different variation modes
	- Notation... again:
		- $\mathbf{X}=[x_{1}y_{1}x_{2}y_{2},\dots]^T$
			- same for $\mathbf{P}^i$
		- while $\mathbf{x}=\begin{bmatrix} x_{1} & x_{2}\dots \\ y_{1} & y_{2} \dots \end{bmatrix}$
			- same for $\mathbf{p}^i$
	- Visualizing the modes:
		- Plot the mean shape $\mathbf{\bar{x}}$
		- Plot the mean shape plus/minus a suitable multiple, k, of each mode, $\mathbf{\bar{x}} \pm k \mathbf{p}_{i}$
			- Usually we select $k=2\sqrt{ \lambda_{i} }$
			- It is also useful to plot for several $k\sqrt{ \lambda_{i} }\mathbf{p}_{i}$ in the same figure
				- Note the 2 taken away from above
	- We select only the first t modes of variation, since they contain the majority of information,
	  $\mathbf{P}_{t}=(\mathbf{P}^1\mathbf{P}^2\dots \mathbf{P}^t)$
	  $\mathbf{b}_{t}=[b_{1}b_{2}\dots b_{t}]^T$
		- How do we select t?
			- Look at the goemetric appearance of each mode and select relevant ones
			- Determine how much energy you want to preserve
				- Total energy is $E=\sum_{i=1}^{2N}\lambda_{i}$
				- Relative contribution for each mode is $\lambda_{i} / E$
				- Contribution of the first t modes is $E_{t}=\sum_{i=1}^t\lambda_{i}$
				- Select for isntance t such that $E_{t} / E = 95\%$
	- We approximate,
	  $\mathbf{X} \approx \mathbf{\bar{X}}+\mathbf{P}_{t}\mathbf{b}_{t}$
	- How do we find $\mathbf{b}_{t}$?
		- Form $\mathbf{X}-\mathbf{\bar{X}} \approx \mathbf{P}_{t}\mathbf{b}_{t}$
		- Multiply by transpose of $\mathbf{P}_{t}$ and solve least squares,
		  $\mathbf{b}_{t}=\mathbf{P}_{t}^{\dagger}(\mathbf{X}-\mathbf{\bar{X}})$
	- In the end we have the shape:
		- $\mathbf{Y}=T_{s,R,t}(\mathbf{\bar{X}}+\mathbf{P}_{t}\mathbf{b}_{t})$
			- $T_{s,R,t}(x)=sR(x+t)$
- Segmentation using a shape model:
	- Given a shape model and an imgae with an edge map
		- Mean shape and transformation matrix of shape model are known
	- We want to optimize some criteria over estimated pose and shape parameters
	- Algorithm:
		- Initialize $s,R,\mathbf{t},\mathbf{b}_{t}$
			-  This gives initial shape $\mathbf{X_{0}}$
				- I think this means $\mathbf{X}_{0}=\mathbf{Y}=T_{s,R,t}(\mathbf{\bar{X}}+\mathbf{P}_{t}\mathbf{b}_{t})$ above
		- Find edges: At each landmark find the closest edge point orthogonal to the countour, giving the points $\mathbf{Y}=(\mathbf{y}_{1},\dots,\mathbf{y}_{N})$
		- Adjust pose: Adjust pose parameter to the best fit of the new $\mathbf{Y}$ points based on the current estiamte of $\mathbf{b}_{t}$
			- I.e. we do the similarity transform from $\mathbf{X}$ to $\mathbf{Y}$
		- Adjust shape parameters:
			- Transfer the new points $\mathbf{Y}$ back to the shape space using the inverse similarity transformation, giving the new shape space points $\mathbf{X}$
				- Inverse similairty transform: $\hat{y}=s^{-1}R^T(y-t)$
			- Calculate displacement vector $\mathbf{dX}=\mathbf{X-\bar{X}}$
			- Update shape parameter $\mathbf{b}$
		- Recompute shape: Calculate $\mathbf{X}$
		- Repeat until convergence
	- We need to solve:
		- $\mathbf{X+dX}=\mathbf{\bar{X}+P_{t}(b_{t}+db_{t})}$
		- Using $\mathbf{X=\bar{X}+P_{t}b_{t}}$ gives $\mathbf{db_{t}=P_{t}^T dX}$
		- Iterate until convergence...
	- Initialization:
		- Segment based on the edge map using any segmentation algorithm
		- Estimate the pose parameters using Procrustes
		- Estimate the shape parameters using $\mathbf{b}_{t}=\mathbf{P}_{t}^T(\mathbf{X}-\mathbf{\bar{X}})$
			- Note: it could be a good idea to restrict the shape parameters according to $-3\sqrt{ \lambda_{t} }\leq \mathbf{b}_{t}\leq 3\sqrt{ \lambda_{t} }$
		- Alternative initialization:
			- Segment based on simple registration e.g. thresholding
			- Then calculate the centre of gravity and the moments and axes of intertia for the binary image obtained
			- Then select the transformation parameters such that the centre of gravity, axes of inertia and total area coincide with a transformed mean shape
			- Use the transformation parameters along with $\mathbf{b}=0$ as an initialization
			- Points along the segmented shape are now easily obtained from the transformed points on the mean shape.
		- Example with grayscale image:
			1. Use transformed mean shape as a first approximation
			2. Determine profiles for each model point
			3. Compare gray-levels to obtain new points, Y
			4. Estimate the model parameters corresponding to the new points by minimizing $\lvert \mathbf{Y}-T_{x_{tr}y_{tr},s,\theta}(\mathbf{\bar{x}+P_{t}b}) \rvert^{2}$
			5. Iterate from 2 until convergence.
			- Something about a scale pyramid