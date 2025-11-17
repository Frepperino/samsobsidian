
what methods to create orthonormal basis

Easy talking points:
- gerschgorin and SDD
- potentially cholesky
- selecting algorithms
- power iteration
- gmres

game plan:
1. Start with SVD, mention casually that we can deduce some cool stuff, e.g., mention 1. Then, really cool is of course low rank approximations.
	1. Add on image analysis stuff
2. Mention SVD for solving lienar systems and casually say that of course this isnt the most usually method in a way.
	1. "do you mind if a draw a bit of a flowchart?". Talk about the different methods and when to use them.
3. Talk about arnoldi, and then gmres. casually mention that we can gmres approximation problem show some onvergence stuff
	1. say that it is a beautiful relationship with the minmax theorem and how that means well converge within as many distinct eigenvalues  


* Concept:
	* Unit 1 - Vector and Matrix norms
		* Vector and matrix norms
	* Unit 2/3 - SVD and orthogonal matrices
		* SVD and properties
		* Low rank matrices
		* Projector
		* Image compressing + data analysis
	* Unit 4 - Orthogonal matrices, QR factorization
		* QR full and reduced
		* Gram schmidt
		* Householder reflection + triangularization
		* Null space of matrix with QR
	* Unit 6 - Least Square problems
		* Vandermonde system
		* pseudoinverse
		* solution with QR
	* Unit 7 - Condition and Stability
		* Perturbations and conidtions
		* Condition numbers
	* Unit 8 - Direct solution methods for linear systems
		* LU algorithm + pivoting
		* Cholesky factorization + spd
	* Unit 9 - Eigenvectors and values
		* Similarity transforms
		* Eigenvalure revealing factorizations
		* Rayleigh quotient
		* SDD
		* Gerschgorins Theorem 1 & 2 and disks
		* Search engines
	* Unit 10 - Iterative for eigenvalues and vectors
		* Power iteration + inverse power iteration (w shifts)
		* QR Algorithm + practical adjustments
	* Unit 11 - Iterative for big stuff
		* Matrix valued polynomials
		* Cayleigh Hamilton theorem
		* Arnoldi iteration, and for eigenvalue computation + why it works
		* GMRES + modifications and theorems
		* that preconditioning stuff