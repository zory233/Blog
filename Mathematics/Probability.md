# Ch1 Events
## 1.1 Space
Def. (**Sample space** $\Omega$) The set of all outcomes of an experiment.
Rmk. Set of all possible outcomes(elementary events)
Def. (**Event**) A subset of the sample space.

Def. (**Field** $\mathcal{F}$) A collection of subsets of $\Omega$ which satisfies
1. $\emptyset \in \mathcal{F}$
2. If $A \in \mathcal{F}$, then $\overline A \in \mathcal{F}$
3. If $A, B \in \mathcal{F}$, then $A \cup B \in \mathcal{F}$
Corollary. If $A, B \in \mathcal{F}$, then $A \cap B \in \mathcal{F}$; $\Omega \in \mathcal{F}$; **Field is closed under finite unions & intersections.**
Rmk. Field is a collection of events that are of interest.

Def. (**$\sigma$-Field** $\mathcal{F}$) A Field satisfies that (closed under countable unions & intersections)
$$A_{1}, A_{2}, \dots \in \mathcal{F} \implies \bigcup_{i=1}^ {\infty} A_{i} \in \mathcal{F}$$
E.g. Smallest $\sigma$-Field=$\{\emptyset , \Omega\}$, largest=$2^{\Omega}$
Rmk. With any experiment, we may associate a pair $(\Omega, \mathcal{F})$.
![[Pasted image 20230207154908.png]]

## 1.2 Assignment
Def. (**Measurable space**) A pair $(\Omega, \mathcal{F})$.
Def. (**General measure**) Given a measurable space $(\Omega, \mathcal{F})$, a measure $\mu$ is a set function $\mu: \mathcal{F} \to [0,  \infty]$, s.t. 
1. $\mu(\emptyset)=0$
2. (countable additivity) If $A_{1}, A_{2}, \dots$ is a collection of disjoint members of $\mathcal{F}$, i.e. $A_{i} \cap A_{j} = \emptyset$ for all $i \ne j$, then $\mu(\bigcup_{i=1}^ {\infty} A_{i})=\sum_{i=1}^ {\infty} \mu(A_{i})$.
Def. (**Measure space**) A triple $(\Omega, \mathcal{F}, \mu)$.

Def. (**Probability measure**) A function $\text{I\kern-0.15em P}: \mathcal{F} \to [0,1]$ satisfying
1. $\text{I\kern-0.15em P}(\emptyset)=0, \text{I\kern-0.15em P}(\Omega)=1$.
2. (countable additivity) If $A_{1}, A_{2}, \dots$ is a collection of **disjoint** members of $\mathcal{F}$, i.e. $A_{i} \cap A_{j} = \emptyset$ for all $i \ne j$, then $\text{I\kern-0.15em P}(\bigcup_{i=1}^ {\infty} A_{i})=\sum_{i=1}^ {\infty} \text{I\kern-0.15em P}(A_{i})$.

Ext. A measure $\mu$ is probability measure if $\mu(\Omega)=1$. Probability measure is a finite measure. Lebesgue measure is a $\sigma$-finite measure.
Def. (**Probability space**) A triple $(\Omega, \mathcal{F}, \text{I\kern-0.15em P})$.
Rmk. 
1. $\text{I\kern-0.15em P}(\overline A)=1-\text{I\kern-0.15em P}(A)$
2. If $B \supset A$, then $\text{I\kern-0.15em P}(B)=\text{I\kern-0.15em P}(A)+\text{I\kern-0.15em P}(B \setminus A) \ge \text{I\kern-0.15em P}(A)$, notice that $B \setminus A \in \mathcal{F}$
3. $\text{I\kern-0.15em P}(A \cup B)=\text{I\kern-0.15em P}(A)+\text{I\kern-0.15em P}(B)-\text{I\kern-0.15em P}(A \cap B)$
4. Inclusion-exclusion principle
5. $\text{I\kern-0.15em P}$ is a continuous set function

