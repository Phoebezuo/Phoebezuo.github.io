---
layout:     post
title:      Practice about Models of Computation
date:       2020-12-12
summary:    Questions with solution on Models of Computation
categories: Computation Logic DFA RegEx
---

# Question 1

<img src='https://i.loli.net/2020/12/09/ASwfc29DoxebEnR.png' alt='ASwfc29DoxebEnR'/>

| p    | q    | $(p \rightarrow (p \rightarrow q))$ | $(q \rightarrow (q \rightarrow p))$ |
| ---- | ---- | ----------------------------------- | ----------------------------------- |
| F    | F    | T                                   | T                                   |
| F    | T    | T                                   | F                                   |
| T    | F    | F                                   | T                                   |
| T    | T    | T                                   | T                                   |

As shown from the table above, when p is F, q is T, $(p \rightarrow (p \rightarrow q)) = T$, but $(q \rightarrow (q \rightarrow p))$ = F.

Hence, they are not logically equivalent.


<img src='https://i.loli.net/2020/12/09/mVhWnyXGUYcaJ9Q.png' alt='mVhWnyXGUYcaJ9Q'/>

| p    | q    | r    | $((p \rightarrow (q \lor r)) \rightarrow ((p \rightarrow q) \lor (p \rightarrow r)))$ |
| ---- | ---- | ---- | ------------------------------------------------------------ |
| F    | F    | F    | T                                                            |
| F    | F    | T    | T                                                            |
| F    | T    | F    | T                                                            |
| F    | T    | T    | T                                                            |
| T    | F    | F    | T                                                            |
| T    | F    | T    | T                                                            |
| T    | T    | F    | T                                                            |
| T    | T    | T    | T                                                            |

As shown from the table above, all the output is T.

Hence, it is valid and satisfiable.

<img src='https://i.loli.net/2020/12/09/V5yTH7mgDLC2Wfr.png' alt='V5yTH7mgDLC2Wfr'/>
$$
\begin{align}
((p \lor (q \lor r)) \land (r \lor \neg p)) &\equiv (((p \lor q) \lor r) \land (r \lor \neg p)) \qquad &\text{associative}\\
&\equiv (((p \lor q) \lor r) \land (\neg p \lor r)) \qquad &\text{associative}\\
&\equiv (((p \lor q) \land \neg p) \lor r) \qquad &\text{distributive}\\
&\equiv (((p \land \neg p) \lor (q \land \neg p)) \lor r) \qquad &\text{distributive}\\
&\equiv ((\bot \lor (q \land \neg p)) \lor r) \qquad &\text{definition of $\bot$}\\
&\equiv ((q \land \neg p) \lor r) \qquad &\text{unsatisfiability}
\end{align}
$$

<img src='https://i.loli.net/2020/12/09/mg8PzaSqtDCbwsu.png' alt='mg8PzaSqtDCbwsu'/>

| Line | Assumptions | Formula                                         | Justification    | References |
| ---- | ----------- | ----------------------------------------------- | ---------------- | ---------- |
| 1    | 1           | $(p \rightarrow  \neg q)$                       | Assump. I        |            |
| 2    | 2           | $( \neg r \lor p)$                              | Assump. I        |            |
| 3    | 3           | $p$                                             | Assump. I        |            |
| 4    | 4           | $ \neg r$                                       | Assump. I        |            |
| 5    | 5           | $( \neg p \rightarrow r)$                       | Assump. I        |            |
| 6    | 6           | $ \neg p$                                       | Assump. I        |            |
| 7    | 5,6         | $r$                                             | $ \rightarrow $E | 5,6        |
| 8    | 4,5,6       | $ \bot $                                        | $ \neg $E        | 4,7        |
| 9    | 4,5         | $p$                                             | RA               | 6,8        |
| 10   | 2,5         | $p$                                             | $ \lor $E        | 2,3,3,4,9  |
| 11   | 1,2,5       | $ \neg q$                                       | $ \rightarrow $E | 1,10       |
| 12   | 1,2         | $(( \neg p \rightarrow r) \rightarrow  \neg q)$ | $ \rightarrow $I | 5,11       |


<img src='https://i.loli.net/2020/12/09/jLfUMosZg4TuWih.png' alt='jLfUMosZg4TuWih'/>

