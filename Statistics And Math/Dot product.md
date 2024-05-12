The dot product (also known as the inner product or scalar product) of two vectors is a mathematical operation that yields a scalar value. It is defined as the sum of the products of the corresponding components of the vectors.

For two vectors, $\mathbf{u} = [u_1, u_2, \ldots, u_n]$ and $\mathbf{v} = [v_1, v_2, \ldots, v_n]$, the dot product is computed as:
$$

\mathbf{u} \cdot \mathbf{v} = u_1v_1 + u_2v_2 + \ldots + u_nv_n

$$
Alternatively, the dot product can be expressed as:

  

$$

\mathbf{u} \cdot \mathbf{v} = \sum_{i=1}^{n} u_iv_i

$$
The dot product is commutative, meaning that $\mathbf{u} \cdot \mathbf{v} = \mathbf{v} \cdot \mathbf{u}$. It is commonly used in various mathematical and computational applications, such as determining the angle between vectors, calculating vector projections, and solving linear systems.

## Relation to matrix notation
While the definition of the dot product operator $\cdot$ makes it clear that we always sum up the products of both vectors and hence order doesn't matter. The definition of _row_ vs. _column_ vectors is also not necessary at this point: we just think of the two operand vectors as lists of coordinates with equal numbers of coordinates. The number of coordinates is practically the same es the length of a list or array in programming (as long as every coordinate just contains a number).

Thinking of row vs. column vectors starts to get useful once we move to 'matrix land'. Then, a row vector would be a matrix of shape $(1 \times n)$ while a column vector would be a matrix of shape $(n \times 1)$.

We could denote the dot product as the product of a row vector $\mathbf{u}$ and a column vector $\mathbf{v}$ and just write 
$$
\mathbf{u}\mathbf{v}
$$
Remember: for matrix multiplication, the number of *rows* in the left matrix needs to match that of the *columns* of the right. The result has the same number of rows as the left matrix and the same number of columns as the right one. Hence multiplying a row vector with a column vector returns a matrix of shape $(1 \times 1)$, in other words: a scalar!

But beware: in matrix land
$$
\mathbf{u}\mathbf{v}\neq \mathbf{v}\mathbf{u}
$$
$\mathbf{v}\mathbf{u}$ would then be a $(n \times n)$ matrix. This is called the tensor product, or also _outer_ product. It is often also denoted with the symbol $\otimes$.

See also [this](https://math.stackexchange.com/a/1198912/1102645) discussion of row vs. column vectors on StackExchange.
