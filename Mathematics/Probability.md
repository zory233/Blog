# Ch1 Events
## 1.1 Space
Def. (**Sample space** $\Omega$):  the set of all outcomes of an experiment.
Rmk. set of all possible outcomes(elementary events)
Def. (**Event**): a subset of the sample space.

Def. (**Field** $\mathcal{F}$): a collection of subsets of $\Omega$ which satisfies
1. $\emptyset \in \mathcal{F}$
2. If $A \in \mathcal{F}$, then $A^{C} \in \mathcal{F}$
3. If $A, B \in \mathcal{F}$, then $A \cup B \in \mathcal{F}$
Corollary. If $A, B \in \mathcal{F}$, then $A \cap B \in \mathcal{F}$; $\Omega \in \mathcal{F}$; Field is closed under finite unions & intersections.
Rmk. Field is a collection of events that are of interest.

Def. (**$\sigma$-Field** $\mathcal{F}$):  a Field satisfies that 
$$A_{1}, A_{2}, \dots \in \mathcal{F} \implies \bigcup_{i=1}^ {\infty} A_{i} \in \mathcal{F}$$
E.g. smallest $\sigma$-Field=$\{\emptyset , \Omega\}$, largest=$2^{\Omega}$
Rmk. With any experiment, we may associate a pair $(\Omega, \mathcal{F})$.
![[Pasted image 20230207154908.png]]
Def. (**Measurable space**): a pair $(\Omega, \mathcal{F})$.
Def. (**General measure**): given a measurable space, a measure $\mu$ is a set function $\mu: \mathcal{F} \to [0,  \infty]$, s.t. 
1. $\mu(\emptyset)=0$
2. (countable additivity) If $A_{1}, A_{2}, \dots$ is a collection of disjoint members of $\mathcal{F}$, i.e. $A_{i} \cap A_{j} = \emptyset$ for all $i \ne j$, then $\mu(\bigcup_{i=1}^ {\infty} A_{i})=\sum_{i=1}^ {\infty} \mu(A_{i})$.
Def. (**Measure space**): a triple $(\Omega, \mathcal{F}, \mu)$.

Def. (**Probability measure**): a function $\mathbb{P}: \mathcal{F} \to [0,1]$ satisfying
1. $\mathbb{P}(\emptyset)=0, \mathbb{P}(\Omega)=1$.
2. (countable additivity) If $A_{1}, A_{2}, \dots$ is a collection of **disjoint** members of $\mathcal{F}$, i.e. $A_{i} \cap A_{j} = \emptyset$ for all $i \ne j$, then $\mathbb{P}(\bigcup_{i=1}^ {\infty} A_{i})=\sum_{i=1}^ {\infty} \mathbb{P}(A_{i})$.

Rmk. A measure $\mu$ is probability measure if $\mu(\Omega)=1$. Probability measure is a finite measure. Lebesgue measure is a $\sigma$-finite measure.
Def. (**Probability space**): a triple $(\Omega, \mathcal{F}, \mathbb{P})$.

## 1.2 Continuity
Recall: 
1. $f$ is continuous at x if $\forall \{x_{n}\}, x_{n} \to x, n \to  \infty \longrightarrow \lim_{n \to  \infty} f(x_{n}) = f(x)$.
2. $\limsup_{n}x_{n}=\lim_{m \to  \infty} \sup_{n \ge m} x_{n}=\lim_{m \to  \infty} c_{m}$, where c is monotonic.

Def. (**Set limit**): given $A_{1}, A_{2}, \dots \in \mathcal{F}$, 
$$\limsup_{n}x_{n}:=\bigcap_{m=1}^{\infty} \bigcup_{n=m}^{ \infty} A_{n}=\bigcap_{m=1}^{\infty} B_m=\{\omega \in \Omega : \omega \in  A_{n} \text{ for infinitely many n}\}$$
Rmk. called $A_n$ happens **infinitely** often.

$$\liminf_{n}x_{n}:=\bigcup_{m=1}^{  \infty} \bigcap_{n=m}^{ \infty} A_{n}=\bigcup_{m=1}^{\infty} B_m=\{\omega \in \Omega : \omega \in  A_{n} \text{ for all but finitely many n}\}$$
Rmk. called $A_n$ happens **all but finitely** often.
Proof. consider $\omega \in RHS$ or not.
Rmk. $\liminf x_{n} \subset \limsup x_{n}$.
Rmk. to connect real number limit and set limit, consider indicate function $1_{A}(\omega):[\omega \in A]$.

E.g. monotonic set sequence converges(if including inf)

Def. (**Continuity of probability measure**): $\mathbb{P}$ is continuous if $\forall \{A_{n}\}, A_{n} \to A, n \to  \infty \longrightarrow \lim_{n \to  \infty} \mathbb{P}(A_{n}) = \mathbb{P}(\lim_{n \to  \infty} A)$.
Rmk. notice the closeness under union&intersection gives that $A \in \mathcal{F}$.

Thm. (**countable additivity implies continuity**)
#TODO 

case1: monotonic An
(recall countable additivity) If $A_{1}, A_{2}, \dots$ is a collection of **disjoint** members of $\mathcal{F}$, i.e. $A_{i} \cap A_{j} = \emptyset$ for all $i \ne j$, then $\mathbb{P}(\bigcup_{i=1}^ {\infty} A_{i})=\sum_{i=1}^ {\infty} \mathbb{P}(A_{i})$.
construct $B_{n}=A_{n} \setminus A_{n-1}$, then $$\mathbb{P}(\bigcup_{n=1}^ {\infty}A_n)=\mathbb{P}(\bigcup_{n=1}^ {\infty}B_{n})=\sum \mathbb{P}(\bigcup_{n=1}^ {\infty}A_n)$$
Rmk. finite additivity + continuity <=> countable additivity
#TODO 

case2: general An
hint: Bn is monotonic, so twice case1
#TODO 



E.g. $\Omega= \mathbb{R}$, $\mathcal{F}$ is some $\sigma$-field including all intervals. If we know $\mathbb{P}([a,b])$ for all $[a,b] \subset \mathbb{R}$, then $$\lim_{n \to  \infty} \mathbb{P}([a+ \frac{1}{n}, b- \frac{1}{n} ])=\mathbb{P}(\lim_{n \to  \infty}  [a+ \frac{1}{n}, b- \frac{1}{n} ])=\mathbb{P}((a,b))$$, which uniquely extend all open intervals.


## 1.3 Conditional probability, independence
Rmk. "B has occurred" means $\omega \in B$. We may consider B as another sample space.
Def. (**Conditional probability**): if $\mathbb{P}(B)>0$, then $\mathbb{P}(A|B)= \frac{\mathbb{P}(A \cap B)}{\mathbb{P}(B)}$(pronounced as probability of A given B).
Lemma. (**Law of total probability**) Let $B_{1}, B_{2}, \dots, B_{n}$ be a partition of $\Omega$(disjoint $B_i$, $\cup B_i=\Omega$). If $\mathbb{P}(B_{i}) >0$, then $\mathbb{P}(A)=\sum_{i=1}^{n} \mathbb{P}(A|B_{i}) \mathbb{P}(B_{i})$.
Rmk. $\mathbb{P}(\cdot | B)=\mathbb{Q}(\cdot)$ is also a probability measure.

Def. (**Independence**): 