For the statement 2, if $F_1 = p$ and $F_2 = \neg p$, they are both individdually satisfiable. However, $F = (F_1 \land F_2) = (p \land \neg p) = \bot$, which is not satisfiable.

# Question 2

<img src='https://i.loli.net/2020/12/09/8ZGU1NtEgHFknQa.png' alt='8ZGU1NtEgHFknQa'/>

The required predicate formula is $\neg eq(x,y) \land \exist x' \exist y' (child(x,x') \land child(y,y') \land sib(x',y'))$.

The $sib(x',y')$ is the formula. $\neg eq(x',y') \land \exist. z (child(x',z) \land child(y', z))$

<img src='https://i.loli.net/2020/12/09/pOsIQPfqytRgWCU.png' alt='pOsIQPfqytRgWCU'/>

If there exists a sentence F and a proof $F \vdash \bot$,  then this F is unsatisfiable.

If we can show $F \vdash \bot$ then we can deduce (by soundness of ND) that $F \vDash \bot$, which means that every assignment that satisfies *F* also satisfies $\bot$. But since no assignment satisfies $\bot$, no assignment satisfies *F*, i.e. *F* is unsatisfiable.

<img src='https://i.loli.net/2020/12/09/COXKZo8x7y5uFqS.png' alt='COXKZo8x7y5uFqS'/>

For all $z \in \mathbb{Z}$ and $y \in \mathbb{Z}$ such that if x < y where $x \leq 0$, then $x + y \geq 0$.

Compute the TV($\forall x \forall y G, \alpha$), where G is the formula $(A(x,y) \rightarrow B(x,y))$. where $A(x,y) = (P(x,y) \land (P(x,c) \lor Q(x,c)))$ and $B(x,y) = (P(c, f(x,y)) \lor Q(c, f(x,y)))$

By the rule of $\forall$ (applied twice), TV($\forall x \forall y G, \alpha$) = 0 if there exist $d \in A$ or $e \in A$: TV($\forall x \forall y G, \alpha[x,y \mapsto d,e]$) = 0.

By the rule for predicates, this means that:

-   $tv(P(x,y), \alpha) = 1 \text{ if } \alpha(x) < \alpha(y)$, and 0 otherwise.
-   $tv(Q(x,y), \alpha) = 1 \text{ if } \alpha(x) = \alpha(y)$, and 0 otherwise.

$$
\begin{align}
	TV(\forall x \forall y G, \alpha) \equiv &\min\{TV(\forall y G, \alpha[x \mapsto d])\} \\
	\equiv &\min\{\min\{TV(A(x,y) \rightarrow B(x,y), \alpha[x,y \mapsto d,e])\}\} \\
    \equiv &\min\{\min\{TV(\neg A(x,y) \lor B(x,y), \alpha[x,y \mapsto d,e])\}\} \\
    \equiv &\min\{\min\{\max\{TV(\neg A(x,y), \alpha[x,y \mapsto d,e]), TV(B(x,y), \alpha[x,y \mapsto d,e])\}\}\} \\
    \equiv &\min\{\min\{\max\{1 - TV(A(x,y), \alpha[x,y \mapsto d,e]), TV(B(x,y), \alpha[x,y \mapsto d,e])\}\}\} \\
    TV(A(x,y), \alpha) \equiv &TV((P(x,y) \land (P(x,c) \lor Q(x,c))), \alpha) \\
    \equiv &\min\{TV(P(x,y), \alpha), TV((P(x,c) \lor Q(x,c)), \alpha)\} \\
    \equiv &\min\{TV(P(x,y), \alpha), \max\{TV(P(x,c), \alpha), TV(Q(x,c), \alpha)\}\} \\
    TV(B(x,y), \alpha) \equiv &TV((P(c, f(x,y)) \lor Q(c, f(x,y))), \alpha) \\
    \equiv &\max\{TV(P(c, f(x,y)), \alpha), TV(Q(c, f(x,y)), \alpha)\} \\
