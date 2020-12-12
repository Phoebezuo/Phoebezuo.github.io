---
layout:     post
title:      Summary Notes for Models of Computation
date:       2020-12-12
summary:    Summary Notes for Models of Computation
categories: Computation Logic DFA RegEx
---

- [Propositional Logic](#propositional-logic)
- [Predicate Logic](#predicate-logic)
- [Regular Languages](#regular-languages)
- [Context-free Languages](#context-free-languages)
- [Universal Models of Computation](#universal-models-of-computation)
- [Useful Tools](#useful-tools)


# Propositional Logic

1.  The truth value of $$(F \land G)$$ under assignment  $$\alpha$$ is equal to the **maximum** of the truth value of F under $$\alpha$$ and the truth value of G under $$\alpha$$.

    False, $$tv((F \land G), \alpha) = \min\{tv(F,\alpha), tv(G, \alpha)\}$$

2.  Let F be the propositional formula $$(p \rightarrow q)$$, and let G be the propositional formula $$(q \rightarrow p)$$. Why is F not a logical consequence of G (i.e. $$G \vDash F$$)?

    when p = 1, q = 0, $$F (1 \rightarrow 0) = 0, G = (0 \rightarrow 1) = 1$$

3.  If $$(F \land \neg G)$$ is statisfiable,  then G is not a logical consequence of F.

    True, if $$(F \land \neg G)$$ is statisfiable, it means there exist an assignment to make $$tv(F \land \neg G) = 1$$, i.e. F = 1 and G = 0. However, for $$G$$ to be a logical consequence of $$F$$, every assignment that makes $$F$$ true should make $$G$$ true. So $$G$$ is not a logical consequence of $$F$$.

4.  Compute $$tv((F \rightarrow G), \alpha)$$ and $$tv((F \leftrightarrow G), \alpha)$$
    $$
    \begin{align}
    tv((F \rightarrow G), \alpha) &= tv((\neg F \lor G), \alpha) \\
    &= max\{tv(\neg F, \alpha), tv(G, \alpha)\} \\
    &= max\{1 - tv(F, \alpha), tv(G, \alpha)\} \\
    tv((F \leftrightarrow G), \alpha) &= tv(((F \rightarrow G) \land (G \rightarrow F)), \alpha) \\
    &= min\{tv((F \rightarrow G), \alpha), tv((G \rightarrow F), \alpha)\} \\
    &= min\{max\{1 - tv(F, \alpha), tv(G, \alpha)\}, max\{1 - tv(G, \alpha), tv(F, \alpha)\}\} \\
    &= 1 - |tv(F, \alpha) - tv(G, \alpha)|
    \end{align}
    $$

5.  How to show that F is not a logical consequence of $$\{E_1, ..., E_k\}$$?

    F is not a logical consequence if it is in the following sitution

    -   For propositional logcial formulas, there is an assignment $$\alpha$$ such that $$\alpha(E_i) = 1$$ and $$\alpha(F) = 0$$
    -   For predicate logical formula, there is a structure $$\mathbb{A}$$ and an assignment $$\alpha$$ such that truth-value of E under $$\mathbb{A}$$ and $$\alpha$$ is 1 while the truth-value of F under $$\mathbb{A}$$ and $$\alpha$$ is 0.

    In both case, you should find specific concrete formula E, F with these properties.

6.  What is the difference and relation between $$(F \leftrightarrow G)$$ and $$F \equiv G$$?
    -   dfifference
        -   $$(F \leftrightarrow G)$$ is a formula of propositional logic
        -   $$F \equiv G$$ is a statement about formula of propositional logic
    -   relation: $$F = G$$ iff $$(F \leftrightarrow G)$$ is valid

7.  Argu why $$\bot \vDash F$$ for every propositional formula F.

    $$A \vDash B$$ is defined as meaning that under all assignments $$\alpha$$, if $$tv(A, \alpha) = 1$$, then $$tv(B, \alpha) = 1$$. Since $$tv(\bot, \alpha) = 0$$ for all assignments, the statement $$\bot \vDash F$$ is absolutely true (i.e. no assignments can make $\bot$ true)

# Predicate Logic

1.  When are two **formulas** of predicate logic logically equivalent? Pick all true statements

    1.  if in every structure under every assignment, the truth values of the formulas agree. √
    2.  if in some structure under some assignment, the truth values of the formulas agree. X
    3.  if in every structure under some assignment, the truth values of the formulas agree. X

2.  When are two **sentences** of predicate logic logically equivalent? Pick all true statements.

    1.  if in every structure under every assignment, the truth values of the formulas agree. √
    2.  if in some structure under some assignment, the truth values of the formulas agree. X
    3.  if in every structure under some assignment, the truth values of the formulas agree. √

    This is because the truth value of a sentence does not depends on the variable assignment. X

3.  **Notes**: $\exist x\forall yF \vdash \forall y \exist x F$, but $\forall x \exist y F \not\vdash \exist x \forall yF$.

4.  For formula $F = (\forall x (P(x,z) \land \exist y Q(y)) \rightarrow P(y,z))$ and term $t = f(x,y)$

    **Notes: ** For $F[x/a]$, and $ a = x + y$, If no free occurrence of a is the scope of qualifiers of x and y (since $a = x + y$), then it can replace.

    1.  write $F[t/y]$ and say whether t is free to replace y in F

        -   Since no free occurrence of y in the scope of qualifiers of $\forall x$ and $\exist y$, so y can be replaced.

        -   It can replaced any free occurrence of y outside the scope of qualifiers of $\forall x$ and $\exist y$, so $F = (\forall x (P(x,z) \land \exist y Q(y)) \rightarrow P(\textcolor{red}{f(x,y)},z))$,

    2.  write $F[t/z]$ and say whether z is free to replace y in F

        -   It cannot replace, a free occurrence of z is in the scope of qualifiers of x and y

    3.  write $F[t/x]$ and say whether x is free to replace y in F

        -   Since no free occurrence of y in the scope of qualifiers of $\forall x$ and $\exist y$, so x can be replace.
        -   However there is no free occurrence of x outside the scope of qualifiers of $\forall x$ and $\exist y$, so $F = (\forall x (P(x,z) \land \exist y Q(y)) \rightarrow P(y,z))$, which is unchanged.

5.  Prove that $(\exists x P(x) \land F)$ is not valid.

    There is a structure $\mathbb{A}$, such that predicate $P^{\mathbb{A}}$ is an empty set. Thus $tv(P, \alpha) = 0$ under any assignment, so $(\exist x P(x) \land F)$  under structure $\mathbb{A}$ is false, i.e. not valid.

# Regular Languages

1.  **Notes**: the empty set $\empty$ and $\{\epsilon \}$ is a language over alphabet $\Sigma = \{a, b\}$, but empty string $\epsilon$ is not.

2.  Which is not the languages over alphabet $\{a,b\}$?
    -   $\{a,b,c\}$ X because c is not in the $\Sigma$
    -   $\empty$ √
    -   $\{\epsilon\}$ √
    -   $(ab)^*$ X because language is the set of strings over $\Sigma$, however $(ab)^*$ is infinite.

3.  Draw a DFA that recognise $L = \{w | w  \text{ begins with ab and ends with ba}\}$

    <img src='https://i.loli.net/2020/12/10/IKr6YB9Eozmtw2p.png' alt='IKr6YB9Eozmtw2p' width="50%"/>

4.  Draw a DFA that recognise $L = \{w | \text{ either number of a in w is divisible by 3 or w begins with bbb}\}$

    <img src='https://i.loli.net/2020/12/10/QkbXxoORJ9hIpg3.png' alt='QkbXxoORJ9hIpg3' width="50%"/>

5.  Draw a DFA that recognise $L = \{w | \text{ number of a in w $=3k + 1, k \in \mathbb{Z}$ and number of b in w is odd}\}$

    <img src='https://i.loli.net/2020/12/10/NbqlP1QCXZvtcUD.png' alt='NbqlP1QCXZvtcUD' width="50%"/>

6.  Draw a DFA that recognise $L = \{w | \text{ number of a in w is even or |w| is even}\}$

    <img src='https://i.loli.net/2020/12/10/yos3J6pQn1kg9Lf.png' alt='yos3J6pQn1kg9Lf' width="50%"/>

7.  Draw a DFA that recognise $L = \{w | \text{w contains exactly one occurrence of substring aaa}\}$

    <img src='https://i.loli.net/2020/12/10/Hao3i5cgJMRrAdN.png' alt='Hao3i5cgJMRrAdN' width="50%"/>

8.  Draw a DFA that recognise $L = \{w | \text{ occurrence of substring bcd is even}\}$

    <img src='https://i.loli.net/2020/12/10/DKxIJow2VihU14T.png' alt='DKxIJow2VihU14T' width="50%"/>

9.  Let $\Sigma = \{0,1\}$, write regular expression over $\Sigma$ for the following languages
    1.  The set of strings whose number of 0's is a multiple of three.

        $(1^*01^*01^*01^*)^*$, try to find a string that contain only 3 0's first, then take the Kleen star for multiples.

    2.  The set of strings with at most one pair of consecutive 1's

        $(0 \cup 10)^*(11\cup1\cup\epsilon)(0\cup01)^*$, find a string that contain no pairs of consecutive 1's first, then add  a pair of consecutive 1's

    3.  The set of string not containing 101 as a substring

        $0^*(1\cup000^*)^*0^*$, in order to not have 101 as a substring, the string must be

        -   two 1's is next to each other
        -   more than 2 0's between two 1's

10.  Prove that every finite language $\{s_1, s_2,..., s_3\}$ is the language of some regular expression

     For every string $s = a_1a_2...a_k \in \Sigma^*$, we have $L(a_1 \cdot a_2 \cdot a_3 ...a_k) = \{s\}$, i.e. $L(s) = \{s\}$. Thus the language $\{s_1, s_2, s_3, ..., s_n\}$ is the language of the regular expression $s_1 \cup s_2 \cup ... \cup s_n$.

11.  If $R^k$ is a regular expression whose language is $\overbrace{L(R) \cdot L(R) \cdots L(R)}^{k}$. Give a recursive definition of $L(R^k)$.

     Define $L(R^0) = \{\epsilon\}$, and for $k \geq 1$, define $L(R^k) = L(R^{k-1})\cdot L(R)$.

12.  Draw a DFA that recognise $L = \{w | \text{ w contains equal number of occurrences of substring 01 and 10}\}$

     <img src='https://i.loli.net/2020/12/10/xntHUyNVQqMpjJ7.png' alt='xntHUyNVQqMpjJ7' width="50%"/>

13.  Let $N_1$, $N_2$ be NFAs.

     1.  Devise an algorithm for testing whether or not $L(N_1) = \empty$
         -   If the acceptstateis not in the connected component from the starting state, then $L(N_1) = \empty$
     2.  Devise an algoirthm for testing whether or not $L(N_1) \subseteq L(N_2)$
         -   If $L(N_1) \ L(N_2) = \empty$, then $L(N_1) \subseteq L(N_2)$

14.  What is the equivalent NFA with no $\epsilon$-transition of the following NFA?

     <img src='https://i.loli.net/2020/12/10/CP9F7iGonLB1vlV.png' alt='CP9F7iGonLB1vlV' width="40%"/>

     1.  Construct a table without $\epsilon$-transition
     2.  Construct NFA using the table

     <img src='https://i.loli.net/2020/12/10/kzcrJyoGhKbgAB5.png' alt='kzcrJyoGhKbgAB5' width="80%"/>

15.  Why does this construction of an NFA M recognising $L(M_1)^*$ given NFA $M_1$ not working?

     <img src='https://i.loli.net/2020/12/10/uyLwdT9Dkzb4rxq.png' alt='uyLwdT9Dkzb4rxq' width="40%"/>

     Suppose $L(M_1) = \{aa^{2k}b | k \geq 0\}$, if using this construction, it will accept aa, but $aa \not\in L(M_1)^*$.

     <img src='https://i.loli.net/2020/12/10/6aHCTAncdODLp5K.png' alt='6aHCTAncdODLp5K' width="80%"/>

16.  Construct a DFA that recognise $L = \{w | \text{x is number of 1's mod 3, y is number of 0's mod 3}, s.t. x \neq y\}$, then give the corresponding RegEx.

     -   Construct corresponding DFA and convert it to GNFA

         <img src='https://i.loli.net/2020/12/10/k8mRcoEUp7YJijs.png' alt='k8mRcoEUp7YJijs'/>

     -   remove $q_0$

         | index | transition                            | $R_1$      | $R_2$         | $R_3$ | $R_4$         | output      |
         | ----- | ------------------------------------- | ---------- | ------------- | ----- | ------------- | ----------- |
         | 1     | $A \rightarrow q_0 \rightarrow q_1$   | $\epsilon$ | $\varnothing$ | 0     | $\varnothing$ | 0           |
         | 2     | $A \rightarrow q_0 \rightarrow q_2$   | $\epsilon$ | $\varnothing$ | 1     | $\varnothing$ | 1           |
         | 3     | $q_1 \rightarrow q_0 \rightarrow q_1$ | 1          | $\varnothing$ | 0     | $\varnothing$ | 10          |
         | 4     | $q_1 \rightarrow q_0 \rightarrow q_2$ | 1          | $\varnothing$ | 1     | 0             | $11 \cup 0$ |
         | 5     | $q_2 \rightarrow q_0 \rightarrow q_1$ | 0          | $\varnothing$ | 0     | 1             | $00 \cup 1$ |
         | 6     | $q_2 \rightarrow q_0 \rightarrow q_2$ | 0          | $\varnothing$ | 1     | $\varnothing$ | $01$        |

         <img src='https://i.loli.net/2020/12/10/ceVT1bfI8dvJjQg.png' alt='ceVT1bfI8dvJjQg' width="50%"/>

     -   remove $q_1$

         | index | transition                            | $R_1$     | $R_2$ | $R_3$      | $R_4$         | output                           |
         | ----- | ------------------------------------- | --------- | ----- | ---------- | ------------- | -------------------------------- |
         | 1     | $A \rightarrow q_1 \rightarrow B$     | 0         | 10    | $\epsilon$ | $\varnothing$ | $0(10)^*$                        |
         | 2     | $A \rightarrow q_1 \rightarrow q_2$   | 0         | 10    | $11\cup0$  | 1             | $0(10)^*(11\cup0)\cup1$          |
         | 3     | $q_2 \rightarrow q_1 \rightarrow A$   | $00\cup1$ | 10    | $\epsilon$ | $\epsilon$    | $(00\cup1)(10)^*\cup \epsilon$   |
         | 4     | $q_2 \rightarrow q_1 \rightarrow q_2$ | $00\cup1$ | 10    | $11\cup0$  | 01            | $(00\cup1)(10)^*(11\cup0)\cup01$ |

         <img src='https://i.loli.net/2020/12/10/dSFgNiGsZcLe8AB.png' alt='dSFgNiGsZcLe8AB' width="50%"/>

     -   remove $q_2$
         $$
         \begin{align}
         R_1 &= 0(10)^*(11\cup0)\cup1 \\
         R_2 &= (00\cup1)(10)^*(11\cup0)\cup01\\
         R_3 &= (00\cup1)(10)^*\cup \epsilon \\
         R_4 &= 0(10)^*\\
         R_1R_2^*R_3\cup R_4 &= \textcolor{red}{0(10)^*(11\cup0)\cup1}\textcolor{blue}{((00\cup1)(10)^*(11\cup0)\cup01)^*}\textcolor{red}{(00\cup1)(10)^*\cup \epsilon}\cup \textcolor{blue}{0(10)^*}
         \end{align}
         $$

# Context-free Languages

1.  If a context-free grammar is unambiguous, then it is in Chomsky Normal Form. False
2.  Every grammar in Chomsky Normal Form is unambiguous. False
3.  If G, H are CFG in Chomsky Normal Form that does not generate the empty string, and if one applies the operation we saw in class to get a grammar G' generating $<option>$ , then G' is also in Chomsky Normal Form.
    1.  $L(G)^*$, True, since it only introdoce $S \rightarrow S_M S$
    2.  $L(G) \circ L(H)$, True, since it only introduce $S \rightarrow S_MS_N$
    3.  $L(G) \cup L(H)$, False, since it introduce $S \rightarrow S_M | S_N$, which can't be the form in CNF.
4.  What is the procedure of *DEL* step when converting a CFG G to a CNF, where G does not generate $\epsilon$?
    -   generate all $\epsilon$-rules, i.e. $A_i \rightarrow \epsilon$, add $A_i$ to set X
        -   for each variable $A_i$ in X:
            -   for each variable B that produce A, i.e. $B \rightarrow A$:
                -   add rule with A removed
        -   remove $\epsilon$-rule in A

# Universal Models of Computation

1.  Every regular language is Turning-decidable and recognisable. True

2.  Every context-free language is Turing-decidable, and every Turing-decidable language is Turing-recognisable.

    True, because $A_{CFG} = \{<G,w> | \text{G is a. CFG that generates w}\}$ is decidable.

3.  For every multi-tape TM M, there is a single-tape TM M' such that L(M) = L(M′). True

4.  One can prove that the acceptance-problem for Turing-machines is not decidable by assuming it is and reaching a contradiction. True

    Suppose $A_{TM}$ is decided by some TM H, so H accepts $<M, w>$ if TM M accepts w, and H rejects $<M, w>$ if TM M doesn't accept w.

    <img src='https://i.loli.net/2020/12/09/6QSb8wOieWJZMru.png' alt='6QSb8wOieWJZMru' width="50%"/>

    Define another TM D using H as a subroutine.

    <img src='https://i.loli.net/2020/12/09/jC74LloONiuXndf.png' alt='jC74LloONiuXndf' width="50%"/>

    So D takes as input any encoded TM $<M>$, then feeds $<M, <M>>$ as input into H, and finally outputs the opposite of what H outputs. Because D is a TM, we can feed $<D>$ as input into D.

    <img src='https://i.loli.net/2020/12/09/DHIlG9BCw4JUzSq.png' alt='DHIlG9BCw4JUzSq' width="50%"/>

    Note that D accepts $<D>$ iff D doesn't accept $<D>$, which is impossible. Thus, $A_{TM}$ must be undecidable.

5.  $(\lambda x.xx)ab$ has the normal form abab.

    False, this is because $(\lambda x .xx)ab \stackrel{\beta}{\rightarrow} (aa)b$, where input is x, output is xx, replace x in output with a.

6.  Prove that every regular language is Turning-decidable

    Construct TM $M = (Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$ to simulates a DFA $D = (Q, \Sigma, \delta, q_0, F)$ which recognise regular language L.

    -   $Q_{TM} = Q_{DFA} \cup \{q_{accept}, q_{reject}\}$
    -   $\Sigma_{TM} = \Sigma_{DFA}$
    -   $\Gamma = \Sigma_{TM} \cup \{\sqcup\}$

    -   For every $\delta(q,a)=a'$ in DFA, introduce a new transition in TM that maps $(q,a)$ to $(q', a,  R)$
    -   For every $q \in F$ in DFA, intdoduce a new transition in TM that maps $(q, \sqcup)$ to $(q_{accept}, \sqcup, R)$
    -   For every $q \not\in F$ in DFA,  intdoduce a new transition in TM that maps $(q, \sqcup)$ to $q_{reject}, \sqcup, R$

7.  Prove that every context-free language is Turning-decidable.

    Suppose languagee $A = \{<G, w> | \text{ G is a  CFG and } w \in L(G)\}$.

    -   Convert G to an equivalent grammar in CNF
    -   If length of w is 0, then list all derivations with 1 step
    -   If length of w is not 0, then list all derivations with $2n-1$ steps, where n is the length of w
    -   If any of these derivations generates w, accept; if not, reject.

8.  Compute $(((\lambda x.(\lambda x.(xy)))a)b)$
    $$
    \begin{align}
    (((\lambda x.\textcolor{red}{(\lambda x.(xy))})a)b) &\stackrel{\beta}{\rightarrow} ((\lambda z.(zy))b) \quad x = x, M = (\lambda x.(xy)), N = a \\
    &\stackrel{\beta}{\rightarrow} ((by)) \quad x = z, M = (zy), N = b \\
    \end{align}
    $$

9.  Compute $(((\lambda x.(xx))(\lambda x.x))x)$
    $$
    \begin{align}
    (((\lambda x.(xx))\textcolor{red}{(\lambda x.x)})x) &\stackrel{\beta}{\rightarrow} (((\lambda x.(xx))(\lambda x.x))x) \quad x = x, M = (xx), N = (\lambda x.x) \\
    &\stackrel{\alpha}{\rightarrow} (((\lambda y.\textcolor{red}{(yy)})(\lambda z.z))x) \\
    &\stackrel{\beta}{\rightarrow} (((\lambda z.z)(\lambda z.z))x) \quad x = y, M = (yy), N = (\lambda z.z) \\
    &\stackrel{\alpha}{\rightarrow} (((\lambda z.z)(\lambda a.a))x) \\
    &\stackrel{\beta}{\rightarrow} ((\lambda a.a)x) \quad x = z, M = z, N = (\lambda a.a) \\
    &\stackrel{\beta}{\rightarrow} x \quad x = a, M = a, N = x \\
    \end{align}
    $$

10.  If TRUE $= \lambda xy.x$, FALSE $=\lambda xy.y$ and NOT $=\lambda fxy.fyx$. Prove NOT TRUE = FALSE.
     $$
     \begin{align}
     &NOT \; TRUE \\
     = &(\lambda fxy.fyx)TRUE \\
     \stackrel{\beta}{\rightarrow} &\lambda xy.TRUEyx \quad x = f, M = fyx, N = TRUE \\
     = &\lambda xy.(\lambda xy.x)yx \\
     \stackrel{\alpha}{\rightarrow} &\lambda xy.(\lambda ab.a)yx \\
     \stackrel{\beta}{\rightarrow} &\lambda xy.(\lambda b.y)x \quad x = a, M =  a, N = y \\
     \stackrel{\beta}{\rightarrow} &\lambda xy.y \quad x = b, M =  y, N = x \\
     = &FALSE
     \end{align}
     $$

11.  If $L_1$ and $L_2$ are decidable, then $L_1 \cap L_2$ is decidable.

     <img src='https://i.loli.net/2020/12/11/D2KU3Xutl9M1Vmo.png' alt='D2KU3Xutl9M1Vmo' width="50%"/>

12.  If $L_1$ and $L_2$ are decidable, then $L_1 \cup L_2$ is decidable.

     <img src='https://i.loli.net/2020/12/11/65xmSnreZgTuDLB.png' alt='65xmSnreZgTuDLB' width="50%"/>

13.  If $L_1$ and $L_2$ are recognizable, then $L_1 \cap L_2$ is recognizable.

     <img src='https://i.loli.net/2020/12/11/xCsfoZvK1SJRNBm.png' alt='xCsfoZvK1SJRNBm' width="50%"/>

14.  If $L_1$ and $L_2$ are recognizable, then  $L_1 \cup L_2$ is recognizable.

     <img src='https://i.loli.net/2020/12/11/NnsrVf5DYdIFJ2h.png' alt='NnsrVf5DYdIFJ2h' width="50%"/>

15.  Prove that recognizable language is closed under concatenation.

     Let $L_1$ and $L_2$ be two recognizable language. Given an input w, use nondeterminism and guess a partition $w (w = xy)$. Now run the respective TM of $L_1$ and $L_2$ on x and y respectively. If both accepts then accept, else reject.

16.  Prove that recognizable language is closed under star.

     Nondeterministically first guess a number k, andthen guess a k partition of the given input. Now for each string in the partition, check whether it belongs to the original language.

# Useful Tools
- [Truth Table Generator](https://web.stanford.edu/class/cs103/tools/truth-table-tool/)
- [Natural Deduction Checker](https://github.com/Phoebezuo/Natural-Deduction-Checker)
- [Context-free Grammar Checker](https://web.stanford.edu/class/archive/cs/cs103/cs103.1156/tools/cfg/)
- [Regex to DFA Converter](https://cyberzhg.github.io/toolbox/nfa2dfa)
- [Context-free Grammar to Chomsky Normal From Converter](https://cyberzhg.github.io/toolbox/cfg2cnf)
- [CTK Table Generator](https://www.xarg.org/tools/cyk-algorithm/)
- [Turning Machine Simulator](https://turingmachinesimulator.com/)
