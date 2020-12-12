---
layout:     post
title:      Natural Deduction Proof
date:       2020-12-18
summary:    Some useful natural deduction proofs
categories: Logic Natural Deduction
---

- [$$F \equiv G$$ Propositional Logic](#f-equiv-g-propositional-logic)
  - [Idempotent](#idempotent)
  - [Commutative](#commutative)
  - [Associative](#associative)
  - [Distributive](#distributive)
  - [de Morgan's Laws](#de-morgans-laws)
  - [Double Negation](#double-negation)
  - [Implication Definition](#implication-definition)
  - [Transposition](#transposition)
  - [Exportation](#exportation)
- [$$F \vdash G$$ Propositional Logic](#f-vdash-g-propositional-logic)
  - [Trivial Proof](#trivial-proof)
  - [Modus Tollens](#modus-tollens)
  - [Hypothetical Syllogism](#hypothetical-syllogism)
  - [Disjunctive Syllogism](#disjunctive-syllogism)
  - [Construction Dilemma](#construction-dilemma)
  - [Destructive Dilemma](#destructive-dilemma)
- [$$F \equiv G$$ Predicate Logic](#f-equiv-g-predicate-logic)
  - [Trivial Proof](#trivial-proof-1)
  - [Qualifier Negation](#qualifier-negation)
  - [Qualifier Unification](#qualifier-unification)
  - [Qualifier Transposition](#qualifier-transposition)

# $$F \equiv G$$ Propositional Logic

## Idempotent

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

## Commutative

<mark>$$$$</mark>

## Associative

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

## Distributive

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

## de Morgan's Laws

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

## Double Negation

<mark>$$$$</mark>

<mark>$$$$</mark>

## Implication Definition

<mark>$$$$</mark>

<mark>$$$$</mark>

## Transposition

<mark>$$$$</mark>

## Exportation

<mark>$$$$</mark>

# $$F \vdash G$$ Propositional Logic

## Trivial Proof

<span class="bg-yellow white" style="text-align: center; font-size:18px">$$B \vdash (A \rightarrow B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$B$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 1,2 | $$(A \land B)$$ | $$ \land $$I | 1,2 |
| 4 | 1,2 | $$B$$ | $$ \land $$E | 3 |
| 5 | 1 | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 2,4 |

<mark>$$\neg A \vdash (A \rightarrow B)$$</mark>

| Line | Assumptions | Formula             | Justification    | References |
| ---- | ----------- | ------------------- | ---------------- | ---------- |
| 1    | 1           | $$ \neg A$$           | Assump. I        |            |
| 2    | 2           | $$A$$                | Assump. I        |            |
| 3    | 1,2         | $$ \bot $$            | $$ \neg $$E        | 1,2        |
| 4    | 1,2         | $$B$$                 | $$ \bot $$         | 3          |
| 5    | 1           | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 2,4        |

<mark>$$A \vdash (\neg A \rightarrow B)$$</mark>

| Line | Assumptions | Formula                   | Justification    | References |
| ---- | ----------- | ------------------------- | ---------------- | ---------- |
| 1    | 1           | $$A$$                       | Assump. I        |            |
| 2    | 2           | $$ \neg A$$                 | Assump. I        |            |
| 3    | 1,2         | $$ \bot $$                  | $$ \neg $$E        | 1,2        |
| 4    | 1,2         | $$B$$                       | $$ \bot $$         | 3          |
| 5    | 1           | $$( \neg A \rightarrow B)$$ | $$ \rightarrow $$I | 2,4        |

<mark>$$(A \rightarrow (B \rightarrow C)) \vdash (B \rightarrow (A \rightarrow C))$$</mark>

| Line | Assumptions | Formula                             | Justification    | References |
| ---- | ----------- | ----------------------------------- | ---------------- | ---------- |
| 1    | 1           | $$(A \rightarrow (B \rightarrow C))$$ | Assump. I        |            |
| 2    | 2           | $$A$$                                 | Assump. I        |            |
| 3    | 1,2         | $$(B \rightarrow C)$$                 | $$ \rightarrow $$E | 1,2        |
| 4    | 3           | $$B$$                                 | Assump. I        |            |
| 5    | 1,2,3       | $$C$$                                 | $$ \rightarrow $$E | 3,4        |
| 6    | 1,3         | $$(A \rightarrow C)$$                 | $$ \rightarrow $$I | 2,5        |
| 7    | 1           | $$(B \rightarrow (A \rightarrow C))$$ | $$ \rightarrow $$I | 4,6        |

<mark>$$\neg(A \lor B) \vdash \neg A$$</mark>

| Line | Assumptions | Formula            | Justification | References |
| ---- | ----------- | ------------------ | ------------- | ---------- |
| 1    | 1           | $$ \neg (A \lor B)$$ | Assump. I     |            |
| 2    | 2           | $$A$$                | Assump. I     |            |
| 3    | 2           | $$(A \lor B)$$       | $$ \lor $$I     | 2          |
| 4    | 1,2         | $$ \bot $$                  | $$ \neg $$E     | 1,3        |
| 5    | 1           | $$ \neg A$$          | $$ \neg $$I     | 2,4        |

<mark>$$\vdash (A \lor \neg A)$$</mark>

| Line | Assumptions | Formula                  | Justification | References |
| ---- | ----------- | ------------------------ | ------------- | ---------- |
| 1    | 1           | $$ \neg (A \lor  \neg A)$$ | Assump. I     |            |
| 2    | 2           | $$A$$                     | Assump. I     |            |
| 3    | 2           | $$(A \lor  \neg A)$$       | $$ \lor $$I     | 2          |
| 4    | 1,2         | $$ \bot $$                 | $$ \neg $$E     | 1,3        |
| 5    | 1           | $$ \neg A$$                | $$ \neg $$I     | 2,4        |
| 6    | 1           | $$(A \lor  \neg A)$$       | $$ \lor $$I     | 5          |
| 7    | 1           | $$ \bot $$                 | $$ \neg $$E     | 1,6        |
| 8    |             | $$(A \lor  \neg A)$$       | RA            | 1,7        |

## Modus Tollens

<mark>$$$$</mark>

## Hypothetical Syllogism

<mark>$$$$</mark>

## Disjunctive Syllogism

<mark>$$$$</mark>

## Construction Dilemma

<mark>$$$$</mark>

## Destructive Dilemma

<mark>$$$$</mark>

# $$F \equiv G$$ Predicate Logic

## Trivial Proof

<mark>$$\forall xF(x) \vdash \exists x F(x)$$</mark>

| Line | Assumptions | Formula          | Justification | References |
| ---- | ----------- | ---------------- | ------------- | ---------- |
| 1    | 1           | $ \forall xF(x)$ | Assump. I     |            |
| 2    | 1           | $F(c)$           | $ \forall $E  | 1          |
| 3    | 1           | $ \exists xF(x)$ | $ \exists $I  | 2          |

<mark>$$\exists x \forall y F(x,y) \vdash \forall x \exists y F(x,y)$$</mark>

| Line | Assumptions | Formula                      | Justification | References |
| ---- | ----------- | ---------------------------- | ------------- | ---------- |
| 1    | 1           | $$ \exists y \forall xF(x,y)$$ | Assump. I     |            |
| 2    | 2           | $$ \forall xF(x,c)$$           | Assump. I     |            |
| 3    | 2           | $$F(d,c)$$                     | $$ \forall $$E  | 2          |
| 4    | 2           | $$ \exists yF(d,y)$$           | $$ \exists $$I  | 3          |
| 5    | 2           | $$ \forall x \exists yF(x,y)$$ | $$ \forall $$I  | 4          |
| 6    | 1           | $$ \forall x \exists yF(x,y)$$ | $$ \exists $$E  | 1,2,5      |

## Qualifier Negation

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

## Qualifier Unification

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

<mark>$$$$</mark>

## Qualifier Transposition

<mark>$$$$</mark>

<mark>$$$$</mark>



