
Unit 0 - Norms:
- non-singular:
	- All the usual stuff with rank, inverse range and null space,
	- 0 is not an eigenvalue
	- 0 is not a singular value
- Orthonormal matrices are either rotations or reflections, they preserve angles and lengths

Unit 1:
- Vector norms:
	- p-norm = Hölder norm 
	- 1 norm, 2 norm, inf norm
	- p-norm is always max diagonal element if A is diagonal
	- Cauchy schwarz  inequality,  special case of hölder inequality
	- Two norms are equivalent if we can bound the norm with the other only using coefficients
- induced matrix norms:
	- definition, with or without circle.
	- 1-norm, inf norm, 2-norm
	- spectral radius is maximal eigenvalue
	- Cauchy schwarz  inequality,  special case of hölder inequality. but now norm instead of absolute value
	- We can bound $\mid\mid AB\mid\mid \leq\mid\mid A\mid\mid\mid\mid B\mid\mid$
	- $\mid\mid A^n\mid\mid \leq \mid\mid A\mid\mid^n$
- general norm:
	- Frobenius norm
		- square of trace of ATA
	- matrix is orthogonal if $Q^TQ=QQ^T=I,Q^T=Q^{-1}$. Only if columns are orthogonal and is square.
	- 2-norm and Frobenius are invariant with orthogonal matrices.
		- Also holds if Q isnt square

Unit 2/3 - SVD:
- $AV=U\Sigma$
- When a value is singular the svd hyperellipse colapses on that that axis.
- left/right singular vectors, singular values
- Form of SVD
- ==Every matrix has an svd with unique singular values==
- How to compute SVD:
	- create ATA
	- singular values are sqrt of eigenvalues of ATA
	- and eigenvectors, vj are of those eigenvalues
	- uj from Avj/sigmaj
		- ==if sigmaj is zero, compute it to be orthogonal with previous uj, e.g. with G==
	- for full svd: 
		- ==use G-S to make extended orthonormal basis==
- V* preserves the sphere
  sigma strteches the sphere into hyperellipse
  U rotates or reflects hyperellipse (without affecting shape)
- SVD and eigenavlue decomposition coincide if A is symmetric
- Can solve linear systems with SVD:
	- we transform to diagonal system $\bar{b}=\Sigma \bar{x}$.
		- ==if over determined we will get a sigma with some rows of zeros==
		- ==if under determined we will geta sigma with columns of zeros==
- Stuff we can deduce:
	- rank of A = number on nonzero singular values
		- ==proof: write as svd and note U and V has full rank==
	- the range of A is the span of uj up until the rank = number of nonzero singular values
		- ==proof: skriv x som linjär kombinationer av v. som vi ser blir alla nollade pga av satsen ovan. $Av_{i}=U\Sigma V^Tv_{i}$ produces scales of U up intil the rank. and vi are linear independent so yes.==
	- $\mid\mid A\mid\mid_{2}=\sigma_{1}$
		- Proof: use definition of 2 norm
	- $\mid\mid A\mid\mid_{2}=\sqrt{ \sum\sigma_{i}^2 }$
		- Proof: insert SVD, svd invariant under norm, 
	- The singular values of A are the sqr roots of eigvals of ATA
		- Proof: show ATA is similar to SigmaTSigma
	- Singular values of a symmetric matrix are the absolute values of its eigenvalues
		- Proof: Note $A=Q\Lambda Q^T=Q|\Lambda|sign(\Lambda)Q^T$ which we also know because $A^T=A$ (insert SVD)
	- If A is square, determinant of A is product sum of singular values. 
		- Proof: determinant split, and det Q is 1