## 1.3 Continuity
Recall: 
1. $f$ is continuous at x if $\forall \{x_{n}\}, x_{n} \to x, n \to  \infty \Longrightarrow \lim_{n \to  \infty} f(x_{n})= f(\lim_{n\to\infty} x_{n} ) = f(x)$.
2. $\limsup_{n}x_{n}=\lim_{m \to  \infty} \sup_{n \ge m} x_{n}=\lim_{m \to  \infty} c_{m}$, where $c_m$ is monotonic, so that it must converge if we include $\pm \infty$.

Def. (**Set limit**) Given $A_{1}, A_{2}, \dots \in \mathcal{F}$, 
$$\limsup_{n \to  \infty}A_{n}:=\bigcap_{m=1}^{\infty} \bigcup_{n=m}^{ \infty} A_{n}=\bigcap_{m=1}^{\infty} B_m=\{\omega \in \Omega : \omega \in  A_{n} \text{ for infinitely many n}\}$$
Proof. Consider $\omega \in RHS$ or not. If yes, $\omega \in B_{m}, \forall m$; if not, disappear eventually.
$$\liminf_{n\to  \infty}A_{n}:=\bigcup_{m=1}^{  \infty} \bigcap_{n=m}^{ \infty} A_{n}=\bigcup_{m=1}^{\infty} C_m=\{\omega \in \Omega : \omega \in  A_{n} \text{ for all but finitely many n}\}$$
Proof. Consider $\omega \in RHS$ or not. If yes, appear eventually; otherwise fail.
Rmk. $\liminf A_{n} \subset \limsup A_{n}$, if equal, we say $A_{n}$ converges.
E.g. Monotonic set sequence converges (if including inf).

Def. (**Continuity of general measure**) $\mu$ is continuous if $\forall \{A_{n}\}, A_{n} \to A, n \to  \infty \longrightarrow \lim_{n \to  \infty} \mu(A_{n}) = \mu(\lim_{n \to  \infty} A_n)=\mu(A)$.
Rmk. Notice the closeness under union&intersection gives that $A:=\limsup_{n}A_{n} \in \mathcal{F}$.

Thm. (**Countable additivity implies continuity**)
Proof. For all convergent sequence $\{A_{n}\}$, which means
Case1: monotonic An ($A_{n-1} \subset A_{n}$)
Recall countable additivity (\*), construct $D_{n}=A_{n} \setminus A_{n-1}$, then 

$$
\begin{aligned}
\mu(A)
&=\mu(\lim_{n \to  \infty} A_n)
:=\mu(\bigcup_{n=1}^ {\infty} \bigcap_{m=n}^ {\infty} A_{m}) \\
&=\mu(\bigcup_{n=1}^ {\infty} A_{n})
=\mu(\bigcup_{n=1}^ {\infty}D_{n})
\overset{(*)}{=} \sum_{n=1}^ {\infty} \mu(D_{n})\\
&=\lim_{n \to  \infty} \sum_{i=1}^{n} \mu(D_i)
=\lim_{n \to  \infty} \mu(\bigcup_{i=1}^{n} D_i)
=\lim_{n \to  \infty} \mu(A_n)
\end{aligned}$$

Case2: general An
Recall $B_{n}=\bigcup_{m=n}^{ \infty} A_{m}, C_{n}=\bigcap_{m=n}^{ \infty} A_m$, 
clearly $C_{n} \subset A_{n}\subset B_{n}$.
From case1, we know that 

$$\begin{align*}
\limsup_{n \to  \infty} A_{n}
=\lim_{n \to  \infty}\mu( B_{n})
=\mu(\lim_{n \to  \infty} B_{n})
=&\mu(B) \\
=&\mu(A) \\
=&\mu(C)
=\mu(\lim_{n \to  \infty} C_{n})
=\lim_{n \to  \infty}\mu( C_{n})
\le \liminf_{n \to  \infty} A_{n}
\end{align*}
$$