\end{align}
$$
When $d = -100$ and $y = 1$:
$$
\begin{align}
    TV(A(x,y), \alpha[x,y \mapsto -100, 1])
    \equiv &\min\{TV(P(x,y), \alpha), \max\{TV(P(x,c), \alpha), TV(Q(x,c), \alpha)\}\} \\
    \equiv &\min\{1, \max\{1,0\}\} \\
    \equiv &\min\{1, 1\} \equiv 1 \\
    TV(B(x,y), \alpha[x,y \mapsto -100, 1])
    \equiv &\max\{TV(P(c, f(x,y)), \alpha), TV(Q(c, f(x,y)), \alpha)\} \\
    \equiv &\max\{TV(P(c, -100 + 1), \alpha), TV(Q(c, -100 + 1), \alpha)\} \\
    \equiv &\max\{0, 0\} \equiv 0 \\
\end{align}
$$
Therefore
$$
\begin{align}
&TV(\forall x \forall y G, \alpha[x,y \mapsto -100,1]) \\
\equiv &\min\{\min\{\max\{1 - TV(A(x,y), \alpha[x,y \mapsto -100,1]), TV(B(x,y), \alpha[x,y \mapsto -100,1])\}\}\} \\
\equiv &\min\{\min\{\max\{1 - 1, 0\}\}\} \\
\equiv &\min\{\min\{\max\{0, 0\}\}\} \\
\equiv &0
\end{align}
$$
Hence, $TV(\forall x \forall y G, \alpha) = 0$.

<img src='https://i.loli.net/2020/12/09/CgOXQFfYbZIlWJc.png' alt='CgOXQFfYbZIlWJc'/>
$$
\begin{align}
	&(\forall x Q(x) \rightarrow \exists z \forall y R(z,y)) \\
	\equiv &(\neg \forall x Q(x) \lor \exists z \forall y R(z,y)) \qquad &\text{definition of $\rightarrow$}\\
	\equiv &(\exist x Q(x) \lor \exist z \forall y R(z,y)) \qquad &\text{Q.Negation} \\
	\equiv &\exist x(Q(x) \lor \exist z \forall y R(z,y)) \qquad &\text{Q.Extraction} \\
	\equiv &\exist x(\exist z \forall y R(z,y) \lor Q(x)) \qquad &\text{association} \\
	\equiv &\exist x \exist z (\forall y R(z,y) \lor Q(x)) \qquad &\text{Q.Extraction} \\
	\equiv &\exist x \exist z \forall y(R(z,y) \lor Q(x)) \qquad &\text{Q.Extraction} \\
\end{align}
$$

<img src='https://i.loli.net/2020/12/09/i2MuGs3rqpt6FRQ.png' alt='i2MuGs3rqpt6FRQ'/>

| Line | Assumptions | Formula             | Justification            | References |
| ---- | ----------- | ------------------- | ------------------------ | ---------- |
| 1    | 1           | ∃x(P(x,x)∧∀yQ(x,y)) | Assumption Introduction  |            |
| 2    | 2           | (P(a,a)∧∀yQ(a,y))   | Assumption Introduction  |            |
| 3    | 2           | P(a,a)              | Conjunction Elimination  | 2          |
| 4    | 2           | ∃yP(a,y)            | Existential Introduction | 3          |
| 5    | 2           | ∀yQ(a,y)            | Conjunction Elimination  | 2          |
| 6    | 2           | Q(a,a)              | Universal Elimination    | 5          |
| 7    | 2           | (∃yP(a,y)∧Q(a,a))   | Conjunction Introduction | 4, 6       |
| 8    | 2           | ∃x(∃yP(x,y)∧Q(x,x)) | Existential Introduction | 7          |
| 9    | 1           | ∃x(∃yP(x,y)∧Q(x,x)) | Existential Elimination  | 1, 2, 8    |

<p style="page-break-after: always;"></p >

# Question 3

<img src='https://i.loli.net/2020/12/09/L3xfAFGOS8hsy4a.png' alt='L3xfAFGOS8hsy4a'/>

<img src='https://i.loli.net/2020/12/08/O174BoSZG6HqAdW.png' alt='O174BoSZG6HqAdW' width="80%"/>

This DFA is correct as whenever there is contiguous a or b, it will goes to the dead state.

<img src='https://i.loli.net/2020/12/09/eIVgn4v7OzuAyk5.png' alt='eIVgn4v7OzuAyk5'/>