- Low rank matrices:
	- $A=\sum\sigma_{j}u_{j}v_{j}^T$
		- We only need as many as the rank of A, rest become zero obv.
		- Proof: Obv from $A=U\Sigma V^*$
	- If we add a subset of these then $\mid\mid A-A_{\nu}\mid\mid_{2}$ is the smallest possible norm when approximateing A with a matrix B of that rank. and this is equal to $\sigma_{\nu+1}$ or 0.
		- Same result for Frobenius norm
		- This is the basis for image applications and such
		- Works well if A has a few large singular values.
		- proof: complex but has to do with showing the contracdiction of it not being the best approximation and using the norms to show the dimensions dont match up. and say you can at least show that norm of full A, full SVD, U and V invariant, so sgima is left of whichh it is the biggest. now of course if we remove all of those we will have the next to biggest.
	- Image compression:
		- Make image to matrix
		- Do svd and keep big ones
	- Data analysis:
		- SVD will give the vectors of the linnear parts as columns in U for the nonzero singular values.
		- Proof sketch: SVD is eeesntially a linnear scale along some dimensions. so svd will identify what vector bases in u we can superposition to represent our new solution, we identify these with singular value 1 or 0.
- Projections:
	- PP=P
	- Projects onto range(P) and along ker(P)
	- complementary projection: I-P
	- Splits v into two spaces
	- Orthogonal iff P=PT
		- Does not mean P is orthogonal matrix
		- components that belong to null space become 0 due to orthogonality
	- Onto orthonormal basis:
		- P=QQT
		- P=PT still, so symmetric which means svd becoes eigenvalue decomposition and since normal it simply becomes $P=QQ^T$
	- Generally:
		- P=A(ATA)-1AT

Unit 4 - QR decomposition:
- Gram Schmidt (**not very stable**)
	- ==take a vector, inner product and remove that component from our vector, normalize and then remove that and the one before. and so on==
	- $r_{ij}=q^Ta_{j}$
- ==All matrices have reduced QR factoization==
- Householder reflection / Householder triangularization:
	- Project a vector to the first axis.
	- So for each iteration we do $Q_{k}=[I 0; 0 H_{k}]$.
	  We decide $H_{k}$ so that it reflects the next column to the first element of row k. $[c,d]$ onto $[X,0]$.
	- $H=I-\frac{2vv^*}{v^*v}$.
	- $v=-x\mid\mid x\mid\mid - e_{1}$
	- ==Can multiply by matvecs if we factor Ha, a inside. Effective.==
	- Affects the bottom right square of the matrix
- GS does a series of R to orthogonalize
- Householder does a series of U to triangularize
- Null space of a matrix:
	- If rank k is less than cols, we will see that R can be factorized as Upper traingular kxk, square $(n-k)*k$, 0 and 0.
		- Proof: Think householder triangularization. it terminates its R when all the next rows are zero, aka weve projected the last part of the vector to an axis, theres nothing more to project.
	- If we split $Ax=QRx=[Q_{1},Q_{2}][R_{1}S;00][x_{1};x_{2}]=0$ we can write this out and find an expression for $x_{1}$ using $x_{2}$, which gives a general solution with the parameter $x_{2}$ and the null space basis $V=[-R_{1}^{-1}S;I]$  .  

Unit 6 - Least Squares:
- Solving Ax=b, becomes a minimization problem.
- Solution is projecting b onto A
- Vandermonde system is 1, x1, x1^2 and so on for each data point per row. c vector. and yhen y answer
	- Full rank if we dont have identical x data points
	- Solve by projection $P_{V}=V(V^TV)^{-1}V^T$ and remember A is V.
- ==Normal equations are smart because they always have a solution $A^TAx^*=A^Tb$==
	- ==since $range(A^T)=range(A^TA)$== 
	- ==$x^*$ is unique iff $A^TA$ is nonsingular iff A has full rank==
		- ==if A has full rank, we have the LS solution which is the pseudo inverse $A^{+}=(A^TA)^{-1}A^T$==
- Solution methods:
	- Normal equations and cholesky
	- QR factorization
	- SVD

Unit 7:
- $f$ is a solution operator for a problem
- Well conditioned if small difference
- ==Absolute condition number: $\hat{\kappa}(x^*)=\lim_{ n \to 0 } \sup  \frac{\mid\mid\delta f\mid\mid}{\mid\mid \delta x\mid\mid}$.==
	- ==if $f$ differentiable, $\hat{\kappa}(x^*)=\mid\mid J(x^*)\mid\mid$==
		- ==from taylor expansion==