However, $\limsup_{n \to  \infty} A_{n} \ge \liminf_{n \to  \infty} A_{n}$, 
therefore $\lim_{n \to  \infty} A_{n} = \limsup_{n \to  \infty} A_{n} = \liminf_{n \to  \infty} A_{n}=\mu(A)$.

Conclusion: $\mu$ is a continuous set function.

Prop. (**Finite additivity + continuity <=> countable additivity**)
Proof. (=>) 
Recall continuity: $\forall \{A_{n}\}, A_{n} \to A, n \to  \infty \longrightarrow \lim_{n \to  \infty} \mu(A_{n}) = \mu(\lim_{n \to  \infty} A_n)=\mu(A)$
and (countable additivity) If $A_{1}, A_{2}, \dots$ is a collection of disjoint members of $\mathcal{F}$, then 

$$
\mu(\bigcup_{i=1}^ {\infty} A_{i})
=\mu( \lim_{n \to  \infty} \bigcup_{i=1}^{n}A_{i}  )
= \lim_{n \to  \infty} \mu( \bigcup_{i=1}^{n}A_{i}  )
= \lim_{n \to  \infty} \sum_{i=1}^ {n} \mu(A_{i}  )
=\sum_{i=1}^ {\infty} \mu(A_{i})
$$

E.g. $\Omega= \mathbb{R}$, $\mathcal{F}$ is some $\sigma$-field including all intervals. If we know $\text{I\kern-0.15em P}([a,b])$ for all $[a,b] \subset \mathbb{R}$, then 
$$\lim_{n \to  \infty} \text{I\kern-0.15em P}([a+ \frac{1}{n}, b- \frac{1}{n} ])=\text{I\kern-0.15em P}(\lim_{n \to  \infty}  [a+ \frac{1}{n}, b- \frac{1}{n} ])=\text{I\kern-0.15em P}((a,b))$$, which uniquely extend all open intervals.

## 1.3 Conditional probability, independence
Rmk. "B has occurred" means $\omega \in B$. We may consider B as another sample space.

Def. (**Conditional probability**) If $\text{I\kern-0.15em P}(B)>0$, then $\text{I\kern-0.15em P}(A|B)= \frac{\text{I\kern-0.15em P}(A \cap B)}{\text{I\kern-0.15em P}(B)}$(pronounced as probability of A given B).

Lemma. (**Law of total probability**) Let $B_{1}, B_{2}, \dots, B_{n}$ be a partition of $\Omega$(disjoint $B_i$, $\cup B_i=\Omega$). If $\text{I\kern-0.15em P}(B_{i}) >0$, then $\text{I\kern-0.15em P}(A)=\sum_{i=1}^{n} \text{I\kern-0.15em P}(A|B_{i}) \text{I\kern-0.15em P}(B_{i})$.

Rmk. $\text{I\kern-0.15em P}(\cdot | B)=\mathbb{Q}(\cdot)$ is also a probability measure.

Cor. Bayes' Theorm

Def. (**Independence of events**) Let $A, B \in \mathcal{F}$, that $\text{I\kern-0.15em P}(A \cap B)=\text{I\kern-0.15em P}(A)\text{I\kern-0.15em P}(B)$, denoted as $A  \perp \!\!\! \perp B$.

Def. (**Mutually independence**) Let $\{A_{i}\}, A_{i} \in \mathcal{F}$, that $\text{I\kern-0.15em P}(\bigcap_{i \in J} A_{i}) = \prod_{i \in J} \text{I\kern-0.15em P}(A_{i}), \forall J \subset I$.

Def. (**Pairwise independence**) Let $\{A_{i}\}, A_{i} \in \mathcal{F}$, that $\text{I\kern-0.15em P}(\bigcap_{i \in J} A_{i}) = \prod_{i \in J} \text{I\kern-0.15em P}(A_{i}), \forall J \subset I, |J|=2$.

Cor. If $A  \perp \!\!\! \perp B$, then $A  \perp \!\!\! \perp \overline B, \overline  A  \perp \!\!\! \perp B, \overline A  \perp \!\!\! \perp \overline B$.