<img src='https://i.loli.net/2020/12/11/jJVnIFQPRAkLoGh.png' alt='jJVnIFQPRAkLoGh'/>

<img src='https://i.loli.net/2020/12/09/xMlZwpieJIKdCmr.png' alt='xMlZwpieJIKdCmr'/>

Only epsilon-closure of $q_2$ has $q_2, q_4$, epsilon-closure of other states are themselves.

| state     | repr | a       | repr(a) | b         | repr(b) |
| --------- | ---- | ------- | ------- | --------- | ------- |
| 0         | A    | 0       | A       | 0,1       | B       |
| 0,1       | B    | 0,3     | C       | 0,1,2     | D       |
| 0,3       | C    | 0       | A       | `0,1,4 `  | `E`     |
| 0,1,2     | D    | 0,3     | C       | 0,1,2     | D       |
| `0,1,4`   | `E`  | `0,3,4` | `F`     | `0,1,2,4` | `G`     |
| `0,3,4`   | `F`  | `0,4`   | `H`     | `0,1,4`   | `E`     |
| `0,1,2,4` | `G`  | `0,3,4` | `F`     | `0,1,2,4` | `G`     |
| `0,4`     | `H`  | `0,4`   | `H`     | `0,1,4`   | `E`     |

Hence,  the equivaent DFA M' = (Q', $\Sigma$, $\delta$, A, F'), where Q' = {A, B, C, D, E, F, G, H} and F' = {E, F, G, H}, with transition function shown below.

| state | a    | b    |
| ----- | ---- | ---- |
| A     | A    | B    |
| B     | C    | D    |
| C     | A    | `E`  |
| D     | C    | D    |
| `E`   | `F`  | `G`  |
| `F`   | `H`  | `E`  |
| `G`   | `F`  | `G`  |
| `H`   | `H`  | `E`  |

<img src='https://i.loli.net/2020/12/09/wdzPBa1iYgfZpjQ.png' alt='wdzPBa1iYgfZpjQ'/>

There exits a NFA M = $(\Sigma, Q, q_0, F, \delta)$ that recognises the paths of G, where:

-   Introduce alphabet $\Sigma = V$
-   Introduce state $q_i \in Q \cup \{q_0, q_{error}\}$, for each vertice $v_i \in V$
-   Introduce start state $q_0$.
-   Introduce final state $q_i \in F$, for every vertice with label $v_k$ in sequence of vertices.
-   Introduce transition function $\delta(w, v) =$
    -   $v$, if $(w,v) \in E$
    -   $v_0$, if $w = q_0$
    -   $q_{error}$, otherwise

Then convert this NFA M to GNFA M' and repeatly eliminate intermediate state $q_{elim}$ between $q_i$ and $q_j$, using $(R_1R_2^*R_3 \cup R_4)$. This will eventually gives us a regular expression. Hence set of paths of G is a regular language over alphabet V.

<img src='https://i.loli.net/2020/12/09/DK3G5eAPaJrcWlY.png' alt='DK3G5eAPaJrcWlY'/>

$ neg(u)$ is also regular as it can be constructed by

-   replacing every terminal 0 in original with 1 and vice versa.
-   replace $\delta(v, 0) = w$ in original to $\delta(v,1) = w$ and vice versa.

So the same sequence of DFA also accepts $neg(u)$, and vice versa.

<img src='https://i.loli.net/2020/12/09/JcySZPXLzpf5sN4.png' alt='JcySZPXLzpf5sN4'/>

This is because mis-matching parentheses is not reuglar, which can also display as $L = \{p^im^j: i \geq j\}$, because p can represent left parenthese and m can represent right parenthese.

-   Assume there is a DFA $M$ that recognises $L = \{p^im^j: i \geq j\}$.

-   Write $f(w)$ for the state that M reaches after reading input $w$.

-   By Pigeonhole Principle, there exists $x < y$ such that $f(p^x) = f(p^y)$.

-   But $p^ym^y \in L$ means that the path from state $f(p^y)$ labeled $m^y$ ends in a final state.

-   So there is a path from the initial state to a final state labeled $p^xm^y$. so $p^xm^y$ is accepted by M.

