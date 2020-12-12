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

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$A \vdash(A \land A)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \land A) \vdash A$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$A \vdash (A \lor A)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor A) \vdash A$$</span>

## Commutative

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor B) \vdash (B \lor A)$$</span>

## Associative

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A\land (B\land C)) \vdash ((A\land B)\land C)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A\land B)\land C) \vdash (A\land (B\land C))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A\lor (B\lor C)) \vdash ((A\lor B)\lor C)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A\lor B)\lor C) \vdash (A\lor (B\lor C))$$</span>

## Distributive

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \land (B \lor C)) \vdash ((A \land B) \lor (A \land C))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \land B) \lor (A \land C)) \vdash (A \land (B \lor C))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor(B \land C)) \vdash ((A \lor B) \land (A \lor C))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \lor B) \land (A \lor C)) \vdash (A \lor(B \land C))$$</span>

## de Morgan's Laws

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg (A\land B) \vdash (\neg A\lor \neg B)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg A\land \neg B) \vdash \neg (A\lor B)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg (A\lor B) \vdash (\neg A\land \neg B)$$</span>

## Double Negation

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg \neg A \vdash A$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$A \vdash \neg \neg A$$</span>

## Implication Definition

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg A\lor B) \vdash (A \rightarrow B)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow B) \vdash (\neg A\lor B)$$</span>

## Transposition

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg B \rightarrow \neg A) \vdash (A \rightarrow B)$$</span>

## Exportation

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \land B) \rightarrow C) \vdash (A \rightarrow (B \rightarrow C))$$</span>

# $$F \vdash G$$ Propositional Logic

## Trivial Proof

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$B \vdash (A \rightarrow B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$B$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 1,2 | $$(A \land B)$$ | $$ \land $$I | 1,2 |
| 4 | 1,2 | $$B$$ | $$ \land $$E | 3 |
| 5 | 1 | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 2,4 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg A \vdash (A \rightarrow B)$$</span>

| Line | Assumptions | Formula             | Justification    | References |
| ---- | ----------- | ------------------- | ---------------- | ---------- |
| 1    | 1           | $$ \neg A$$           | Assump. I        |            |
| 2    | 2           | $$A$$                | Assump. I        |            |
| 3    | 1,2         | $$ \bot $$            | $$ \neg $$E        | 1,2        |
| 4    | 1,2         | $$B$$                 | $$ \bot $$         | 3          |
| 5    | 1           | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 2,4        |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$A \vdash (\neg A \rightarrow B)$$</span>

| Line | Assumptions | Formula                   | Justification    | References |
| ---- | ----------- | ------------------------- | ---------------- | ---------- |
| 1    | 1           | $$A$$                       | Assump. I        |            |
| 2    | 2           | $$ \neg A$$                 | Assump. I        |            |
| 3    | 1,2         | $$ \bot $$                  | $$ \neg $$E        | 1,2        |
| 4    | 1,2         | $$B$$                       | $$ \bot $$         | 3          |
| 5    | 1           | $$( \neg A \rightarrow B)$$ | $$ \rightarrow $$I | 2,4        |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow (B \rightarrow C)) \vdash (B \rightarrow (A \rightarrow C))$$</span>

| Line | Assumptions | Formula                             | Justification    | References |
| ---- | ----------- | ----------------------------------- | ---------------- | ---------- |
| 1    | 1           | $$(A \rightarrow (B \rightarrow C))$$ | Assump. I        |            |
| 2    | 2           | $$A$$                                 | Assump. I        |            |
| 3    | 1,2         | $$(B \rightarrow C)$$                 | $$ \rightarrow $$E | 1,2        |
| 4    | 3           | $$B$$                                 | Assump. I        |            |
| 5    | 1,2,3       | $$C$$                                 | $$ \rightarrow $$E | 3,4        |
| 6    | 1,3         | $$(A \rightarrow C)$$                 | $$ \rightarrow $$I | 2,5        |
| 7    | 1           | $$(B \rightarrow (A \rightarrow C))$$ | $$ \rightarrow $$I | 4,6        |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg(A \lor B) \vdash \neg A$$</span>

| Line | Assumptions | Formula            | Justification | References |
| ---- | ----------- | ------------------ | ------------- | ---------- |
| 1    | 1           | $$ \neg (A \lor B)$$ | Assump. I     |            |
| 2    | 2           | $$A$$                | Assump. I     |            |
| 3    | 2           | $$(A \lor B)$$       | $$ \lor $$I     | 2          |
| 4    | 1,2         | $$ \bot $$                  | $$ \neg $$E     | 1,3        |
| 5    | 1           | $$ \neg A$$          | $$ \neg $$I     | 2,4        |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\vdash (A \lor \neg A)$$</span>

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

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow B), \neg B \vdash \neg A$$</span>

## Hypothetical Syllogism

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow B), (B \rightarrow C) \vdash (A \rightarrow C)$$</span>

## Disjunctive Syllogism

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor B), \neg B \vdash A$$</span>

## Construction Dilemma

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \rightarrow B) \land (C \rightarrow D)), (A \lor C) \vdash (B \lor D)$$</span>

## Destructive Dilemma

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \rightarrow B) \land (C \rightarrow D)), (\neg B \lor \neg D) \vdash (\neg A \lor \neg C)$$</span>

# $$F \equiv G$$ Predicate Logic

## Trivial Proof

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall xF(x) \vdash \exists x F(x)$$</span>

| Line | Assumptions | Formula          | Justification | References |
| ---- | ----------- | ---------------- | ------------- | ---------- |
| 1    | 1           | $ \forall xF(x)$ | Assump. I     |            |
| 2    | 1           | $F(c)$           | $ \forall $E  | 1          |
| 3    | 1           | $ \exists xF(x)$ | $ \exists $I  | 2          |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x \forall y F(x,y) \vdash \forall x \exists y F(x,y)$$</span>

| Line | Assumptions | Formula                      | Justification | References |
| ---- | ----------- | ---------------------------- | ------------- | ---------- |
| 1    | 1           | $$ \exists y \forall xF(x,y)$$ | Assump. I     |            |
| 2    | 2           | $$ \forall xF(x,c)$$           | Assump. I     |            |
| 3    | 2           | $$F(d,c)$$                     | $$ \forall $$E  | 2          |
| 4    | 2           | $$ \exists yF(d,y)$$           | $$ \exists $$I  | 3          |
| 5    | 2           | $$ \forall x \exists yF(x,y)$$ | $$ \forall $$I  | 4          |
| 6    | 1           | $$ \forall x \exists yF(x,y)$$ | $$ \exists $$E  | 1,2,5      |

## Qualifier Negation

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg \forall x F(x) \vdash \exists x \neg F(x)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x \neg F(x) \vdash \neg \forall x F(x)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg \exists x F(x) \vdash \forall x \neg F(x)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x \neg F(x) \vdash \neg \exists x F(x)$$</span>

## Qualifier Unification

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x F(x) \land \forall x G(x)) \vdash \forall x (F(x) \land G(x))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x (F(x) \land G(x)) \vdash (\forall x F(x) \land \forall x G(x))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\exists x F(x) \lor \exists x G(x)) \vdash \exists x (F(x) \lor G(x))$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x (F(x) \lor G(x)) \vdash (\exists x F(x) \lor \exists x G(x))$$</span>

## Qualifier Transposition

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x \forall y F(x,y) \vdash \forall y \forall x F(x,y)$$</span>

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x \exists y F(x,y) \vdash \exists y \exists x F(x,y)$$</span>