- Relative condition number (to put things in scale):
  $\kappa(x^*)=\lim_{\delta \to 0 }\sup \frac{\frac{\mid\mid \delta f\mid\mid}{\mid\mid f\mid\mid}}{\frac{\mid\mid \delta x\mid\mid}{\mid\mid z\mid\mid}}$
	- If f differentiable: $\kappa(x^*)=\frac{\mid\mid J(x^*)\mid\mid}{\frac{\mid\mid f(x^*)\mid\mid}{\mid\mid x^*\mid\mid}}$
	- ==Thumb rule: $\kappa(x)\leq 10^6$==
- ==Condition number of Matrix Vector Multiplication:==
	- $x \to Ax$
		- If A invertible: $\kappa(A) \leq\mid \mid A\mid\mid\mid\mid A^{-1}\mid\mid$
	- Equally for $b \to A^{-1}b$
		- If A invertible $\kappa(b) \leq\mid \mid A\mid\mid\mid\mid A^{-1}\mid\mid$

Lecture 8:
- *Solving Ax=b (also called inverse problem) with SVD, QR, Normal eq., shows most expensive is normal, then SVD, then QR.*
- Inverse problems tend to be ill-conditioned wrt b, as in small errors in b cause large changes in the solution x.
- For well-conditioned problems use stable algos. to not make things worse.
- Ax=b A is nxn => Any method needs to relate $n^2$ entries to x which means we need minimum $O(n^2)$. **I like this reasoning**. We do not know if such an algo exists.We know a lower bound.
- Comparing solutions to Ax=b:
	- *Gaussian elimination is $\frac{2}{3}O(n^3)$. Good up until 50,000*
	- Solving inverse with GE and applying is bad idea. DONT! If A is orthogonal though $A^{-1}=A^{T}$ then inverse is free and we get $O(n^2)$.
	- *Cramer's Rule - Determinants scale (n+1)!, unsuable for n>20*
	- Real alternatives:
		- Normal eq. via Cholesky factorization fastest but not always stable with rounding errors
		- QR slower but stable. $O\left( \frac{4}{3}n^3 \right)$, also good <50,000
		- SVD if A almost rank deficient.
	- To note here: all these methods are
		- direct
		- exact solution after some fixed amount of operations
		- black box = does not explot structure of A
	- *later we will use iterative methods that are the oppostie of this: GMRES needed for >100,000*

Lecture 9:
- LU algorithm (practical without matrices) = Gauss Elimination viewed as a factorization:
	- for k
		- for j = k+1:
			- $l_{jk}=\frac{u_{jk}}{u_{kk}}$
			- $u_{j,k:m}-=l_{jk}u_{k,k:m}$
- L is lower triangular
- U is uppper triangular
- The factorization is $\frac{2}{3}O(n^2)$
- If we solve Ly=b is easy = forward substitution $O(n^2)$
- Ux=y = back substitution $O(n^2)$
- LU always exist for any nonsingular matrix but sometimes we need pivoting. THIS MAKES SENSE CUZ WERE JUST DOING THE INVERSE BASICALLY
- pivoting also if diagonal element is Veeery small becuase huuuuge resulting $l_{jk}$.
- complete pivoting is expensive, so we do partial
- for each elimination we record a P to the left of A and then swap our L and U. so we change our A with P to make L and U safer. and then we record each P to reverse afterward.
- pivoting algorihtm:
	- for k
		- pick pivot row with max element
		- if j is not k:
			- swap rows of U
			- swap rows of L
			- swap rows of P (record change)
			- compute
	- when solving Ax=b we do PAx=Pb <=> LUx=Pb instead
- edge case: i guess pivoting with biggest element can be bad if it is too big? like bigger than our range, tho that is not realistic anyway

