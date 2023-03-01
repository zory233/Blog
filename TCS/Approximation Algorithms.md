```toc
style: bullet | number | inline (default: bullet)
min_depth: number (default: 2)
max_depth: number (default: 6)
title: string (default: undefined)
allow_inconsistent_headings: boolean (default: false)
delimiter: string (default: |)
varied_style: boolean (default: false)
```

# Formulation

- **Optimization Problem** P
    - input and output $I, O \in \Sigma^*$
    - **computable cost function**
        - $C: \Sigma^* \times \Sigma^* \to \mathbb R^+$
        - $C_{opt}(I)=\inf_O C(I,O)$ (say it's a minimization problem)
- **Approximation algo for P with ratio $\rho$**
    -  $\forall I \in \Sigma^*, \max \{ {C(I,O_A) \over C_{opt}(I)}, {C_{opt}(I) \over C(I,O_A)} \} \le \rho$
    -  no matter maximization or minimization problem
    -  $\rho \ge 1$, could be a function of input or the desired solution quality
-   **Approximation scheme**
    - input $\epsilon>0$
    - output algo A such that it solves P within ratio $1+\epsilon$
- **Polynomial-Time Approximation Scheme(PTAS)**
    - $\forall \epsilon>0, \exists c_\epsilon, s.t., I \in \Sigma^n, T(A_\epsilon,I) \le n^{c_\epsilon}$
    - e.g. $O(n^{1/\epsilon })$
- **Fully Polynomial-Time Approximation Scheme(FPTAS)**
    - $\exists polynomial\ P, \forall \epsilon>0,I \in \Sigma^n, T(A_\epsilon,I) \le P(n,1/\epsilon)$
    - e.g. $O\left( \frac{n^4}{\epsilon^2} \right)$

# COMP5711 Scope

In summary, to find a PTAS, you may define parameters depend on eps, and show a XP algo has low relative deviation.

## e.g. minimum vertex cover(MIN VC)

- $C(G, X) = |X|$ if X is a vertex cover
- ApproxMinVC
    - given edge (u,v), then at least one of u and v have to be in the cover
    - choose both of them; remove them from G
    - linear time
- claim: $\rho = 2$ approximation
    - **Induction**
        $$
        \begin{gather}
        C(G, A)=2+C(G-u-v, A) \\
        C_{opt}(G) \ge 1+\min\{C_{opt}(G-u),C_{opt}(G-v)\} \\
        \text{show that: } C(G, A)<=2 C_{opt}(G)
        \end{gather}
        $$
    - **Reasoning**
        pairs of (u,v) will not overlap, then ApproxMinVC only doubles the size
- relation to set cover: the special case that every elements (as edge) appear at most twice(for once cases, simply add one dummy node)

## e.g. minimum set cover(MIN SC)

- decision version: NP-hard
- $C(S, X) = |X|$, if X, a set of S, is a set cover
- **greedy**: pick the "most useful" set in the remaining ones and then maintain usefulness correspondingly
- **claim**: greedy gives a $O(\log n)$-approximation algorithm for MIN SC
- t:=optimal, k:=greedy
- corner case: t=1, handle seperately
- **motivation**
    - at least one set chosen by OPT has $size \ge \lceil n/t \rceil$
    - then the 1st iteration of greedy has $|S_{i,1}| \ge \lceil n/t \rceil$
- **proof**
    - keep track of remaining size ni=|V| at i-th iteration
    - at least one set chosen by OPT has $size \ge \lceil n_{i}/t_{i} \rceil \ge \lceil n_{i}/t \rceil$, ti is the optimal solution for the status at i-th iteration
    - then since we're selecting the largest one, we have $n_i \le n_{i-1}- \frac{n_{i-1}}{t} \to n_i \le (1-\frac 1 t)^i *n$
    - find k such that $(1-\frac 1 t)^k <1/n$, then simply run k iterations and select these k sets
    - $k > \ln n *\frac{1}{\ln \frac t {t-1}}$ will be enough
    - one way is by WolfrarmAlpha, ${1 \over \ln \frac t {t-1}} < t$ for t>1; the other way is using $1-x<e^{-x}$
    - $k=1+t\ln n$ is enough -> $\frac{k}{t} = O(\ln n)$

## e.g. register allocation: minimum number of register

- **interference graph H**
    - variable set X
    - edge (x,y) iff the lifetimes of x and y intersect
    - use smallest amount of colors(registers) to color all vertices
    - two endpoints of each edge have different colors
- **control-flow graph(CFG) G**
    - directed graph $G=(V,E)$, showing control-flow
    - each node represents one line of code
    - sparse graph (at most two out edges)
    - theorm: treewidth<=7 ("*All Structured Programs Have Small Tree Width  and Good Register Allocation*")
    - say pathwidth is w
- **idea: use the bounded treewidth of G to solve H coloring**
    - variable x live in lifetime(x), a connecting subset of V
    -  $\alpha = \max_{v \in V} | \{ x \in X|v \in lifetime(x) \} |$ is a lowerbound of solution($OPT \ge \alpha$)
    -  for each bag b, $X_b \overset{def}{=} \{ x \in X|lifetime(x) \cap V_b \ne \emptyset \}$
-  **greedy on path decomposition**
    -  from left to right to color new vertices using the smallest colorid among usable colors
    -  validity: by induction.
    -  approximation: number of colors used is bounded by $|V_{b}|$, which is bounded by treewidth+1
    -  polynomial runtime
    -  $k \le \alpha(w+1)$
-   **greedy on tree decomposition**
    -  coloring from top to bottom

## e.g. Knapsack: maximum sum of values
- firstly formulate it as a optimize problem: maximize $C=\sum_{j \in S} v_{j}$, such that $\sum_{j \in S } w_{j} \le c$.
- normal DP: $O(nc)$
- approximate capacity is hard, let's look at value instead
- value-base DP: $dp[i,B']$ = the size of smallest knapsack that only contain first i items with total value at least B’, where $m=v_{max}, B = nm$, then $O(n^2m)$
- if we floor a item with value v into $\lfloor \frac v k \rfloor$, then if we pick $k=\max\{1, \lfloor \frac {\epsilon m} {2n} \rfloor \}, O(n^2m/k ) \to O(n^3/\epsilon)$, FPTAS.
- to prove the ratio:  (notice that to have $OPT \ge m$, remove those $w_{i} >c$)
  $$
  \begin{align}
  ANS 
    = ret \cdot k 
  &\ge \sum_{i \in S_{OPT}} v_{i}' \cdot k  \\
  & \ge \sum_{i \in S_{OPT}} v_{i} - k
  = OPT-|S_{OPT}| \cdot k \\
  &\ge OPT-n \cdot k = OPT - \frac{\epsilon}{2} m \\
  &\ge OPT - \frac{\epsilon}{2}OPT ~~~~~~~~ (OPT \ge m) \\
  \to
  \frac{OPT}{ANS} &\le \frac{1}{{1-\epsilon}/2} < (1+\epsilon),
  if\ \epsilon<1
  \end{align}
  $$
## e.g. Traveling Salesman Problem(TSP)
-  compute a route of minimum cost that visits every node of a complete, non-negative-weighted graph G exactly once.
-  claim: no PTAS unless P=NP
    - HAMILTONIAN CYCLE is NP-complete
    - make instance T in HAMILTONIAN CYCLE complete by adding edge weighted $w \in (1, \infty)$, and produce instance S of TSP
    - T is YES-instance iff $OPT(S)=|V|$
    - if exists $(1+\epsilon)$-approximation A, then let $w:=(1+\epsilon) |V|$, then T is YES-instance iff $ANS(S)=|V|$, otherwise $ANS(S) \ge (1+\epsilon)|V|$

## e.g. BIN PACKING: minimum # bin

-  ***BIN PACKING***: n items, each has size $s_i \in (0,1]$; infinit many bins of size 1; C=#bin
-  **claim1**: NP-hard
    -  ***SET PARTITION***: is there a partition such that $sum(A)=sum(C  -  A)$
    -  **reduction**: rescale instance T of *SET PARTITION* by $s_{i}= \frac{a_{i}}{ \sum a_{i}/2 }$ to reduce into a instance S of *BIN PACKING*. The instance T is a YES-instance of *SET PARTITION* if and only if S a 2-instance of *BIN PACKING*.
-  **claim2**: NP-hard to have polynomial ($\frac{3}{2} - \epsilon)$-approximation A
    -  hardness mainly from the case that OPT=2, because A will return at most $3-2\epsilon$, which will be 2. And if OPT=3, A can't do better than OPT and will return 3. Then finding A is as hard as solving NP-hard in polynomial time. BIN PACKING is hard to approximate with a ratio<3/2, unless P=NP.
-  **bound**: $OPT \ge \lceil \sum s_i \rceil$
-  **greedy1**: first-fit algo, a **2-approx.**
    -  add item one by one by finding the first bin that fits this item, or add one more bin otherwise
    -  **claim**: at any moment, at most one bin that is not greater than half full
        -  otherwise, we should put all the later ones in the former bin at that time
    -  then $\sum s_i > (k-1)/2$ when using k bins
        -  $k-1<2 \sum s_i \le 2 OPT \to k < 2OPT$
-  **greedy2**: first-fit algo + **sorting**, a **3/2-approx.**
    -  assume 3|k (k=3k’); look at the last item in the first 2k’ bin
    -  if the $s_{last}>\frac{1}{2}$
        -  then all previous 2k' bins have a (>1/2) item
        -  $OPT \ge 2k'=\frac{2}{3} k$
    -  if the $s_{last} \le \frac{1}{2}$
        -  at least 2 items in bins 2k'+1 ... 3k'-1, and 1 item in bin 3k', totally 2k'-1 items, that can be add in bins 1 ... 2k'-1, such that all bins overflow. Now we have $\sum s_{i} > 2k'-1$
        -  $OPT \ge \sum s_{i} > 2k'-1, OPT \ge 2k'=\frac{2}{3}k$
-  **consider variants by introducing 2 assumptions?**
    -  **assumption1**: $\forall i, s_i \ge \delta$
    -  **assumption2**: at most $K$ distinct $s_i$
    -  $m := \lfloor 1/\delta \rfloor$, the upperbound of # of items in each bin; to be specific, consider $(x_1,x_2,x_{3}, \dots ,x_K):=$ # of items of size $s_i$ in certain bin, where $x_{1}+x_{2}+x_{3} \dots x_{K} \le m$.
    -  $x_{1}+x_{2}+x_{3}+\dots+x_{K}+x' =m$
    -  $\alpha = {m+K \choose K}$ different types of bin
    -  similarly, ${\alpha+n \choose \alpha}$ different ways to combine bins, which is $\le (n + \alpha)^\alpha$
    -  $O( (n+\alpha)^\alpha p(n) )$ -> XP algo with params $K, \epsilon$, producing exact answer.
-  **assumption1 only?** $(1+\epsilon)$-approx.
    -  inspiration: like Knapsack, round up to nearest multiple of $\epsilon$ could be an approx.
    -  sort in $s_{1} \le s_{2} \dots \le s_{n}$
    -  instance $I^{up}$: partition equally into K groups, and then round elements in each group to the largest one in that group
    -  want K to be a function of $\epsilon$, so that we might get a PTAS
    -  it turns out $K=\lceil \frac{1}{\epsilon^{2}} \rceil$
    -  hopefully $OPT(I^{up}) \le OPT(I) (1+\epsilon)$, so that we can get a $(1+\epsilon)$-approx.
    -  we're sure that $OPT(I^{down}) \le OPT(I)$, so we only need to have $OPT(I^{up}) \le OPT(I^{down}) (1+\epsilon)$.
        - that means we try to obtain a solution of up from a solution of down
        - look at the last group, with at most $q = \lfloor \frac{n}{K} \rfloor$ elements
        - if put them in seperated bins, we can get $OPT(I^{up}) \le OPT(I^{down}) +q$
        - recall the bound: $OPT \ge \lceil \sum s_i \rceil \ge n \epsilon$
        - so $OPT(I^{up}) \le OPT(I^{down}) +n\epsilon^{2} \le OPT(I^{down})(1+\epsilon)$
- **no assumption at all?** $(1+\epsilon)OPT+1$
    - consider parameter $\epsilon'$ as a function of given $\epsilon$
    - recall greedy algo, we can pack $s \ge \epsilon'$ items first with $[assumption1\ only]$ algo to have an $(1+\epsilon)$-approx for that part, and for the remaining, use first-fit
    - it turns out $\epsilon'=\min \left\{  \frac{1}{2}, \frac{\epsilon}{2}  \right\}$, such that answer  $k \le (1+\epsilon)OPT+1$
    - case 1: small items do not create a new bin
    - case 2: small items create some new bins
        - the first item in the k-th bin gives a lowerbound to previous bins
        - $OPT \ge \sum_{i=1}^n s_{i} > (k-1)(1-\epsilon')$
        - $k-1 < \frac{OPT}{1-\epsilon'} \le OPT(1+\epsilon)$, if $\epsilon<1$
    - effective solution for the case that you know you will have far more than 2 bins, where you may ignore such 1

## e.g. Minimum Makespan Scheduling(MMS)
- **input**: n jobs; each takes $t_{i}$ time to finish; m identical machines
- find a assignment f to minimize the time they take($\max_{j} \sum_{f(i)=j} t_{i}$)
- **Graham's algorithm**: iterate through all jobs, and assign each job to the machine that has the smallest makespan at that time
- **lower bound**: $OPT \ge  \max (\lceil  \frac{\sum t_{i}}{m} \rceil, t_{max})=l$
- **2-approx. algo**
    - consider the last job that is assigned to each machine j
    - $T_{j}= t_{last_{j}}+\sum_{f(i)=j, i<last_{j}} t_{i}$
    - $t_{last_{j}} \le t_{max} \le l \le OPT$
    - $\sum_{f(i)=j, i<last_{j}} t_{i} \le \frac{\sum_{i<last_{j}} t_{i}}m\le \frac{\sum t_{i}}{m} \le l \le OPT$ (given that machine j had the smallest makespan at that time)
    - therefore $T_{j} \le 2l \le 2OPT$
- **$(1+ \frac{1}{3})$-approx. algo**
    - to get a $(1+ \epsilon)$-approx. algo, try to let $t_{last_{j}} \le \epsilon OPT$
    - from 2-approx, we know $l \le OPT \le 2l$
    - iterate through all jobs in the order that ti decreasing
    - no need to consider boundary case $m<n$; then there's a optimal sol. such that every machine has at least one job, and $m \ge n$
    - assign jobs in order
    - case 1: $t_{last_{j}} \le \epsilon OPT$: immediately $(1+\epsilon)$-approx.
    - case 2: $t_{last_{j}} > \epsilon OPT$
        - claim: $T_{j} = OPT$ when $\epsilon=\frac{1}{3}$
        - proof by contradiction: $T_{j}>OPT$
        - find the i such that $T_{j}$ no longer optimal, i.e. $ANS[1\dots i-1]=OPT[1\dots i-1]; ANS[1\dots i]>OPT[1\dots i]$, which means we can simply take $last_{j}=i$ to analyse(should still within case 2)
        - we know $t_{i} > \frac 1 3 OPT$, therefore every machine has at either 1 or 2 jobs now
        - say a job is **heavy** if it has a dedicated machine in $ANS[1\dots i-1]$
        - keep in mind that $ANS[1\dots i]$ is based on $ANS[1\dots i-1]$, while $OPT[1\dots i]$ maybe not based on $OPT[1\dots i]$.
        - **after putting i, a job k that was heavy in $OPT[1\dots i-1]$ is still heavy $OPT[1\dots i]$**: otherwise, that means we put i on that corresponding machine j. Given that ANS is worse than OPT, $t_{i} + t_{k}>OPT[1\dots i]$, i should not combine with k in OPT. 
        - now consider $i-1 \to i$
            - k:= # heavy job in first i-1
            - m-k remaining machines
            - 2(m-k) light jobs and the job $i$ to be assigned
            - there will be a machine with at least 3 jobs, contradict

# Linear Programming based
-  **Linear Programming(LP)**: vector of real variables $\vec x$, maximize $\vec c \cdot \vec x$, subject to a set of linear constraints $\vec a_{i} \vec x + b_{i} \le 0$. **LP is in P.**
-  **Integer Linear Programming(ILP)**: all variables are restricted to a destrete set of values. **NP-Hard.** e.g. 3-SAT can be reduced into ILP.
-  a common scheme of approximation algo design:
    1. reduce problem to ILP
    2. relax ILP to LP, and solve it(the only trivial part, because $ILP(A) \le LP(A)$ for maximization)
    3. round result of LP to integers without breaking constraints
    4. prove the rounded instance is an approximation
## e.g. Vector Cover
- reduction: $x_{v}=[\text{v is in VC}], \min \sum x_v$, subject to $x_{v}\in \{0,1\}; \forall (u,v) \in E, x_{u}+ x_{v} \ge 1$
- round by the usual rounding. Every edge must has one endpoint that is larger than half.
- this doubles variables that are larger than half, therefore $ANS \le 2 \cdot LP_{OPT} \le 2 \cdot ILP_{OPT}$, a 2-approx
## e.g. Set Cover
- rounding
    - regard x as sort of probability to be picked. In this case, 
  $$
  Pr[fail_{j}]=\prod_{i|(j \in S_{i})} (1-x_{i)}
  \le \prod_{i|(j \in S_{i})} e^{-x_{i}}=e^{-\sum_{i|(j \in S_{i})} x_{i}}
  \le \frac{1}{e}
  $$
      - still the logn trick, then $Pr[fail_{j]}\le \frac{1}{2n} \to Pr[fail] \le \frac{1}{2}$
  - $E[ANS]= O(\log n) \cdot \sum x_{i}=O(\log n) \cdot LP_{OPT} \le O(\log n) \cdot ILP_{OPT}$
  - $O(\log n)$-approx for proba=1/2
  - #todo: with high proba, it's a $O(\log n)$-approx
## e.g. Metric Store Location Problem
- problem: open store at point i takes $f_i$, and each costumer j has $c_{i,j}$ shipping cost from i to j, where $c_{i,j}$ comes from a metric space.
- \[reduction\]:
    - $\min \sum_{i} y_{i}f_{i}+ \sum_{j} \sum_{i} x_{i,j} c_{i,j}$
    - $x_{i,j}, y_{i} \in \{0,1\}; \forall j, \sum_{i}x_{i,j} \ge 1; \forall i,j, x_{i,j} \le y_{i}$
- OPT must have $\forall j, \sum_{i} x_{i,j} = 1$, no matter LP or ILP
- \[rounding\] **look at each costumer j**, define $C_{j}= \sum_{i} x_{i,j} c_{i,j}$, a weighted sum for j
    - **Markov**: the fraction of stores that server costumer j that are more than $k C_{j}$ far away from j is at most 1/k
    - **Filtering**: if $c_{i,j} >k C_j$, let $x_{i,j} \gets 0$; for remaining $x_{i,j}$, multiply by a constant C s.t. $\sum_{i} x_{i,j} =1$ still holds. The $y_i$ also need multiplying C. Then we know $C \le \frac{k}{k-1}$.
    - after such, take the costumer $j$ with the smallest $C_j$(expectation), and find the cheapest j-available($x_{i,j}>0$) store $i^*$, $c_{i^{*},j}\gets 1$, then close all other j-available stores, $y_{i'} \gets 0$.
- the total cost for one custormer j cannot increase, the first part is multiplied by $\frac{k}{k-1}$, and the second by $3k$. Then $\max\{ \frac{k}{k-1}, 3k \}=4, if\ k=\frac{4}{3}$
# Counting Problems
- given NP problem algo A, count the # certificate/proof
- it have to be more difficult than optimization/decision problem
- consider randomization(with fail rate less than $\delta$) and approximation($\epsilon$), i.e. for $\alpha=ANS(\text {CERT COUNT}), \beta=B_{\epsilon,\delta} (A, x, m)$, we want $$Pr[|\beta-\alpha| > \epsilon \alpha] <\delta$$, and runtime be polynomial in $|x|, \frac{1}{\epsilon}, \ln(\frac{1}{\delta})$. Here the logarithm is for repeating times given constant fail rate.
- **Monte Carlo method**: 
    - let $H=\{y|~|y|=m\}, G=\{y|~|y|=m \wedge A(x,y)=1\}$, then take N samples in H uniformly at random, among which S are in the G. We then output $\beta= \frac{S}{N} \cdot |H|$. The only variable we can adjust is N.
    - Note that $E[S]=N \cdot E[S_{i}]=N \cdot \frac{|G|}{|H|}=N \cdot \rho$. Then we actually want $Pr[|S-E[S]| > \epsilon E[S]] <\delta$. 
    - By Chernoff's bound, we know that $Pr[|S-E[S]| > \epsilon E[S]] < 2 exp(- \frac{\epsilon^2}{3}E[S])$, so we want to have $2 exp(- \frac{\epsilon^{2}}{3}E[S])\le \delta$. 
    - By rearranging, it's sufficient to take $N:= \frac{3 \ln(2/\delta)}{\epsilon^{2} \rho}$. 
    - The runtime is $O\left( \frac{1}{\rho} \cdot \ln (\frac{1}{\delta}) \cdot \frac{1}{\epsilon^{2}} \cdot T(A,x,y) \right)$.
    - Notice that $\rho$ might be small, but when it's big, this gives a good algo already.

## e.g. Disjuctive Normal Form(DNF) counting
- the disjunction of k conjective clauses
- an valuation satisfies DFN only need to satisfies at least one of the clauses
- try to define G and H in a smarter way s.t. $\rho$ is large.
- for an evaluation v, define its index as the first clause that is satisfied.
- we hope to count H, so keep H the same size, as $\{(y,i)|~|y|=m \wedge A(x,y)=1 \wedge i=index(y)\}$
- however, we pick a much smaller G, as $\{(y,i)|~|y|=m  \wedge C_i(y)=1\}$.
- every certificate in G already satisfies DNF, so that $|G| \le k \cdot |H|$
- $\frac{1}{\rho}= O(|x|)$

## e.g. Perfect Bipartite Matching counting
-   [Lecture 25: Counting Perfect Bipartite Matchings (Video)](https://canvas.ust.hk/courses/45495/modules/items/990303 "Lecture 25: Counting Perfect Bipartite Matchings (Video)")
- 