-   But since $x \not \geq y$ (in fact $x < y$), so M accepts a word not in $L$

-   This contradicts the assumption that M recognises $L$, thus $L$ is not regular.

<p style="page-break-after: always;"></p >

# Question 4

<img src='https://i.loli.net/2020/12/09/JKGYqWMwPmXOUEa.png' alt='JKGYqWMwPmXOUEa'/>

Language generated is $L = \{a,b\}^*, where |L| \geq 2$.

This language is ambiguous as it has string ababaa which has two leftmost derivation.
$$
\begin{align}
&S \rightarrow AA \rightarrow aAAA \rightarrow abAAA \rightarrow abaAA \rightarrow ababAA \rightarrow ababaA \rightarrow ababbaa \\
&S \rightarrow AA \rightarrow AAAA \rightarrow aAAA \rightarrow abAAA \rightarrow abaAA \rightarrow ababAA \rightarrow ababaA \rightarrow ababaa
\end{align}
$$
Convert it into CNF

-   START
    $$
    \begin{align}
    	&S \rightarrow  AA \\
    	&A \rightarrow AAA | a | bA | Ab
    \end{align}
    $$

-   TERM
    $$
    \begin{align}
    	&S \rightarrow  AA \\
    	&A \rightarrow AAA | a | N_bA | AN_b \\
    	&N_b \rightarrow b \\
    \end{align}
    $$

-   BIN
    $$
    \begin{align}
    	&S \rightarrow  AA \\
    	&A \rightarrow AA_1 | a | N_bA | AN_b \\
    	&A_1 \rightarrow AA \\
    	&N_b \rightarrow b \\
    \end{align}
    $$

-   DEL
    $$
    \begin{align}
    	&S \rightarrow  AA \\
    	&A \rightarrow AA_1 | a | N_bA | AN_b \\
    	&A_1 \rightarrow AA \\
    	&N_b \rightarrow b \\
    \end{align}
    $$

-   UNIT
    $$
    \begin{align}
    	&S \rightarrow  AA \\
    	&A \rightarrow AA_1 | a | N_bA | AN_b \\
    	&A_1 \rightarrow AA \\
    	&N_b \rightarrow b \\
    \end{align}
    $$


    | S, A, $A_1$ |          |      |       |
    | ----------- | -------- | ---- | ----- |
    | A           | S        |      |       |
    | A           | S, $A_1$ | A    |       |
    | $N_b$       | A        | A    | $N_b$ |
    | b           | a        | a    | b     |

So, baab is accepted.

<img src='https://i.loli.net/2020/12/09/6lYtawnZskALzgT.png' alt='6lYtawnZskALzgT'/>

For every regular language, there is an ambiguous context-free grammar that generates it.

Let L be a regular language. Then there exists a DFA *M* = $(\Sigma, Q, q_0, F, \delta)$ that recognises it. We construct a CFG from *M* as follows:

-   Introduce a variable $V_i \in V$, for each state $q_i \in Q$
-   Introduce rule $V_i \rightarrow cV_j$, for each $\delta(q_i, c) = q_j$
-   Introduce rule $V_i \rightarrow \epsilon$, for each $q_i \in F$
-   Let $V_i$ be the start variable, where $q_i$ is the start state of the DFA.

First, this grammar is unambiguous. This is becuase

-   DFA has one transition from each state for each terminal, e.g. $V_i \rightarrow \epsilon$
-   Each rule generates at most one variable, e.g. $V_i \rightarrow cV_j$
-   Inductively, all parse trees generated by this grammar are binary trees where the left child is always a terminal (except the final leaf $\epsilon$)
-   There is never more than one way to generate the next terminal

Second, this grammar generates L.This is because

-   If string S is in the language, then there is a path in DFA from the start state to a final state
-   The path maps directly to a derivation, i.e. each transition on the path corresponds to a usage of a rule from this grammar, generating the input symbol followed by the variable corresponding to the next state (i.e. $\delta(q_i,c) = q_j$)
-   Because the path ends in a final state, the remaining variable has $V_i \rightarrow \epsilon$ rule

<img src='https://i.loli.net/2020/12/09/hxfw4iAgoCjp27T.png' alt='hxfw4iAgoCjp27T'/>