Lecture 10:
- When can positive definite matrices be exploited to speed up algorithms?
- If we have a a spd then its principal submatrix is also spd. this is the basis of cholesky factorization.
- For each submatrix we factorize our matrix with a lower (left) and upper (right) triangular matrices that are each others transpose. Doing this repeatedly expands more and more lower and upper triangular matrices around that central identity-becoming spd matrix. we can then merge this expression to just $LL^T$ or $R^TR$
- **understand proof in homework**
- ==Cholesky factorization is dterministic and gives unique factorization.==
- ==LU decomposition does not retain spd. and using these properties is key to faster algorithms.== the cholesky factorization retains positive definite since $LDL^T=L\sqrt{ D }\sqrt{ D }L^T=L\sqrt{ D }(L\sqrt{ D })^T$ which is the cholesky form
- iterative algs are state of the art.

Lecture 11:
- If X is invertible/nonsingular then $XSX^{-1}$ is a similarity transform.
	- preserves eigenvalues, and thus traces, char. polynomial and determinants
	- but not eigenvectors!
- A is normal ($A^TA=AA^T$) => symmetric
	- Normal matrices are diagonalizable with an orthogonal system of eigenvectors:  $Q\Lambda Q^T$
- More generally
	- ANY nxn matrix have a Schur form $T$: $A=QTQ^T$.
	- Proof by induction over matrix dimension n. See book.
- Thus we have three stages of **eigenvalue revealing factorizations**:
	- $A=X\Lambda X^{-1}$ : <mark style="background: #FFF3A3A6;">diagonalization : if A is nondefective</mark>
	- $A=Q\Lambda Q^T$ : <mark style="background: #FFF3A3A6;">unitary diag. : if A is normal</mark>
	- $A=QTQ^T$ : <mark style="background: #FFF3A3A6;">Schur factor. : ALWAYS</mark>
	- If A is normal Schur becomes unitary diag.
- If A symmetric, reduce computational work by half.
- Unitary matrices tend to make stable algorithms
- Rayleigh quotient:
	- $r(x)=\frac{x^TAx}{x^Tx}$
	- For any eigenvector it is equal to its eigenvalue.
	- It is also functions as a way to say what scalar acts most like an eigenvalue to that vector
	- $\nabla r(q_{j})=0$ for any eigenvector
	- They are quadratically accurate by taylor expansion
- Strictly diagonal dominant matrices
	- Strictly (row) diagonally dominant if every diagonal is more than the sum of the rest of the row
	- ==invertible/nonsingular
	- ==numerically stable
	- symmetric + SDD = spd
- Gerschgorins Theorem 1:
	- exists $|\lambda-A_{ii}|<$i row sum
	- ==proof: opposite means $\lambda I-A$ is SDD which means invertible which cant happen since determinant is zero for eigenvalue duh==
- Gerschgorin disk
	- Make a disk with radius of each row sum excluding diagonal, centered around diagonal.
	- Theorem 1 says every eigenvalue is within at least one of the disks! notice how it says there exists i, so several lambda can have the same i.
- Gerschgorins Theorem 2:
	- for each non disjoint union of gerschgorin disks there are as many disks as eigenvalues
	- small disks => strong diagonal dominance which makes sense cuz then eig vals are close to the diagonal entries.
	- SDD => no disk contains 0 eigenvalues
	- proof: have a factor p for all non diagonal entries. from p = 1 which we start with to p=0, where each eigenavlue belongs to its own disk we follow the eigenvalue paths and since they must be continous we can see that the disk must always follow the "areas" aloowed by the disks. it cant be discontinous. think growing and shrinking disks
- Search engines:
	- webcrawlers search the webs and store hyperlink, index pages and ranks importance.
	- PageRank:
		- Track importance by how many sites point to it
			- each website gives each website it links to 1/hj of its importance.
		- Hyperlink matrix. each row summed up is the importance for a website. each col is the importance it gives, which sums to 1.
		- by setting $x=[PR(1) PR(2) \dots]$ then each row product when doing Hx simply become x. so H is eigenvector with lamda=1. we can explot this
		- if matrix has nonnegative entries and columns sums to one = column stochastic.
			- they have 1 as eigenvalue. easy proof, $e=[1, 1, 1]$ is an eigenvec to $A^T$ with eigen val 1 since it becomes scalar product sum the row. and thus also eigenval to A
		- Problem: if not outgoing links then it doesnt sum to 1.
			- Solution: We construct the Google matrix which just factors H by alpha and adds 1-alpha divided by n to all entries, which maintains column stochastic.
			- Now we solve by iterative solvers!!!


