```toc
style: bullet | number | inline (default: bullet)
min_depth: number (default: 2)
max_depth: number (default: 6)
title: string (default: undefined)
allow_inconsistent_headings: boolean (default: false)
delimiter: string (default: |)
varied_style: boolean (default: false)
```
Basics
1. **random**: we consider **randomness in algorithm**, but a **fixed worst input**
2. $Pr[fail]=1-\frac{1}{p(n)}$, then repect p(n) times, such that $Pr[allfail]=(1-\frac{1}{p(n)})^{p(n)} \to \frac{1}{e}$
3. $Pr[fail]=1/c$, repect $t \log n$ times, such that $Pr[allfail]=(\frac{1}{c})^{t \log n} = \frac{\log c}{n^{t}}$
4. $Pr[\text{at least one among n fail}] = \cup_i Pr[\text{i fail}] \le \sum_i Pr[\text{i fail}] \le n \cdot \frac{\log c}{n^{t}}$

# Randomized Complexity Classes

[Complexity](https://www.notion.so/Complexity-8e6fc7b3400544d89f3032b13ad45424)

## Normal Problem

## e.g. QuickSort
-   sorting a permutation of n by choosing a pivot and put smaller ones on left
-   $T(n)=f(n)+T(h_1(n))+T(n-h_1(n)-1)$
-   when we say a pivot is good enough? say $n/4 < h_1(n) < 3n/4$
**if we randomly pick pivot until it’s good enough**
-   $f(n)=(n-1)* {1 \over {1/2}}$
**if we simply randomly pick one, and that’s it?**
-   say $X_{i,j}$ is a random variable indicating whether i-th and j-th smallest elements are compared
-   $E[\sum_{i<j} X_{i,j}]=\sum_{i<j} E[X_{i,j}]$
-   i-th and j-th smallest elements is compared ↔ one is the ansector of the other on the binary tree of dividing ↔ i-th or j-th smallest element is the first being chosen as pivots in $[i,j]$ elements ↔ $\frac{2}{j-i+1}$ for random permutation
-   $\sum_{i<j} \frac{2}{j-i+1}=2\sum_l \frac{n-l+1}{l}=O(n \log n)$

## e.g. MinimumCut

- input: undirected, unweighted, multi-edges, no self-loops, connected $G=(V,E)$
- contraction algo:
    - pick an edge (u,v) randomly
    - contract edge by replacing u and v with new supernode w and preserving edges(keep parallel edge, but remove self-loops)
    - repeat until only two supernodes left
- consider the first edge we contract; the probability that wrongly contract a edge in mincut: $\frac{|C|}{|E|} \le \frac{k}{nk/2}$
-   totally n-2 contraction, we can do recursive analysis
-   $P(n) \ge P(n-1) * (1-2/n) \ge \frac{(n-2)!2}{n!}=\frac{2}{n(n-1)}$
-   run multiple times, then $P(wrong)=(1-\frac{2}{n(n-1)})^{n(n-1)/2} \le 1/e$
-   run more multiple times, then $P(wrong)=(1-{1 \over e})^{k}$



## Zero-Sum Matrix Game

e.g. Rock-Paper-Scissor

-   player 1 want to maximize
-   $\max_{i \in \{R,P,S\}} \min_{j \in \{R,P,S\}} A_{i,j}=-1$
-   notation issue: the left operator choose first, and to maximize the score
-   if players choose probability distribution?
-   $F=\max_{\delta_i \in \Delta(\{R,P,S\})} \min_{\delta_j \in \Delta(\{R,P,S\})} \mathbb{E}_{i \sim \delta_i, j \sim \delta_j} [A_{i,j}]=0$

**Prop**: all zero-sum matrix game have

$$ \max_{\delta_i \in \Delta(\{R,P,S\})} \min_{\delta_j \in \Delta(\{R,P,S\})} \mathbb{E}_{i \sim \delta_i, j \sim \delta_j} [A_{i,j}]

=\min_{\delta_j \in \Delta(\{R,P,S\})} \max_{\delta_i \in \Delta(\{R,P,S\})} \mathbb{E}_{i \sim \delta_i, j \sim \delta_j} [A_{i,j}] $$

### Yao's Minimax Principle: algorithm-adversary input

-   consider player 1 choose algorithm $A_i$ and player 2 choose input $I_j$ from **finite set**?
-   player 1 want to minimize the cost

deterministic algo: player 1 just choose a certain row

undeterministic algo: player 1 choose a probability distribution; player 2 doesn’t need to do so, but instead just pick the worst one

$$ \begin{align*} (chosen\ \delta_A)\max_{j \in I} \mathbb{E}_{i \sim \delta_A} [A_i,I_j] &\ge \min_{\delta_A \in \Delta(Algo)} \max_{j \in I} \mathbb{E}_{i \sim \delta_A} [A_i,I_j] \\

&\text{\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ ||} \\

(chosen\ \delta_I)\min_{i \in A} \mathbb{E}_{j \sim \delta_I} [A_i,I_j] & \le\max_{\delta_I \in \Delta(Input)} \min_{i \in A} \mathbb{E}_{j \sim \delta_I} [A_i,I_j] \end{align*} $$

[choosing a **WC**(worst-case) input over a **randomized algo**] is at most as good as [choosing the best algo over an **arbitrary input distribution**]

## e.g. Minimax-Tree/And-Or Tree/Game Tree

-   $T_k=$full binary tree with k max layers, k min layers and 4^k leaves
-   every node is either max or min except leaves, on which have numbers
-   each min has 2 max children, vice versa
-   imaging reading input(values on leaves) is expensive, and we hope to output the value at root
-   adversary input:
    -   let the deterministic algorithm can only find the value of only one node each query → $C_k=4^k$
    -   when root=AND, give T first and hide F in later [*]
-   we want to evaluate: **when the input is the worst, what’s the expected runtime of our algo.**

### [upper bound] top-down view considering worst case [maybe problematic]

-   recall: we consider **randomness in algorithm**, but a **fixed worst input**
-   say root is AND
-   C[k]=max{root=F, root=T} to give a rough bound (theoretically we should use C[k,T/F])
    -   root=F (say transverse child 1 first)
        -   children are OR nodes
        -   case1: child1 with F(OR1=F)
        -   case2: child1 with T(OR1=T)
            -   OR1=T, need 0.5_C[k-1]+0.5_2*C[k-1]
            -   OR2=F → both children of child2 is F → 2C[k-1]
        -   0.5_2C[k-1]+0.5_3.5C[k-1]
    -   root=T
        -   OR1=OR2=T
        -   each has 1/2 chance that only need to evaluate one side
        -   2*(C+0.5C)
-   $C_k \le \max\{ {11 \over 4} C_{k-1}, 3 C_{k-1} \}=3 C_{k-1} \le 3^k$

### [lower bound] with Yao’s Technique

-   **replace all operations in tree to be NOR while the root(MAX) value remains unchanged**
    -   a NOR b=NOT(a OR b)=(NOT a) AND (NOT b)
    -   (a or b) and (c or d)=(a nor b) nor (c nor d)
-   now that we have a fix distribution of input $\delta_I^*$
-   if all leaves have P(one)=p, then P(parent)=(1-p)^2
-   $p=(1-p)^2 \to p=\frac{3-\sqrt 5}{2}$
-   what happen to our best deternimistic algo? Let’s find a lower bound
-   $C_k \ge p C_{k-1}+(1-p)2 C_{k-1}=(2-p)C_{k-1}={1+\sqrt 5 \over 2} C_{k-1}$
-   now we get a very rough bound

## **Lemma1**

when we’re at n, we randomly choose a x, with $E[x]$

-   #TODO

$$ E[T_n]=1+E_{x \sim X}[T_{n-x}] \ge 1+E_{x \sim X}[\int_1^{n-x} \frac 1 {g(t)} dt] $$

### e.g. lemma1→QuickSelect

-   select k-th smallest element in a permutation of size n
-   by choosing a pivot and put smaller ones on left
-   want to analyze **the depth of recursion**
-   decreasing n by X
-   $E[X] \ge \frac 1 2(\frac 1 4 n)+\frac 1 2=\frac 1 8 n+\frac 1 2 \ge n/8=g(n)$
-   $E[T_n] = O(\log n)$

## Derandomization

### e.g. Max 3-SAT

-   maximize # clauses that can be satisfied
-   flip a coin to decide each variable (each variable may appear multiple times)
    -   $E(X)=\sum_{i-th\ clause} E(X_i)=n*\frac 7 8$
-   this leads to a deterministic algo
    -   pick x1 such that there’re the most potential clauses left
    -   #TODO

## Martingales

## Probability Bounds

TODO: https://math.mit.edu/~goemans/18310S15/chernoff-notes.pdf




“with high probability”: $\lim_{n \to \infty} Pr[\epsilon]=1$

-   a and k do not need to be deterministic

$$
\begin{gather}
\text{Markov’s inequality } X \ge 0, \forall a>0, P(X \ge a) \le E(X)/a \\ \text{Chebyshev's inequality } \forall k>0, P(|X-\mu| \ge k \sigma) \le 1/k^2 
\end{gather}
$$

e.g. **Balls and Bins**

-   n labeled bins and n unlabeled balls; throw balls into bin in order
-   ${n \choose i} \le (ne/i)^i$ ????????? #TODO
-   why k=xx, then <1/n^2 ????????? #TODO

$$
\begin{gather}
\epsilon^*_j(i)=\text{bin j has exactly i balls}= \\ {n \choose i} (\frac 1 n)^i (1-\frac 1 n)^{n-i} \le {n \choose i} (\frac 1 n)^i \le (\frac {ne} i)^i (\frac 1 n)^i=(\frac e i)^i \\

\epsilon_j(k)=\text{bin j has at least k balls}= \sum \epsilon^*_j(k) \le \sum_{i=k}^\infty (e/i)^i\le \frac{(e/k)^k}{1-e/k} \\

when\ k=\lceil \frac{e\ln n}{\ln\ln n} \rceil, \epsilon_j(k) \le 1/n^2 \\ Pr[\cup \epsilon_j(k)] \le \sum Pr[\epsilon_j(k)] \le 1/n \to 0
\end{gather}
$$

-   n labeled bins and m unlabeled balls, how large the m need such that we can say with a high probability, all bin have less than k balls

$$
\begin{gather}
\epsilon_i=\text{i-th ball falls into an empty bin} \\ Pr[\cap \epsilon_i]=\prod (1-\frac{i-1}{n}) \le \prod exp(-\frac{i-1}{n}) \\ =exp(-\frac 1 n \sum \frac{i-1}{n}) =exp(-\frac{m(m-1)}{2n})\\ m=\lceil \sqrt{2n}+1 \rceil, Pr[\cap \epsilon_i] \le 1/e \\ m=\lceil \sqrt{2n}+1 \rceil \log^*n,Pr[\cap \epsilon_i] \le (1/e)^{\log^*n} \to 0\\ 
\end{gather}
$$

-   how large m should be, such that with low probability, there’s no empty bin
    
$$
\begin{gather}
X_i=\text{step needs to touch the i-th bin,which are independent} \\ E(X_i)=\frac{1}{(n-i+1)/n}=\frac{n}{n-i+1}, \\ E(X)=\sum_{i=1}^{n} E(X_i) \le n\ln n+O(n),Pr[X \ge 2n\ln n]\le 1/2+o(1)\\ Var(X)=\sum Var(X_i)=\sum \frac{1-p}{p^2}=\\ n \sum \frac{i}{(n-i)^2} \le n^2\sum_j {1 \over j^2}= O(n^2)\\ Pr[X \ge 2n\ln n]\le O(1/\ln ^2n) \to 0
\end{gather}
$$
    

## e.g. Lazy Select

-   input: araay A of size n, elements are distinct and comparable
-   goal: output median of A (could be k-th) in O(n)
-   procedure
    -   randomly choose a subarray R of size m and then sort it in O(mlogm)≤O(n)
    -   take two pivots u,v from neighbors of the median of R (say $m/2- \alpha , m/2+\alpha$)
    -   **claim: with high probability, the median of A is between these two pivots in A**
    -   view “sorted” A into [A1 u A2 v A3]; sort A2
-   failure
    -   the A2 is too large (larger than $\beta$)
    -   the median of A is not in A2
-   result: $m=n^{3 \over 4}, \alpha=\sqrt n, |A_2| \le 4n^{3 \over 4}$

Analysis:

-   assume simpling elements are **repeatable** (such that independent sampling)
-   Pr[FAIL] ≤ Pr[|A1|>n/2]+Pr[|A3|>n/2]+Pr[ (|A2|>beta) | condition1,2 holds]
-   Pr[|A1|>n/2]=Pr[ R’[u]>A’[n/2] ]=Pr[ at least m/2+alpha elements in R are larger than median of A ]=Pr[X≥m/2-alpha]
    -   X is the number of naughty samples=X1+X2…Xm
    -   E[Xi]=1/2-1/n, E[X]=mE[Xi]~m/2
    -   Var[Xi]=1/4-1/n^2, Var[X]=mVar[Xi]~m/4
    -   Chebyshev’s: Pr[X≥m/2+alpha]~Pr[X-E[X]≥alpha] ≤ $\frac 1 2 \frac{Var^2}{\alpha^2}=\frac {m^2} {8 \alpha^2}$
-   Pr[ (|A2|>beta) | condition1,2 holds]
    -   intuition is that alpha is small but cover a large portion of A
    -   the same as saying “at least half of elements in A2 is larger than median of A”  #TODO
    -   rank(A,u)≥n/2+beta/2=t
    -   Y is the number of naughty samples(larger than A[t])=Y1+Y2…Ym
    -   E[Yi]=(n-t)/n, Var[Yi]=(n-t)t/n^2, E[Y]=mE[Yi]=m(n-beta)/(2n)=m/2-mbeta/(2n), Var[Y]=mVar[Yi]=m(n^2-beta^2)/(4n^2)
    -   Pr[ Y≥m/2-alpha ]~Pr[Y-E[Y]≥mbeta/(2n)-alpha]

### Chernoff inequality

**result**: $Pr[X\ge (1+\epsilon)\mu] \le (e^\epsilon/(1+\epsilon)^{1+\epsilon})^\mu$

moment generating function $Y=M_X(t)=\mathbb E [ e^{tX} ]$

independent r.v. X,Y, $M_{X+Y}(t)=M_{X}(t)M_{Y}(t)$

**e.g.**

r.v. X=X1+X2..+Xn independent, where Xi~B(1,pi)

$\mathbb E[e^{tX}]=\sum_{i=0}^\infty \frac{ t^i \mathbb E [X^i]}{i!}, \frac{d^k}{d t^k}|_{t=0} \mathbb E[e^{tX}]= \mathbb E[X^k]$

given 1+x≤e^x, $\mathbb E[e^{tX_1}]=p e^t+1-p=1+p(e^t-1) \le e^{p(e^t-1)}$

$M_X(t)=\mathbb E[e^{tX}]=\prod_i \mathbb E[e^{tX_i}] \le e^{(e^t-1) \sum p_i}=e^{(e^t-1) \mu}$, here mu is the expectation

$Pr[X \ge a]=Pr[e^{tX}\ge e^{ta}] \le \frac{\mathbb E[e^{tX}]}{e^{ta}}=\frac{M_X(t)}{e^{ta}}$ [markov] **works for all t**

therefore $Pr[X \ge a] \le \inf_{t\ge0} \frac{e^{(e^t-1) \mu }}{e^{ta}}, Pr[X \le a] \le \inf_{t\le0} \frac{e^{(e^t-1) \mu }}{e^{ta}}$

$Pr[X\ge (1+\epsilon)\mu] \le \inf_t e^{(e^t-1) \mu -t(1+\epsilon)\mu }= (\inf_t \frac{e^{e^t-1}}{e^{t(1+\epsilon) }} )^\mu$

$\frac{d}{dt} exp(e^t-1 -t(1+\epsilon))=(e^t-1-\epsilon)exp(e^t-1 -t(1+\epsilon))=0$

set $t=\ln(1+\epsilon),$ then $Pr[X\ge (1+\epsilon)\mu] \le (e^\epsilon/(1+\epsilon)^{1+\epsilon})^\mu$

**e.g.**

pi=1/2, $Pr[X \ge 0.8n] \le \frac{e^{n(e^t-1)/2}}{e^{0.8nt}} \le (0.859)^{n/2}$ by calculus

lemma2: $R^\mu,\epsilon^2/3 \le R \le \epsilon^2/2$

### Probabilistic Method

**e.g. prove MaxCut≥|E|/2**

put vertex into A with proba 1/2

$\mathbb E[X]=\sum \mathbb E[X_i]=\sum 1/2=|E|/2$, then **such a cut exists**

combine this idea with derandomization → construct such a cut

insight: E[plan A] ≤ E[X] ≤ E[plan B], choose B, then existence of that kind of cut is preserved

**e.g. dominating set ($S \cup N(S)=V$)**

randomly choose S1 with E[|S1|]=np, and then pick $S_2=\{ v| v \notin S_1,N(v) \notin S_1 \}$

$\mathbb E[|S_{2,v}|]=(1-p)^{deg_v+1} \le (1-p)^{mindeg+1}, \mathbb E[|S_{2,v}|] \le n(1-p)^{mindeg+1}$

calculus → $p=\ln(mindeg+1)/{mindeg+1},\mathbb E[|S|] \le n\frac{\ln (mindeg+1)+1}{mindeg+1}$

**e.g. Ramsey Numbers**

-   R(r,b): smallest graph such that either a red clique of size r, or a blue clique of size b exist
-   upper bound exists by inductive method: R(r,b)≤R(r-1,b)+R(r,b-1)
    1.  the only case that can’t satisfy the (r,b) is that red edges connecting vertex 1 is less than R(r-1,b) and blue edges connecting vertex 1 is less than R(r,b-1) → total # vertex is less than R(r-1,b)+R(r,b-1)-1
    2.  inductive by increasing r+b
    3.  R(r,b)≤2^(r+b)*C
-   how about lower bound?
    -   N<R(k,k)
    -   can construct a graph with size N such that no red clique or blue clique with size k
-   X = # of single-colored cliques of size k = $\sum_{S \subset V,|S|=k} X_S$
    -   want to show that E[X]<1 by choosing N base on k
-   $\mathbb E[X_S]=2^{1-{k \choose 2}}, \mathbb E[X]={|V| \choose k} \mathbb E[X_S]={N \choose k} 2^{1-{k \choose 2}}<1 \to {N \choose k}< 2^{{k \choose 2}-1}$
-   enough to have $N<2^{k/2}$

## e.g. Treap

**a binary search tree w.r.t. key and, at the same time, a max heap w.r.t. priority**

**Lemma3**: treap unique for set of elements with distinct keys and priorities

inductively, unique root and division of two sides

**operations**

-   change priority
    -   maintain the heap property under restriction of BST property by rotations
    -   runtime is bounded by the height of tree
-   add new element
    -   add it to the tree as if it has the lowest priority, and then change it
    -   runtime is bounded by the height of tree
-   delete a element
    -   change its priority to the lowest and delete it, a leaf
    -   runtime is bounded by the height of tree

**analysis**

assume the keys $K_1<K_2<\dots<K_n$

Xi = # ancestor of ei = $\sum_j X_{i,j}$

$\mathbb E[X_{i,j}]=Pr[P_j\text{ is the largest among i to j}]=1/(|j-i|+1)$

$\mathbb E[X_i]=\sum_{j} 1/(|j-i|+1)=\sum_{j<i} 1/(i-j+1)+\sum_{j>i} 1/(j-i+1)=O(\log n)$

## e.g. skip list

![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/Skip_list.svg/800px-Skip_list.svg.png)
[wikipedia](https://en.wikipedia.org/wiki/Skip_list)

-   add
    -   search, update the lowest level link list, and then flip a coin to decide whether update next level link list.
    -   $1+1/2+1/2^2 .. \to 2$
-   lemma4: with high proba, the # levels ≤ clogn for every c>1
    -   $Pr[\#level>K] \le n*Pr[K\ heads]=n/2^{K}$
    -   pick $K=c\log n,c>1$ is enough
-   search
    -   reverse the search process to analyse: whenever can go up, go up, otherwise go left
    -   when coin is head, go up, otherwise go left
    -   recall that Pr[X≥0.8n]≤(0.857)^(n/2)
    -   by lemma4, with high proba, we can only go **up** clogn times, let’s assume so
        -   $Pr[\#left \ge 4clogn] \le Pr[X' \ge 0.8n'] \le (0.857)^{n'/2}$, where n’=5clogn

#TODO: n'对应#left这个rv的trial的总数

## Lemma5

-   n balls in a bin, where b balls are white and n-w=b balls are black
-   goal: take r balls randomly so that exactly 1 white ball is taken, with proba≥c
-   proba=$\frac{w {b \choose r-1}}{n \choose r}$
-   lemma5: if $\frac n {2w} \le r \le \frac n w$, correct proba≥1/(2e)

## boolean matrix multiplication

-   in boolean matrix multiplication, $c_{i,j}=\vee_k (a_{i,k} \wedge b_{k,j})$, say those good k as witnesses
-   for boolean matrix A, consider $\bar A, \bar a_{i,j}=j*a_{i,j}$
-   if witnesses is unique, which means we’re lucky, we can have $\bar C=\bar A B$ to find the witnesses
-   let’s kill some witnesses by only selecting some of columns to have $\bar a_{i,j}=j*a_{i,j}$, others 0
-   to use lemma 5 to find a suitable r, we need to know w, which is # witnesses, **w.r.t each cij**
-   hard to know w, then let’s just try different r
-   $r=2^k, n/2^{k+1} \le w \le n/2^k$, covers all possible w
-   for each r, repeat this process 2e times
    -   randomly pick r columns, kill others, then do a matrix multiplication, check the validity of computed witness for each cij
-   correct rate=$(\frac 1 {2e})^{n^2}$, a constant

#TODO: on ipad

-   $O(n^\omega \log n)$
-   repeat $\log n$ times

## e.g. all-pairs shortest path

**input**: unweighted undirected graph G=(V,E), sequence of queries (i,j)

**output**: print Dij and one shortest path between them

**constraint**: have to solve each query (i,j) in **optimal** expected time O(Dij)

**sol1**: preprocess BFS tree for each start point with O(n^3) when |E|~n^2

**sol2**: Floyd-Warshall algorithm: dynamic programming

[we know that matrix multiplication can be done in $O(n^\omega), \omega \le 2.373$]

1.  define $G^{(2)}$, where **i and j are connected if their distance is not more than 2**

-   $A^{(2)}=max(A^2,A)$
-   $D_{tj}^{(2)}=\lceil D_{ij}/2 \rceil$
-   recursively until 2^k, $D_{ij}^{(2^k)}=1, \forall i,j$

1.  consider the distance in G

-   $D_{ij}\ even \to \forall t \in N_G(i), D_{tj}^{(2)} \ge D_{ij}^{(2)}$
-   $D_{ij}\ odd \to \exists t^* \in N_G(i), D_{t^*j}^{(2)} <D_{ij}^{(2)} ;\forall t\in N_G(i),D_{tj}^{(2)} \le D_{ij}^{(2)}$

1.  how to restore?

-   $\exists t^* \in N_G(i), D_{t^*j}^{(2)} <D_{ij}^{(2)} \to D_{ij}\ odd \to D_{ij}=2D_{ij}^{(2)}-1$
-   otherwise, it’s even, $D_{ij}=2D_{ij}^{(2)}$

1.  to make it similar to matrix, consider the sum form

-   $(\sum_{t \in N_G(i)} D_{tj}^{(2)} < |N_G(i)|D_{ij}^{(2)}) \to D_{ij}\ odd$
-   $(A D^{(2)} < |N_G|D^{(2)})$

1.  restore the D from $D^{(2^k)}$ can be done in $O(n^\omega \log n)$
2.  how about the shortest path? need to find witness to retore the process of dynamic programming
    -   we know boolean matrix multiplication and witness computation with expected runtime $O(n^\omega \log^2 n)$
    -   consider the path u, k1, k2, …. v
    -   the condition of k1?
        -   $D_{u,t}=1 \wedge D_{t,v}=t-1$
        -   observe that all vertex beside u can only have $D_{t,v}=m-1,m,m+1$
        -   $D_{u,t}=1 \wedge D_{t,v}=t-1 (\mod 3)$
        -   $AW^{(t-1\mod 3)}$, only need 3 set of W
    -   witness? $\mathbb E=(c\times \frac{n-1}n+n\frac{1}n)=c+1$ to ensure a valid witness #TODO