Cor. If A, B, and C are mutually independent, then A is independent of whatever events formed from B and C.

Def. (**Generated $\sigma$-field**) $\sigma(A)$ is the smallest $\sigma$-field generated by A, a collection of subset, by keeping taking countable union, intersection, or complement.

Def. (**Product space**) Given $(\Omega_{1}, \mathcal{F}_{1},  \text{I\kern-0.15em P}_1)$ and $(\Omega_{2}, \mathcal{F}_{2},  \text{I\kern-0.15em P}_2)$, then their product space is $(\Omega, \mathcal{F},  \text{I\kern-0.15em P})$, where $\Omega=\Omega_{1} \times \Omega_{2}, \mathcal{F}= \sigma(\mathcal{F_{1}} \times \mathcal{F_{2}}),  \text{I\kern-0.15em P}$ is defined on $\Omega$ by $\text{I\kern-0.15em P}(A_{1}\times A_{2})= \text{I\kern-0.15em P}(A_{1})  \text{I\kern-0.15em P}(A_{2})$ and then continuity.

Def. (**Independent trials**) If a combined experiment is modeled by the product space, the two sub-experiments are independent.

# Ch2 Random variable
## 2.1 "Preimage" viewpoint
Rmk. To answer the question that $\text{I\kern-0.15em P}(X \in B)=\text{I\kern-0.15em P}(\{\omega:X(\omega) \in B\})$, random variable acts as a "translation", where $\{\omega:X(\omega) \in B\}$ is the preimage $X^{-1}(B) \in \mathcal{F}$.

Def. (**Random variable**) Given $(\Omega, \mathcal{F},  \text{I\kern-0.15em P})$, consider a function $X: \Omega \to \mathbb{R}$, s.t. $X^{-1}(B) \in \mathcal{F}, \forall \text{ intervals } B \subset \mathbb{R}$, called "X is $\mathcal{F}$-measurable"(\*).

Observ. 
1. Preimage can be interchanged with any set operation, e.g. $X^{-1}(B_{1} \cap B_{2})=X^{-1}(B_{1}) \cap X^{-1}(B_{2})$.
2. $\mathcal{F}$ is a $\sigma$-field: closed under taking countable intersections...

Rmk. Equivalently, holding on the following B will be sufficient instead of the condition (\*):
1. All open intervals
2. All closed intervals
3. All (a,b] intervals
4. All $(- \infty, x]$ intervals (simplest)

Prop. From Prop8.2 in Frederick Fong's book, if $\mu$ is $\mathcal{F}$-measurable, and $\varphi$ is continuous, then $\varphi(\mu)$ is also $\mathcal{F}$-measurable.

## 2.2 Borel Measure space
Rmk. Eventually, by taking countable set operations, we get a **Borel set**. The collection of them are a $\sigma$-field generated by all open intervals, called **Borel $\sigma$-field**, e.g. $(a,b) \in \mathcal{B}(\mathbb{R}), \mathbb{Q}\in \mathcal{B}(\mathbb{R}), \mathbb{R} \setminus \mathbb{Q} \in \mathcal{B}(\mathbb{R})$.

Rmk. Prefer to define by "open set" instead of "open interval", because the latter only works in $\mathbb{R}$.

Rmk. (level 2 understanding) $X: (\Omega, \mathcal{F}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ is a measurable map, s.t. $X^{-1}(B) \in \mathcal{F}, \forall B \in \mathcal{B}(\mathbb{R})$.

## 2.3 Borel Probability space
Motiv. (level 3 understanding) Is there a probability measure Q, such that Q(B) can answer the question of $\text{I\kern-0.15em P}(X \in B)$? That is consider $X: (\Omega, \mathcal{F}, \text{I\kern-0.15em P}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}), Q)$.

