# Eigenvalue

## Eigenvalue, eigenvector and movement
For a matrix $A_{n \times n}$, consider all $(\vec u,\lambda)$ pair such that: $A \vec u=\lambda \vec u$
We call them **eigenvalues** and **eigenvectors** of matrix A.
There're totally n pairs of $(\vec u_i, \lambda_i)$ for diagonalizable linear transformation, and the eigenvectors form a basis(some $\lambda_i$ might be the same).

If we regard matrix/transformation W as a space movement in Euclidean space, we need to apply it on certain vector to examine its feature. What if we try to apply it multiple times?
$$
\begin{gather}
\vec v=\sum_i \alpha_i \vec  u_i
\\\\
W^k \vec v
=\sum_i \alpha_i  W^k \vec  u_i
=\sum_i \alpha_i  \lambda_i^k \vec  u_i

\end{gather}
$$
We find out that the largest eigenvalue corresponding eigenvector will eventually dominate as k getting larger and larger. That's why we would like to conclude:
- first principle eigenvalue(largest) indicates the movement speed
- first principle eigenvector indicates the movement direction

e.g. 
When A is the adjacency matrix, $(A \vec v)_i = \frac 1 {deg_i }\sum_{j \in N(i)} v_j$
When $L=I-D^{-1}A$ , the Laplacian matrix, $(L \vec v)_i = \frac 1 {deg_i} \sum_{j \in N(i)} (v_i - v_j)$

## How to find them?
When the transformation A is normal operator, which means orthogonal diagonalizable, then:
$$
\begin{gather}
A=P \Lambda P^{-1}
\end{gather}
$$
where $\Lambda$ stretchs (eigenvalues), $P$ rotates (orthonormal eigenvectors).
Further more, when A is symmetric real matrix(e.g. adjacency and Laplacian matrix), then it is hermitian/self-adjoint, which means all eigenvalues are real.

## THM
Symmetric real matrix M
$M := \sum_{i}\lambda_{i} v_{i} v_{i}^T$, #TODO 
(upd) dim V=K
We may use the same eigenvectors in $M^k$, such that $M^k := \sum_{i}\lambda_{i}^k v_{i} v_{i}^T$
claim: $M^{-1} := \sum_{i} \frac{1}{\lambda_{i}} v_{i} v_{i}^{T} , M^{-1} M=I$
proof: substitute

thm2: $tr(M)=\sum_{i} \lambda_{i}$
https://courses.cs.washington.edu/courses/cse521/16sp/521-lecture-8.pdf

## Variational Characterization of Eigenvalues
$$
\begin{gather}
\text{symmetric real}\ M_{n \times n},\text{ eigenvalue}\ \lambda_1 \le \lambda_2 ... \le\lambda_n
\\
\text{Rayleigh quotient }R_M(\boldsymbol x)=\frac{\boldsymbol x^T M \boldsymbol x}{\boldsymbol x^T \boldsymbol x}
\\
\lambda_k = \min_{\forall V,\dim V=k} \max_{\boldsymbol x \in V-\{\boldsymbol 0\}} R_M(\boldsymbol x)
\end{gather}
$$
proof:
https://blog.csdn.net/a358463121/article/details/100166818


证明$V$里面一定存在向量使得Rayleigh quotient时，只需要取$\lambda_1,\lambda_2, ...,\lambda k$对应的$v1, v_2, ..., v_k$组成的空间$V$即可。
https://zhuanlan.zhihu.com/p/80817719


# Hilbert space
conjucture symmetric

## Reference
Basic knowledge in Spectral Theory.