Lecture 13:
- Solving $Av=\lambda v$ by char. poly. is only realistic for $\leq 4$. now we need something iterative
- Iteration => we assume A is symmetric => diagonalizable with orthogonal similarity transformation $A=Q\Lambda Q^T$.
- Power Iteration:
	- Pick an arbitrary vector v and apply A, and then norm time and t ime again. v will converge to largest eigenvector (that it has a component in).
	- Convergence rate: $\frac{|\lambda_{2}|}{|\lambda_{1}|}$.
	- It converges since we can write v as a linear combination of eigenvectors. $A^kq_{i}=\lambda_{i}^k q_{i}$ shows that if we factor out $\lambda_{1}$ the rest will tend to zero.
- Inverse power iteration:
	- Instead of making the largest dominate we can make the smallest, by doing it for $A^{-1}$.
	- Algorithm:
		- Solve $Ay_{k+1}=x_{k}$
			- by Cholesky if full rank and well conditioned, otherwise LU, etc.
		- Normalize $y_{k+1}$
- Shifted Inverse Power Iteration:
	- Now we target a specific eigenvalue $\mu$ by using a shift $(A-\mu I)$ and use that in inverse power iteration. This makes the closest eigenvalue to that the smallest.
	- This is because $Av=\lambda v$ so $(A-\mu I)v=Av - \mu v=(\lambda-\mu)v$ which means each eigenvalue is this reduced by $\mu$ amount.
- In both these algorithms we approx. the eigenvalue from that eigenvector by the rayleigh quotient for $y_{k+1}$.
- Simultaneous Power Iteration:
	- We begin with some orthonormal matrix Q. Each step we apply A as before. But on the result we Take the QR, and that Q becomes the start of the next step.
	- 1) Since theyre constantly kept orthogonal they will be kept from all converging to the biggest eigenvalue, and 2) With every the same reasoning as with normal power iteration each will converge to eigenvalues. **Im trying to say that each vector will have some eigenvalue that dominates + orthogonality forces them to adopt different ones** 
- QR Algorithm:
	- $A_{0}=A$
	- $Q_{k}R_{k}=A_{k-1}$ (QRa den)
	- $A_{k}=R_{k}Q_{k}$ (recombine in reverse order)
	- This is the same as applying $A_{k}=Q_{k}^TA_{k-1}Q_{k}$ at each step. This is a similarity transform so eigenvalues preserved.
	- One can explain its converge as being the same as simultaneous power iteration as we essentially apply A again and again but through Q.
	- A ends up as either:
		- Diagonal, if A normal. Q are the eigenvectors, as seen by identification.
		- Upper triangular, otherwise. Solve $(T-\lambda_{i}I)y_{i}=0$, $v_{i}=Qy_{i}$ for eigenvectors. Easy, uppertriangular.
	- Compared to simultaneous power iteration where we get the eigenvectors and use rayleigh quotient for the eigenvalues. 
- QR and simultaneous generate identical sequences of matrices. 
- Practical QR to make it $O(n^3)$:
	- 3 adjustments:
		- ==1. Before start, reduce to tridiagonal form, through HH reflectors.==
		- 2. Instead of $A_{k}$ factor a shifted matrix $qr(A_{k-1}-\mu_{k}I)$ and then $A_{k}=R_{k}Q_{k}+\mu_{k}I$. E.g. some diagonal. This works similar to shifting in power iteration. 
		- ==3. Whenever possible break into submatrices, especially when eigenvalue is found. This splits the matix into $[[A1, 0] [0, A2]]$, which i justified by doing $det(\lambda I-A)$ for this expression which means the upper right becomes zero anyway.== 


