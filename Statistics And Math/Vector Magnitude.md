For a two-dimensional vector $\mathbf{v} = [v_1, v_2]$, the length is calculated using the Euclidean norm or the Pythagorean theorem:
$$

\|\mathbf{v}\| = \sqrt{v_1^2 + v_2^2}

$$
For a three-dimensional vector $\mathbf{v} = [v_1, v_2, v_3]$, the length is computed as:
$$

\|\mathbf{v}\| = \sqrt{v_1^2 + v_2^2 + v_3^2}

$$
More generally, for an n-dimensional vector $\mathbf{v} = [v_1, v_2, \ldots, v_n]$, the length is given by:
$$

\|\mathbf{v}\| = \sqrt{v_1^2 + v_2^2 + \ldots + v_n^2}=\sqrt{ \sum_{i=1}^{n}v_{i}^2
 }
$$
The length of a vector represents its magnitude or size and is always a non-negative value. It provides information about the vector's overall scale or extent in the given space.

## Relationship to dot product
The dot product of a vector $\mathbf{v}$ with itself is equal to the square of the norm of the vector, i.e.
$$
\mathbf{v}\cdot\mathbf{v}=\|\mathbf{v}\|^2
$$Let's try to understand that.

Recall that the square root of any scalar $x$ can be written as $x^{\frac{1}{2}}$ and $x^ax^b=x^{a+b}$.  
Furthermore, the dot product of a vector with itself is simply the sum of squares of its components:
$$
\mathbf{v} \cdot \mathbf{v} = \sum_{i=1}^{n}v_{i}v_{i}=\sum_{i=1}^{n}v_{i}^2
$$
Let's briefly substitute $\sum_{i=1}^{n}v_{i}^2$ with $u$. Then we can write
$$
u = u^1 = u^{\frac{1}{2}} u^{\frac{1}{2}} = \sqrt{ u } \sqrt{ u }
$$
Substituting back, we get:
$$
\sqrt{ u } \sqrt{ u }= \sqrt{ \sum_{i=1}^{n}v_{i}^2 } \sqrt{ \sum_{i=1}^{n}v_{i}^2 }=\|\mathbf{v}\| \|\mathbf{v}\|=\|\mathbf{v}\|^2
$$