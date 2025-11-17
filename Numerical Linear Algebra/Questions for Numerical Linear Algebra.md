1. When is the QR unique?
2. how do we solve Ax=b with QR.
3. How can we calculate the QR?
4. Whats the difference between householder vs gram-schmidt?
5. Explain householder reflection
6. How can you find the null space?
7. What do we do if were solving Ax=b and b is not in the range(A)
8. How can we solve the normal equations?
9. Explain absolute and relative condition number  


Answers:
1. A is full rank
2. Rx=Q.T b. is easy to solve 
	1. Compute A=QR
	2. Compute y'=Q.T b
	3. Solve Rx=y' for x 
	4. **Though Gauss elimination is used in practice due to half as many operations**
3. G-S BUUUT it is not a good idea sooooo....
4. Householder slowly creates R by QT=inv(Q), G-S slowly creates Q by what becomes inv(R). Householder is way more stable, keeping orthogonality to machine precision.
5. Mention, submatrix H_22, reflection across plane orthogonal to v that is the difference between of vector and where we want to go.
6. SVD, the columns of V corresponding to singular values with 0 is the null space. OR faster is using QR and partitioning the matrix A to bottom zero row submatrices, some algebra gives it.
7. then r=b-Ax => generalized solutions x* => project b (non orthogonal base) onto A -> Pb=Ax*
8. 3 ways:
	1. Just calculate the pseudoinverse bleh
	2. (Cholesky decomposition)
	3. SVD can also be used cuz it creates diagonal system but it is slow
	4. QR-factorization and calculate upepr triangular system Rx = Q* b
9. A way to quantify the effect of small perturbations in data on the solution. Absolute is like a induced matrix norms, it tells us the limit of that maximal perturbation of f. Relative is the relative change so perturbation of f "normed" by f, and x.
10.  