Rmk. Define $Q(B):=\text{I\kern-0.15em P}(X^{-1}(B))$, or $Q=\text{I\kern-0.15em P} \circ X^{-1}$, and $Q$ is called the **pushforward measure, induced measure**, or **(cumulative) distribution function(c.d.f.)** of X.

Proof. (countable additivity) Notice that $X^{-1}(B_{n})=\{ \omega : X(\omega ) \in B_{n} \}$, and must be disjoint if $B_n$ disjoint, therefore $Q(\bigcup_{i=1}^ {\infty} B_{i})=\bigcup_{i=1}^ {\infty} \text{I\kern-0.15em P}(X^{-1}(B_{i}))=\sum_{i=1}^ {\infty} Q(B_{i})$.

## 2.4 Distribution function
Rmk. Because of the continuity, it's enough to know the **distribution function** $F_X(x):=\text{I\kern-0.15em P} \circ X^{-1}((- \infty, x]), \forall x$, given Caratheodory's extension theorem, to understand the prabability distribution of a random variable.

Prop. Distribution func is right continuous.
Proof. Given the monotonicity of $F_X$,
$$
\begin{align*}
\lim_{h\to0^+} F_{X}(x+h)
&=\lim_{h\to0^+} \text{I\kern-0.15em P} \circ X^{-1}((- \infty, x+h])
=\text{I\kern-0.15em P} \circ X^{-1}(\lim_{h\to0^+} (- \infty, x+h]) \\
&=\text{I\kern-0.15em P} \circ X^{-1}(\lim_{n\to  \infty} (- \infty, x+ \frac 1 n ])\\
&=\text{I\kern-0.15em P} \circ X^{-1}(\cap_{n=1}^{\infty} (- \infty, x+ \frac 1 n ])
=\text{I\kern-0.15em P} \circ X^{-1}((- \infty, x ])=F_{X}(x)
\end{align*}
$$

In contrast, for $\lim_{h\to0^-} F_{X}(x+h)=\text{I\kern-0.15em P} \circ X^{-1}((- \infty, x))=F_X(x-)$.

Def. (**Constant r.v.**) for some constant c, $\text{I\kern-0.15em P}(X=c)=\text{I\kern-0.15em P}(\omega \in \Omega: X(\omega)=c)=1$.

Def. (**Bernoulli r.v.**) $A \in \mathcal{F}$, r.v. $I_{A}$ that $I_{A}(\omega)=[\omega\in A]$.

Def. (**Discrete r.v.**) X takes values in some countable subset of $\mathbb{R}$, as a property of distribution func.

Def. (**Probability mass func p.m.f.**) $f(x)=\text{I\kern-0.15em P} \circ X^{-1}(\{x\})=\text{I\kern-0.15em P}(X=x)=F_X(x)-F_X(x-)$.

Def. (**(Absolutely) continuous r.v.**) distribution func $F_X(x)$ can be written as an integral of some Lebesgue integrable function $f:\mathbb{R} \to [0, \infty)$. $f$ is called **probability density function**(p.d.f.).


## 2.5 Random vector
Def.1 (**Random vector**) Given $(\Omega, \mathcal{F},  \text{I\kern-0.15em P})$, consider a function $\vec X: \Omega \to \mathbb{R}^n$, s.t. $X^{-1}(D) \in \mathcal{F}, \forall D \in B(\mathbb{R}^n)$.

Rmk. We can replace all Borel sets by all "rectangles".

Def.2 (**Random vector**) Given $(\Omega, \mathcal{F},  \text{I\kern-0.15em P})$, consider n random variables $X_i$, which means $X_{i}^{-1}(D_{i}) \in \mathcal{F}, \forall D_{i} \in B(\mathbb{R})$, to constitute $\vec X=[X_{1}, X_{2}, \dots, X_{n}]$.

Def. (**Random function**) By metric -> open set -> Borel $\sigma$-field.

Def. (**Joint distribution func**) $F_{X_{1}, X_{2}}(x_{1}, x_{2}) = \text{I\kern-0.15em P} \circ \vec X^{-1}((- \infty, x_{1}] \times (- \infty, x_{2}])$.