Lecture 15:
- Now we assume square very large matrices
- Sparse
- We assume we know how to compute Ay efficiently for any y.
- We want to solve $Ax=b$ or $Ax=\lambda x$
- Matrix valued polynomials:
	- $p(A)=p(SBS^{-1})=Sp(B)S^{-1}$. Especially $p(A)=Xp(\Lambda)X^{-1}$
- Cayleigh Hamilton Theorem:
	- $\chi(z)$ be char. poly. of A, then $\chi(A)=0$.
	- Proof: for nondefective at least, use $Xp(\Lambda)X^{-1}=0$
	- => If A is invertible, $A^{-1}=-\frac{1}{a_{0}}A^{m-1}-\frac{a_{m-1}}{a_{0}}- \dots-\frac{a_{1}}{a_{0}}I$.
	- <mark style="background: #BBFABBA6;">Thus the matrix inverse can be expressed by a matrix polynomial of exact degree m-1. Thus we can approx. $A^{-1}$ using matrix polynomials.</mark>
- Krylov subspaces:
	- A chain of subspaces with increasing dimension.
	- $K_{n}=span(b, A{b}\dots,A^{n-1}b)$
	- **Note n-1**
	- Thus we can express any x (e.g. the solution) in $K_n$ as a lin.comb. of these bases. $x=(\sum^{n-1}_{i=0} \alpha_{i}A^i)b=p_{n-1}(A)b$. Aka a matrix polynomial of A with order n-1 where the coefficients are the coordinates.
	- Krylov spaces consists of maximally m spaces but it can stop earlier. Once $K_{n}=K_{n+1}$, the rest of the spaces will be the same.
- ==Hessenberg form: $A=QHQ^T$==
	- ==Upper triangular + first subdiagonal==
	- ==<=>$AQ=QH$== 
	- If we just want the first n cols, $Q_{n}$, we can write $AQ_{n}=Q_{n+1}\tilde{H}_{n}$ Where we add an extra col on Q and an extra row on H to bring along the whole first subdiagonal
- Arnoldi iteration:
	- Constructs orthonormal basis of a krylov subspace iteratively by MatVecs only (no other operations with A). $K_{n}=span(b, A{b}\dots,A^{n-1}b)=span(q_{1},q_{2},\dots,q_{n})$.
	- ==From the Hessenberg n size expression above, the last column $q_{n}$ gives the recurrence relation: $q_{n+1}=\frac{1}{h_{n+1,n}}(Aq_{n}-h_{1n}q_{1}-\dots h_{n,n}q_{n})$.== Where we can get each coefficient by $q_{i}^TAq_{n}=h_{1i}$ as seen if we multiply with the expression above considering orthogonality. This is expensive though as we need to do it n times.
	- ==See algorithm in 33.1 in book. We take $v=Aq_{n}$ as our vector according to the formula above and then we calculate each h coefficient by projection and subtract its corresponding term. In the end we only have $v=\frac{Aq_{n}}{h_{n+1,n}}$ so $h_{n+1,n}$ is just the norm and we thus have the next base.==
	- q1= normed b
	- essentially the same thing as gram schmidt
- Arnoldi Iteration for Eigenvalue computation:
	- We can write $AQ_{n}=Q_{n+1}\tilde{H}_{n}$ => $Q_{n}^TAQ_{n}=Q_{n}^TQ_{n+1}\tilde{H}_{n}=H_{n}$ where $H_{n}$ is just the square nxn matrix with last row having two elements due to kept subdiagonal. This is a similarity transformation if n is same as dim(A), so this transformation shouldnt skew our eigenvalues. Does it approximate them well? We answer this in the next bullet section
	- When we jump out of Kn by multiplying with A, we can jump back by projection $P_{K_{n}}=Q_{n}Q_{n}^T$.
	- ==Eigenvalues of $H_{n}$ are called Ritz-values.== Arnoldi eigenvalue estimates of A.
	- The "Arnoldi" part is finished after have have calculated $H_{n}$, the rest is a separate algorithm of our choice. So arnoldi only tells us how to approximate the matrix while preseving eigenvalues (approximately), not an actual algorithm to calculate the eigenvalues.
	- Then we can use QR algorithm