$L = \{u\#v: u,v \in \{a,b\}^*, |u| = |v|, reverse(u_ \neq v \}$

The gramma $G = (V, \Sigma, R, S)$, where $V = \{S, T\}$, $\Sigma = \{a,b\}$ and R is
$$
\begin{align}
	&S \rightarrow aSa | bSb | aSb | bSa | aTb | bTa \\
	&T \rightarrow aTa | aTb | bTa | bTb | \#
\end{align}
$$
First,  we show that G only generates strings in L.

-   The rules $S \rightarrow aSa | bSb | aSb | bSa | aTb | bTa$, which rewrite S until S is removed from the intermediate string of the form $uaTbv$ or $ubTav$, where $|u| = |v|$.
-   The rules $T \rightarrow aTa | aTb | bTa | bTb | \#$, will generate the form $x\#y$, where $|x| = |y|$.

Applying those rules in any order we get the derivation is strings S of the form $uax\#ybv$ and $ubx\#yav$, where $|u| = |v|$ and $|x| = |y|$, where $S \in L$

Second, we show that G generates all strings in L.

-   A string s is in L if and only if (i.e. exactly when) it can be written as $uax\#ybv$ or $ubx\#yav$ for some u, v, x, y with $|u| =|v|$ and $|x| = |y|$ (to see this simply let $uk$ be the shortest preﬁx of s such that
    -   $k \in \{a,b\}$ and
    -   the reverse of uk is not a suﬃx of s.

-   But we have seen that each such string is generated by G.

# Question 5

<img src='https://i.loli.net/2020/12/09/Gm9CbgkI6lporTL.png' alt='Gm9CbgkI6lporTL'/>

Yes, every finite language is decidable. Because finite language L is regular language. There exists a string w, if $w \in L$, DFA will accepts w; if $w \not \in L$, DFA will rejects w.

<img src='https://i.loli.net/2020/12/09/BZbSzajchQq1wFW.png' alt='BZbSzajchQq1wFW'/>

>   The question is asking if you can build a TM that is a ddecider and recognises the set of strings of the form <G> where <G> is the string encodding a CFG G.

Yes, context-free grammars are Turning decidable. Since context-free grammar can be converted in CNF and to have the Turning machine implements the CYK algorithm.

<img src='https://i.loli.net/2020/12/09/3bTwKHqhQVoyrzB.png' alt='3bTwKHqhQVoyrzB'/>

>   If true, you should explain why (e.g. give a construction of a TM that recognises the intersection)
>   If false you should explain why (e.g. give examples that show it is false).

Yes, intersection of a recognisable language and a decidable language is recognisable. Let $L_1 = \Sigma^*$ be language that is **decided**  by TMs $M_1$ and $L_2 = L_{HALT}$ be language that is **recognised** by TMs $M_2$. Then $L_1 \cap L_2 = L_2$, which is not decidable, but recognisable.

Therefore on input x:

1.  Run $M_1$ and $M_2$ in parallel on x.
2.  Accept. if both $M_1$ and $M_2$ accepts.

<img src='https://i.loli.net/2020/12/09/6y9LJ1cMtxbovfP.png' alt='6y9LJ1cMtxbovfP'/>
$$
\begin{align}
&(\lambda p.p(\lambda xy.x))((\lambda xyz.zxy)ab) \\
\stackrel{\beta}{\rightarrow} &(\lambda p.p(\lambda xy.x))((\lambda yz.zay)b) \quad &x = x, M = zxy, N = ab \\
\stackrel{\beta}{\rightarrow} &(\lambda p.p(\lambda xy.x))(\lambda z.zab)) \quad &x = y, M = zay, N = b \\
\stackrel{\beta}{\rightarrow} &(\lambda z.zab)(\lambda xy.x) \quad &x = p, M = p, N = (\lambda z.zab) \\
\stackrel{\beta}{\rightarrow} &(\lambda xy.x)ab \quad &x = z, M = zab, N = (\lambda xy.x) \\
\stackrel{\beta}{\rightarrow} &(\lambda y.a)b \quad &x = x, M = x, N = a \\
\stackrel{\beta}{\rightarrow} &a \quad &x = y, M = a, N = b \\
\end{align}
$$
