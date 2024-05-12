Eigenvalues (and hence Eigenvectors) can only exist on square matrices.

## Definition
The Eigenvector of a square matrix $\mathbf{A}$ is any vector $\mathbf{x\neq 0}$ that, if multiplied with that matrix, results in a multiple of itself. The 'multiplier' $\lambda$ of this vector (a real number) is then called its Eigenvalue. Expressed in pure math terms:
$$
\mathbf{A}\mathbf{x}=\lambda \mathbf{x}, x\neq 0,\lambda \in \mathbb{R}
$$

Side-note: every square matrix has Eigenvalues, but they may not be in the real domain (otherwise no Eigenvectors or Eigenvalues possible; side note: every square matrix has eigenvalues, though they [can sometimes be complex](https://math.stackexchange.com/a/654470/1102645), not real)

## Finding Eigenvectors and -values

To figure out how to compute the eigenvalues of a matrix $\mathbf{A}$, we need to rewrite what we already have just a bit, making use of the fact that multiplying any vector with an identity matrix $\mathbf{I}$ of suitable shape (i.e. same number of columns and rows as the number of components in the vector) is kind of like multiplying a simple equation by 1 (it is the neutral element of matrix multiplication), rearranging stuff a bit:
$$
\begin{aligned}
\mathbf{A} \mathbf{x} = \lambda \mathbf{x} &= \lambda \mathbf{I} \mathbf{x} & \text{multiply with } \mathbf{I}\\
\mathbf{A} \mathbf{x} - \lambda \mathbf{I} \mathbf{x} &= 0 & \text{subtract }\lambda \mathbf{I}\mathbf{x} \\
(\mathbf{A} - \lambda \mathbf{I}) \mathbf{x} &= 0 & \text{factor out }\mathbf{x}
\end{aligned}
$$
As we already defined that $\mathbf{x}\neq0$, we  

can use the _characteristic equation_ or _characteristic polynomial_. It is given as the _determinant_ of

$$
\text{det}(\mathbf{A} - \lambda \mathbf{I}) = 0
$$

where \(\lambda\) represents the eigenvalue, \(\mathbf{I}\) is the identity matrix, and \(\text{det}\) denotes the determinant.

Solving this equation will give you the eigenvalues of \(\mathbf{A}\).