- XXXX:
	- An element x that belongs to $K_{n}$ can be written as $x=c_{n-1}A^{n-1}b+\dots+c_{1}Ab + c_{0}b$. $x=q(A)b$
	- if $c_{n-1}=1$ it is called **monic**. The set of monic polynomials of degree n are denoted $\Pi_{n}$. Char. poly. are monic.
	- $min_{p\in\Pi_{n}}\mid\mid p(A)b \mid\mid_{2}$ is the Arnoldi approximation problem. if n=m then char. poly. is the solution since $\chi(A)b=0$ from Cayleigh-Hamiltons theorem.
	- Theorem: If dim$K_{n}=n$, then the unique solution of the Arnoldi approximation problem is $p^n=\chi_{H_{n}}$, i.e. the char.poly. of the Hessenberg matrix at the n-th stage of Arnoldi iteration. *As such n=m is $\chi_{A}$ makes sense since H is from a similarity transform at that point with no compression*.
	- This is why we approximate eigenvalues of A with eigenvalues of $H_{n}$.
	- A way to view this is $q(A)b=A^nb+z$, $z \in K_{n}$, $z =Q_{n}y$ for some $y$. Thus Arnoldi approx. problem becomes a least squares problem. Where the solution y is given by $Q^T_{n}(A^nb-Q_{n}y)=0$ <=> $p_{n}(A)b \perp K_{n}$ 
	  ![[Pasted image 20251025174623.png]]
	- Proof of theorem:  DO THIS LATER 
