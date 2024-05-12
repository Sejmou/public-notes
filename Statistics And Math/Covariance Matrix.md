source for most of the information here is [this](https://youtu.be/152tSYtiQbw?si=SogGn4ZPgWlFSuHj) awesome video and its [follow-up](https://youtu.be/F-aku75OpoM?si=Ix8CW8WeryXsn6NZ) as well as the [Wikipedia article](https://en.wikipedia.org/wiki/Sample_mean_and_covariance) for sample covariance. You will need to understand [Covariance vs. Correlation](Covariance%20vs.%20Correlation.md).

**Note:** The videos apparently define the matrix for population covariance (not exactly sure why). The only real difference with sample covariance is that we divide by the sample size $n-1$ instead of population size $N$.
## How to interpret it
As we learned earlier already, we can formulate any set of $n$ observations of $p$ variables each as matrix $\mathbf{X}'$ of shape $(n \times p)$ containing $n$ observations of $p$ variables (as defined [here](1.%20Linear%20Model%20in%20Matrix%20Form.md#Inputs) - this 'input matrix' idea translates to arbitrary models, not just linear regression models). The corresponding covariance matrix $Cov(\mathbf{X}')$ is a symmetric matrix with shape ($p \times p$). The number in the $i^{th}$ row and $j^{th}$ column represents the covariance between variables $x_i$ and $x_{j}$, i.e. $\sigma_{i,j}$. Its diagonal elements are the variances of the $p$ variables (the $i^{th}$ diagonal element being $\sigma_{i,i}=\sigma_{i}^2$):
$$Cov(\mathbf{X'})=\left[ \begin{array}{cccc} \sigma_{1}^2 & \sigma_{1,2} & \ldots & \sigma_{1,p}  \\ \sigma_{2,1} & \sigma_{2}^2 & \ldots & \sigma_{2,p}  \\
 \vdots & \vdots & \ddots & \vdots \\
 \sigma_{p,1} & \sigma_{p,2} & \ldots & \sigma_{p}^2 \ \end{array} \right] $$
As covariance is symmetric (i.e. $\sigma_{i,j}=\sigma_{j,i}$), the covariance [matrix is also symmetric](Symmetric%20Matrix.md).
## How to generalize to $p$ variables
We already learned [earlier](Links%20between%20Variance,%20Covariance%20and%20Standard%20Deviation.md#Covariance) how to compute the sample covariance for just two vectors. For an arbitrary matrix $\mathbf{X}'$ of $n$ observations (rows) of $p$ variables (columns), we just need to adapt the formulation slightly.  Note: I am using the $'$ to emphasize that we don't mean the [design matrix](1.%20Linear%20Model%20in%20Matrix%20Form.md#The%20'Design%20Matrix') which has an extra column of 1s up front.

Let  $x_{ij}$ be the $i^{th}$ independently drawn observation on the $j^{th}$ random variable (i.e., an element in the matrix $\mathbf{X}'$.

Furthermore, we define the sample mean vector $\overline{\mathbf{x}}$ as a column vector whose $j^{th}$ element $\bar{x}_j$ is the average value of the $N$ observations of the $j^{\text {th }}$ variable (i.e. its components are the means of the columns of $\mathbf{X}'$):
$$
\bar{x}_j=\frac{1}{N} \sum_{i=1}^N x_{i j}, \quad j=1, \ldots, K .
$$
Thus, the sample mean vector contains the average of the observations for each variable, and is written
$$
\overline{\mathbf{x}}=\frac{1}{N} \sum_{i=1}^N \mathbf{x}_i=\left[\begin{array}{c}
\bar{x}_1 \\
\vdots \\
\bar{x}_j \\
\vdots \\
\bar{x}_K
\end{array}\right]
$$

Then, every entry $s_{jk}$ of $Cov(\mathbf{X}')$ stands for the covariance estimate between the $j^{th}$  and the $k^{th}$ variable of the population we sample from and is computed like this:
$$
s_{j k}=\frac{1}{N-1} \sum_{i=1}^N\left(x_{i j}-\bar{x}_j\right)\left(x_{i k}-\bar{x}_k\right),
$$
### Rewriting in closed form
Ideally, we would want to have a closed form expression for the covariance matrix as well, as it makes it easier to express/rewrite/rearrange operations and computations using it. This is it:
$$
Cov(\mathbf{X}')=\frac{1}{N-1} \sum_{i=1}^N\left(\mathbf{x}_{i \cdot}-\overline{\mathbf{x}}\right)\left(\mathbf{x}_{i \cdot}-\overline{\mathbf{x}}\right)^{\mathrm{T}},
$$
Here, in the summation, every $\mathbf{x}_{i \cdot}$ is a row vector of shape $(p \times 1)$ that corresponds to one observation in our dataset. As it is multiplied with its transpose, a $(1 \times p)$, the result of every expression under the sum is a $(p \times p)$ (the sample mean $\bar{\mathbf{x}}$ is also just a scalar and doesn't change the shape of the vectors). Those $n$ sums are then simply summed up to produce a matrix. Hopefully it is obvious now that the end result is equivalent to the formulation above.