Def. (**Margined distribution func**) $F_{X}(x)=\lim_{y \uparrow  \infty} F_{X,Y}(x,y)$.

Def. (**(Absolutely) continuous r.v.s.**) distribution func $F_{X,Y}(x,y)$ can be written as an double integral of some Lebesgue integrable functions $f:\mathbb{R^2} \to [0, \infty)$. $f$ is called **joint probability density function**.

Two X, Y may not
#TODO 


# Ch3
## 3.1 Independence
Def. (**Independence of r.v.**) $X,Y:\Omega\to \mathbb{R}$ are independent($X  \perp \!\!\! \perp Y$) if $\text{I\kern-0.15em P}(X \in E, Y \in F)=\text{I\kern-0.15em P}(X \in E) \text{I\kern-0.15em P}(Y \in F),\forall E,F \in B(\mathbb{R})$.

Rmk. The following two are also equivalent to the definition:
1. Holding on all half spaces is enough: $F_{X,Y}(x,y)=F_{X}(x)F_{Y}(y)$.
2. Holding on all single points is enough: p.m.f if discrete; otherwise p.d.f

Def. (**Mutually independence of r.v.s.**) $F_{X_{1},X_{2}, \dots, X_{n}}(x_{1}, x_{2}, \dots, x_{n})=F_{X_{1}}(x_{1})F_{X_{2}}(x_{2}) \dots F_{X_{n}}(x_{n})$. By choosing $x_i= \infty$, we have the freedom to restrict on all subsets of r.v.s, not only all of them.

Rmk. Independence of events is a special case of indepence of r.v., given that $A  \perp \!\!\! \perp B \iff I_{A}  \perp \!\!\! \perp I_{B}$.

Thm. If $X  \perp \!\!\! \perp Y$, and two Borel measurable functions $g,h: \mathbb{R} \to \mathbb{R}$, then $g(X), h(Y)$ are still r.v.s., and that $g(X)  \perp \!\!\! \perp h(Y)$.
Proof. By measure theory.

E.g. $\omega=(\omega_{1}, \omega_{2}), X_{1}(\omega) \equiv \tilde X_{1}(\omega_{1}), X_{2}(\omega) \equiv \tilde X_{2}(\omega_{2})$, where $X_{1}, X_{2}$ are defined on the product space, then $X_{1}  \perp \!\!\! \perp X_{2}$.


Def. (**Bernoulli trial**) $A \in \mathcal{F}$. We call the trial a success if $A$ occurs. Bernoulli distribution  $X \sim Be(p)$.

Def. (**Binomial distribution** $Y \sim Bin(n,p)$) Perform n independent Bernoulli trials with $p=\text{I\kern-0.15em P}(A)$, and let Bernoulli r.v.s. $X_{1}, X_{2} \dots X_{n}$ be the indicator funciton of success of the experiments. Let $Y:=\sum X_{i}$, then the p.m.f. $f_{Y}(k)={n \choose k} p^{k} (1-p)^{n-k},k=1, 2, \dots, n$.

Def. (**Geometric distribution** $W \sim Geom(p)$) Keep performing Bernoulli trials until the first success, and let $W:=\text{the waiting time}$, then $f_{W}(k)=(1-p)^{k-1}p,k=1, 2, \dots$

Def. (**Negative Binomial distribution** $W_{r} \sim NB(r,p)$) Let $W_{r}:=\text{the waiting time for r sucesses}$, then $f_{W_{r}}(k)={k-1 \choose r-1} p^{r-1} (1-p)^{k-r}p ,k=1, 2, \dots$

Def. (**Poisson distribution** $X \sim poisson(\lambda)$) $f_{X}(k):= \frac{\lambda^{k}}{k!} e^{-\lambda}, k=1, 2, \dots$ The Poisson distribution is an approximation of a binomial distribution of a rare event in the case that n is large, p is small, and $\lambda=np$ is moderate.