- GMRES:
	- Use Krylov spaces to construct an approximate solution to linear equation systems $Ax=b$. Aka find $x^*= A^{-1}b$.
	- We approximate the solution x* by $x_{n} \in K_{n}$, which solves $\mid\mid Ax_{n}=b\mid\mid=\min_{x \in K_{n}}\mid\mid Ax-b\mid\mid$ => residual is $r_{n}=b-Ax_{n}$.
	  ![[Pasted image 20251025175731.png]]
	- Running Arnoldi algorithm gives an orthonormal basis of $K_{n}$ being the columns of $Q_{n}$, i.e. find $y_{n}$ such that $\min_{x \in K_{n}}\mid\mid Ax-b\mid\mid=\min_{y \in R^n }\mid\mid AQ_{n}y-b\mid\mid$. Which is a least squares problem!
	- To solve this least squares problem:
		- We know $AQ_{n}=Q_{n+1}\tilde{H}_{n}$. Denoting the solution to the minimization problem $y_{n}$. We can write
		  $\mid\mid Q_{n+1}\tilde{H}_{n}y_{n}-b\mid\mid=\min_{y \in R^n}\mid\mid Q_{n+1}\tilde{H}_{n}y-b\mid\mid$.
		  We can simplify to,
		  $\mid\mid \tilde{H}_{n}y_{n}-Q_{n+1}^Tb\mid\mid=\min_{y \in \mathbb{R}^n}\mid\mid \tilde{H}_{n}y-\mid\mid b\mid\mid e_{1}\mid\mid$.
		- b is just the norm of e1 as we choose q to be normed b when we initialize.
		- This reduces the dimensions vastly
	- Termination criterion:
		- Optimal choice is to solve is QR decomposition using Givens rotation. This allows us to calculate the LS solution at each iteration without having to redo the entire calculation, we just add another rotation at the bottom right. This eleminates the extra subdiagonal.  And because the LS norm is invariant to it, we only now have to solve "Rny=". And what we get is a system of Rn is upper triangular with a full zero bottom row from the removed subdiagonal. The nice part here is that since it is zero we cannot "help this dimension", and so when it equals the last element of the also rotated gn it becomes the residual error we cannot account for. As such we dont have to recalculate the qr at each frame, we just apply a givens matrix and then solve the upper triangular system.
		- To clarify we solve by the top submatrix $R_{n}y=g_{n}$ follwed by $x_{n}=Q_{n}y$ and then we terminate when $\mid\mid r_{n}\mid\mid_{2}=\mid \gamma_{n+1}\mid$ is low enough.
		- Even better, we have this value without solving the ls problem, so we compute $x_{n}$ first after we've fulfilled the  termination criterion.
	- Polynomical formation
		- GMRES approximation problem: $\min_{p_{n} \in P_{n}}\mid\mid p_{n}(A)b\mid\mid$. Look at the form were finding the best approximation for $A^{-1}$. 
		- Since GMRES by definition picks the polynomical that minimizes this, remember:
		  ![[Pasted image 20251026100821.png]]
		- Thus we have that the solution to the GMRES approximation problem is the residual aka $\mid\mid r_{n}\mid\mid=\mid\mid p_{n}(A)b\mid\mid \leq\mid\mid p(A)b\mid\mid$.
		- Using this theorem ^ we can prove some finite termination results, by choosing an appropriate polynomial in $P_{n}$ that makes the right hand side in the theorem 0.
			- E.g. Theorem: If A is nonsingular then GMRES will find the exact solution within m iterations.
				- Proof: We can construct a polynomial (of length m) that is simply the characteristic polynomial. But we need it to be $p(0)=1$ so we normalize it and $\chi(0)=\det(a)$ which works if we are non singular.
			- E.g. Theorem: For diagonalizable matrices, $A=V\Lambda V^{-1}$ we have: $\frac{\mid\mid r_{n}\mid\mid}{\mid\mid r_{0}\mid\mid} \leq \kappa_{2}(V) \max_{z \in \sigma(A)}|\bar{p}(z)| \forall p \in P_{n}$.
				- This basically says: GMRES reduction of residual is bounded by the minimum polynomial when looking at the max distance of polynomial to a spectral value on the x-axis, while pinned to 1 at 0. The $\kappa_{2}=\frac{\sigma _n}{\sigma_{1}}$ means and relates to the fact that if our eigenvalues are close (clustered) it is easier to zero in on all spectral values (they lie on a line). And if we have a normal matrix it is 1.
					- ==Proof: $\mid\mid r_{n}\mid\mid_{2}=\mid\mid p_{n}(A)r_{0}\mid\mid=\mid\mid Vp_{n}(\Lambda)V^{-1}r_{0}\mid\mid \leq \mid\mid V\mid\mid\mid\mid p_{n}(\Lambda)\mid\mid\mid\mid V^{-1}\mid\mid\mid\mid r_{0}\mid\mid$. Divi==sion and realizing the definition of $\kappa_{2}$, and realizing the 2 norm of $p_{n}(\Lambda)$ simply is the maximum of $p_{n}(\lambda_{i})$ since the 2 norm measures spectral radius. 
					- Corollary: We only need as high of order of polynomial as there are distinct eigenvalues to get the perfect solution.
				- Theorem: 
	- Preconditioning:
		- Preconditioning transforms your problem so that your iterative solver sees a matrix closer to the identity — done either by left- or right-multiplying by an approximate inverse $P^{-1}$.  In practice, $P^{-1}$.
		- Left: Instead of Ax=b solve $P^{-1}Ax=P^{-1}b$.
			- easy to invert P where P-1A is approx I so easy to solve
			- We replace all MatVecs Av with first v=Pinvv
				- i.e. we our residual becomes $r=P^{-1}(Ax-b)$
		- Right: $AP^{-1}y=b$ and then $x=P^{-1}y$.
			- So our effective matrix is AP-1.
			- This does not affect the residual, so TOL can be checked and stuff
			- In this the residual is unchanged, we just solve $x_{k}=P^{-1}y$ in the end.
	- ILU:
		- LU decomposition of a sparsse will be nonspares
		- So we force it to be sparse by simply not computing the patterns outside our allowed liitation




compare simultaneous iteration, QR algorithm and arnoldi iteration



For the Oral exam:
- Options to solve
- Does it converge fast? (what does it mean to conv. fast)
- Pen & paper, write down
- If you dont know, say so
- Talk as you want
- Lecture 15&16 important