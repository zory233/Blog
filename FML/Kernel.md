dictionary: normed textbftor space, metric space, complete metric space(Banach space).
Reference:
1. [Moore-Aronszajn Theorem and Mercer theorem](https://stats.stackexchange.com/questions/576815/moore-aronszajn-theorem-and-mercer-theorem-for-the-kernel-trick)
2. [Reproducing Kernel Hilbert Space, Mercer's Theorem, Eigenfunctions, Nyström Method, and Use of Kernels in Machine Learning: Tutorial and Survey](https://arxiv.org/abs/2106.08443)
3. [wikipedia](https://en.wikipedia.org/wiki/Reproducing_kernel_Hilbert_space)
4. Foundations of Machine Learning (second edition)

## Kernels
def. (**Real-valued Hilbert space**) a real textbftor space $\mathcal{H}$ equipped with an inner product, s.t. the induced normed textbftor space($|| \textbf v||=\sqrt{ \left<  \textbf v, \textbf v \right> }$) is a Banach space.

def. (**Kernel**) $k:\mathcal{X} \times \mathcal{X} \to \mathbb{R}$ is a kernal if there exists a Hilbert space $\mathcal{H}$(feature space) and some map $\phi: \mathcal{X} \to \mathcal{H}$ that satisfies $\forall x, x' \in \mathcal{X}, k(x, x')=\left< \phi(x), \phi(x') \right>_{\mathcal{H}}$.

thm. (**Mercer's condition**) let $\mathcal{X}$ be a compact set and $k:\mathcal{X} \times \mathcal{X} \to \mathbb{R}$ is continuous and symmetric, then k admits a uniformly convergent expansion of the form $k(x, x')= \sum_{n=0}^{\infty} a_{n} \phi_{n}(x) \phi_{n}(x')$ with $a_{n}>0$ iff $\forall c \in L_{2}(\mathcal{X}), \int \int_{\mathcal{X} \times \mathcal{X}} c(x)c(x')k(x,x') dxdx' \ge 0$.  
Proof. no yet


def. (**Positive definite symmetric kernel**, PDS) for any $S=\{x_{1}, \dots, x_{m}\} \subset \mathcal{X}$, the matrix $K=[k(x_i,x_j)]_{i,j} \in \mathbb{R}^{m \times m}$ is symmetric positive semidefinite(SPSD).  
comment: 
- SPSD iff all eigenvalues non-negative iff $c^{T} K c \ge 0$ for any textbfter c.
- K is called the kernal matrix/Gram matrix associated to k and sample S.

e.g. (*Polynomial kernel*) a polynomial kernel of degree $d \in \mathbb{N}$ is defined by $\forall \textbf x, \textbf x' \in \mathbb{R}^{N},k(\textbf x, \textbf x') = ( \textbf{x} \cdot  \textbf{x}' + c)^d$.   
(exercise 6.12) The range is in space of dimension $N+d \choose d$ . 

e.g. (*Gaussian kernel*) a Gaussian kernel/radial basis function(RBF) is defined by $\forall \textbf x, \textbf x' \in \mathbb{R}^{N},k(\textbf x, \textbf x') = exp(-  \frac{||\textbf{x}'- \textbf{x}||^{2}}{ 2\sigma^{2}})$. The range is in space of infinite dimension.  
(section 6.2.3) Gaussian kernel can be derived by normalization from the kernel $k':( \textbf{x} ,  \textbf{x}') \mapsto exp( \frac{\textbf{x}\cdot\textbf{x}'}{\sigma^{2}})$, and can be further rewrote as $k'( \textbf{x} ,  \textbf{x}')=\sum_{n=0}^{+\infty} \frac{(\textbf{x} \cdot  \textbf{x}')^{n}}{\sigma^{2n}n!}$, a positive linear combinations of polynomial kernels of all degrees.

e.g. (*Sigmoid kernel*) for any real constant $a,b \ge 0$, a sigmoid kernel is defined by $\forall \textbf x, \textbf x' \in \mathbb{R}^{N},k(\textbf x, \textbf x') = \tanh( a  (\textbf{x} \cdot  \textbf{x}') + b)$.   
(exercise 6.18) if a<0 or b<0

## Reproducing kernel Hilbert space
lemma (**Cauchy-Schwarz inequality for PDS kernels**) let k be a PDS kernel. Then $\forall x,x' \in \mathcal{X}, k(x,x')^{2}  \le k(x,x) k(x',x')$.  
Proof. when k is PDS, then K:=the Gram matrix associated to k and sample x,x' is SPSD. Then $\det(K) \ge 0$.

def. (**Reproducing kernel Hilbert space**, RKHS) let $\mathcal{X}$ be a set and $\mathcal{H}$ a Hilbert space of real-valued functions on $\mathcal{X}$, equipped with pointwise addition and pointwise scalar multiplication. The evaluation functional over $\mathcal{H}$ is $L_{x}: f \mapsto f(x), f: \mathcal{H} \to \mathbb{R}$. Then $\mathcal{H}$ is a RKHS if, $\forall x \in \mathcal{X}, L_{x}$ is continuous at every $f \in \mathcal{H}$ or equivalently(1), $L_{x}$ is a bounded operator on H.   
Equivalently, given a kernel k, there exists a Hilbert space $\mathcal{H}$ and a mapping $\phi$ by definition. Further more, $\mathcal{H}$ has the reproducing property:   
Equivalence(1): no yet  
Equivalence(2):  


Venn: 
![from (2)](https://ngilshie.github.io/assets/venn.jpg)




# ChatGPT
A reproducing kernel Hilbert space (RKHS) is a Hilbert space of functions that is defined by a positive definite kernel. One of the key properties of an RKHS is that the evaluation functional, $L_x$, defined by $L_x(f) = f(x)$, is a continuous linear functional on the space. The equivalence you mentioned states that the continuity of the evaluation functional at every point in the input space, $\mathcal{X}$, is equivalent to the evaluation functional being a bounded operator on the Hilbert space, $\mathcal{H}$.

The equivalence is true because a linear functional $L$ on a Hilbert space is continuous if and only if it is bounded. To see this, consider the Cauchy-Schwarz inequality:

$$ |L(f)|^2 \leq |L|^2 |f|^2 $$

This tells us that if $L$ is a continuous linear functional, then $|L(f)|$ is bounded by the product of the norm of $L$ and the norm of $f$. In other words, if $L$ is continuous, then $|L|$ is a finite non-negative number, which means $L$ is a bounded operator.

Conversely, if $L$ is a bounded operator, then the Cauchy-Schwarz inequality tells us that $|L(f)|$ is also bounded by a constant times $|f|$, so $L$ is continuous.

Thus, we see that continuity of the evaluation functional at every point in the input space is equivalent to the evaluation functional being a bounded operator on the Hilbert space.

It is also important to note that the key condition for $L_x$ being a bounded operator, is that the kernel is a positive definite function, as it gurantees the inner product of the space is well defined and the Cauchy-Schwarz inequality holds.