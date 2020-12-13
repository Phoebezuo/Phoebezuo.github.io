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

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$A$$ | Assump. I |  |
| 2 | 1 | $$(A \land A)$$ | $$ \land $$I | 1,1 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \land A) \vdash A$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \land A)$$ | Assump. I |  |
| 2 | 1 | $$A$$ | $$ \land $$E | 1 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$A \vdash (A \lor A)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$A$$ | Assump. I |  |
| 2 | 1 | $$(A \lor A)$$ | $$ \lor $$I | 1 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor A) \vdash A$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \lor A)$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 1 | $$A$$ | $$ \lor $$E | 1,2,2,2,2 |

## Commutative

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \land B) \vdash (B \land A)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \land B)$$ | Assump. I |  |
| 2 | 1 | $$A$$ | $$ \land $$E | 1 |
| 3 | 1 | $$B$$ | $$ \land $$E | 1 |
| 4 | 1 | $$(B \land A)$$ | $$ \land $$I | 2,3 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor B) \vdash (B \lor A)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \lor B)$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 2 | $$(B \lor A)$$ | $$ \lor $$I | 2 |
| 4 | 4 | $$B$$ | Assump. I |  |
| 5 | 4 | $$(B \lor A)$$ | $$ \lor $$I | 4 |
| 6 | 1 | $$(B \lor A)$$ | $$ \lor $$E | 1,2,3,4,5 |

## Associative

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A\land (B\land C)) \vdash ((A\land B)\land C)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \land (B \land C))$$ | Assump. I |  |
| 2 | 1 | $$A$$ | $$ \land $$E | 1 |
| 3 | 1 | $$(B \land C)$$ | $$ \land $$E | 1 |
| 4 | 1 | $$B$$ | $$ \land $$E | 3 |
| 5 | 1 | $$C$$ | $$ \land $$E | 3 |
| 6 | 1 | $$(A \land B)$$ | $$ \land $$I | 2,4 |
| 7 | 1 | $$((A \land B) \land C)$$ | $$ \land $$I | 5,6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A\land B)\land C) \vdash (A\land (B\land C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \land B) \land C)$$ | Assump. I |  |
| 2 | 1 | $$(A \land B)$$ | $$ \land $$E | 1 |
| 3 | 1 | $$A$$ | $$ \land $$E | 2 |
| 4 | 1 | $$B$$ | $$ \land $$E | 2 |
| 5 | 1 | $$C$$ | $$ \land $$E | 1 |
| 6 | 1 | $$(B \land C)$$ | $$ \land $$I | 4,5 |
| 7 | 1 | $$(A \land (B \land C))$$ | $$ \land $$I | 3,6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A\lor (B\lor C)) \vdash ((A\lor B)\lor C)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \lor (B \lor C))$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 2 | $$(A \lor B)$$ | $$ \lor $$I | 2 |
| 4 | 2 | $$((A \lor B) \lor C)$$ | $$ \lor $$I | 3 |
| 5 | 5 | $$(B \lor C)$$ | Assump. I |  |
| 6 | 6 | $$B$$ | Assump. I |  |
| 7 | 7 | $$C$$ | Assump. I |  |
| 8 | 6 | $$(A \lor B)$$ | $$ \lor $$I | 6 |
| 9 | 6 | $$((A \lor B) \lor C)$$ | $$ \lor $$I | 8 |
| 10 | 7 | $$((A \lor B) \lor C)$$ | $$ \lor $$I | 7 |
| 11 | 5 | $$((A \lor B) \lor C)$$ | $$ \lor $$E | 5,6,7,9,10 |
| 12 | 1 | $$((A \lor B) \lor C)$$ | $$ \lor $$E | 1,2,4,5,11 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A\lor B)\lor C) \vdash (A\lor (B\lor C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \lor B) \lor C)$$ | Assump. I |  |
| 2 | 2 | $$(A \lor B)$$ | Assump. I |  |
| 3 | 3 | $$A$$ | Assump. I |  |
| 4 | 3 | $$(A \lor (B \lor C))$$ | $$ \lor $$I | 3 |
| 5 | 5 | $$B$$ | Assump. I |  |
| 6 | 5 | $$(B \lor C)$$ | $$ \lor $$I | 5 |
| 7 | 5 | $$(A \lor (B \lor C))$$ | $$ \lor $$I | 6 |
| 8 | 2 | $$(A \lor (B \lor C))$$ | $$ \lor $$E | 2,3,4,5,7 |
| 9 | 9 | $$C$$ | Assump. I |  |
| 10 | 9 | $$(B \lor C)$$ | $$ \lor $$I | 9 |
| 11 | 9 | $$(A \lor (B \lor C))$$ | $$ \lor $$I | 10 |
| 12 | 1 | $$(A \lor (B \lor C))$$ | $$ \lor $$E | 1,2,8,9,11 |

## Distributive

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \land (B \lor C)) \vdash ((A \land B) \lor (A \land C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \land (B \lor C))$$ | Assump. I |  |
| 2 | 1 | $$A$$ | $$ \land $$E | 1 |
| 3 | 1 | $$(B \lor C)$$ | $$ \land $$E | 1 |
| 4 | 4 | $$B$$ | Assump. I |  |
| 5 | 1,4 | $$(A \land B)$$ | $$ \land $$I | 2,4 |
| 6 | 1,4 | $$((A \land B) \lor (A \land C))$$ | $$ \lor $$I | 5 |
| 7 | 7 | $$C$$ | Assump. I |  |
| 8 | 1,7 | $$(A \land C)$$ | $$ \land $$I | 2,7 |
| 9 | 1,7 | $$((A \land B) \lor (A \land C))$$ | $$ \lor $$I | 8 |
| 10 | 1 | $$((A \land B) \lor (A \land C))$$ | $$ \lor $$E | 3,4,6,7,9 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \land B) \lor (A \land C)) \vdash (A \land (B \lor C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \land B) \lor (A \land C))$$ | Assump. I |  |
| 2 | 2 | $$(A \land B)$$ | Assump. I |  |
| 3 | 2 | $$A$$ | $$ \land $$E | 2 |
| 4 | 2 | $$B$$ | $$ \land $$E | 2 |
| 5 | 2 | $$(B \lor C)$$ | $$ \lor $$I | 4 |
| 6 | 2 | $$(A \land (B \lor C))$$ | $$ \land $$I | 3,5 |
| 7 | 7 | $$(A \land C)$$ | Assump. I |  |
| 8 | 7 | $$A$$ | $$ \land $$E | 7 |
| 9 | 7 | $$C$$ | $$ \land $$E | 7 |
| 10 | 7 | $$(B \lor C)$$ | $$ \lor $$I | 9 |
| 11 | 7 | $$(A \land (B \lor C))$$ | $$ \land $$I | 8,10 |
| 12 | 1 | $$(A \land (B \lor C))$$ | $$ \lor $$E | 1,2,6,7,11 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor(B \land C)) \vdash ((A \lor B) \land (A \lor C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \lor (B \land C))$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 2 | $$(A \lor B)$$ | $$ \lor $$I | 2 |
| 4 | 2 | $$(A \lor C)$$ | $$ \lor $$I | 2 |
| 5 | 2 | $$((A \lor B) \land (A \lor C))$$ | $$ \land $$I | 3,4 |
| 6 | 6 | $$(B \land C)$$ | Assump. I |  |
| 7 | 6 | $$B$$ | $$ \land $$E | 6 |
| 8 | 6 | $$(A \lor B)$$ | $$ \lor $$I | 7 |
| 9 | 6 | $$C$$ | $$ \land $$E | 6 |
| 10 | 6 | $$(A \lor C)$$ | $$ \lor $$I | 9 |
| 11 | 6 | $$((A \lor B) \land (A \lor C))$$ | $$ \land $$I | 8,10 |
| 12 | 1 | $$((A \lor B) \land (A \lor C))$$ | $$ \lor $$E | 1,2,5,6,11 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \lor B) \land (A \lor C)) \vdash (A \lor(B \land C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \lor B) \land (A \lor C))$$ | Assump. I |  |
| 2 | 1 | $$(A \lor B)$$ | $$ \land $$E | 1 |
| 3 | 1 | $$(A \lor C)$$ | $$ \land $$E | 1 |
| 4 | 4 | $$A$$ | Assump. I |  |
| 5 | 5 | $$B$$ | Assump. I |  |
| 6 | 6 | $$C$$ | Assump. I |  |
| 7 | 4 | $$(A \lor (B \land C))$$ | $$ \lor $$I | 4 |
| 8 | 5,6 | $$(B \land C)$$ | $$ \land $$I | 5,6 |
| 9 | 5,6 | $$(A \lor (B \land C))$$ | $$ \lor $$I | 8 |
| 10 | 1,6 | $$(A \lor (B \land C))$$ | $$ \lor $$E | 2,4,5,7,9 |
| 11 | 1 | $$(A \lor (B \land C))$$ | $$ \lor $$E | 3,4,6,7,10 |

## de Morgan's Laws

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg A\lor \neg B) \vdash \neg (A\land B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$( \neg A \lor  \neg B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg A$$ | Assump. I |  |
| 3 | 3 | $$ \neg B$$ | Assump. I |  |
| 4 | 4 | $$(A \land B)$$ | Assump. I |  |
| 5 | 4 | $$A$$ | $$ \land $$E | 4 |
| 6 | 2,4 | $$ \bot $$ | $$ \neg $$E | 2,5 |
| 7 | 2 | $$ \neg (A \land B)$$ | $$ \neg $$I | 4,6 |
| 8 | 4 | $$B$$ | $$ \land $$E | 4 |
| 9 | 3,4 | $$ \bot $$ | $$ \neg $$E | 3,8 |
| 10 | 3 | $$ \neg (A \land B)$$ | $$ \neg $$I | 4,9 |
| 11 | 1 | $$ \neg (A \land B)$$ | $$ \lor $$E | 1,2,3,7,10 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg (A\land B) \vdash (\neg A\lor \neg B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \neg (A \land B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg ( \neg A \lor \neg B)$$ | Assump. I |  |
| 3 | 3 | $$ \neg A$$ | Assump. I |  |
| 4 | 3 | $$( \neg A \lor  \neg B)$$ | $$ \lor $$I | 3 |
| 5 | 2,3 | $$ \bot $$ | $$ \neg $$E | 2,4 |
| 6 | 2 | $$ \neg \neg A$$ | $$ \neg $$I | 3,5 |
| 7 | 7 | $$ \neg B$$ | Assump. I |  |
| 8 | 7 | $$( \neg A \lor \neg B)$$ | $$ \lor $$I | 7 |
| 9 | 2,7 | $$ \bot $$ | $$ \neg $$E | 2,8 |
| 10 | 2 | $$ \neg  \neg B$$ | $$ \neg $$I | 7,9 |
| 11 | 2 | $$(\neg \neg A) \land  \neg \neg B)$$ | $$ \land $$I | 6,10 |
| 12 | 2 | $$ \neg \neg A$$ | $$ \land $$E | 11 |
| 13 | 2,3 | $$ \bot $$ | $$ \neg $$E | 3,12 |
| 14 | 2 | $$A$$ | RA | 3,13 |
| 15 | 2 | $$ \neg  \neg B$$ | $$ \land $$E | 11 |
| 16 | 2,7 | $$ \bot $$ | $$ \neg $$E | 7,15 |
| 17 | 2 | $$B$$ | RA | 7,16 |
| 18 | 2 | $$(A \land B)$$ | $$ \land $$I | 14,17 |
| 19 | 1,2 | $$ \bot $$ | $$ \neg $$E | 1,18 |
| 20 | 1 | $$( \neg A \lor \neg B)$$ | RA | 2,19 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg A\land \neg B) \vdash \neg (A\lor B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$( \neg A \land  \neg B)$$ | Assump. I |  |
| 2 | 1 | $$ \neg A$$ | $$ \land $$E | 1 |
| 3 | 1 | $$ \neg B$$ | $$ \land $$E | 1 |
| 4 | 4 | $$(A \lor B)$$ | Assump. I |  |
| 5 | 5 | $$ \neg B$$ | Assump. I |  |
| 6 | 6 | $$B$$ | Assump. I |  |
| 7 | 5,6 | $$ \bot $$ | $$ \neg $$E | 5,6 |
| 8 | 5,6 | $$A$$ | $$ \bot $$ | 7 |
| 9 | 9 | $$A$$ | Assump. I |  |
| 10 | 4,5 | $$A$$ | $$ \lor $$E | 4,6,8,9,9 |
| 11 | 1,4,5 | $$ \bot $$ | $$ \neg $$E | 2,10 |
| 12 | 1,4 | $$B$$ | RA | 5,11 |
| 13 | 1,4 | $$ \bot $$ | $$ \neg $$E | 3,12 |
| 14 | 1 | $$ \neg (A \lor B)$$ | $$ \neg $$I | 4,13 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg (A\lor B) \vdash (\neg A\land \neg B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \neg (A \lor B)$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 2 | $$(A \lor B)$$ | $$ \lor $$I | 2 |
| 4 | 1,2 | $$ \bot $$ | $$ \neg $$E | 1,3 |
| 5 | 1 | $$ \neg A$$ | $$ \neg $$I | 2,4 |
| 6 | 6 | $$B$$ | Assump. I |  |
| 7 | 6 | $$(A \lor B)$$ | $$ \lor $$I | 6 |
| 8 | 1,6 | $$ \bot $$ | $$ \neg $$E | 1,7 |
| 9 | 1 | $$ \neg B$$ | $$ \neg $$I | 6,8 |
| 10 | 1 | $$( \neg A \land  \neg B)$$ | $$ \land $$I | 5,9 |

## Double Negation

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg \neg A \vdash A$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \neg  \neg A$$ | Assump. I |  |
| 2 | 2 | $$ \neg A$$ | Assump. I |  |
| 3 | 1,2 | $$ \bot $$ | $$ \neg $$E | 1,2 |
| 4 | 1 | $$A$$ | RA | 2,3 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$A \vdash \neg \neg A$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$A$$ | Assump. I |  |
| 2 | 2 | $$ \neg A$$ | Assump. I |  |
| 3 | 1,2 | $$ \bot $$ | $$ \neg $$E | 1,2 |
| 4 | 1 | $$ \neg  \neg A$$ | $$ \neg $$I | 2,3 |

## Implication Definition

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg A\lor B) \vdash (A \rightarrow B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$( \neg A \lor B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg A$$ | Assump. I |  |
| 3 | 3 | $$A$$ | Assump. I |  |
| 4 | 2,3 | $$ \bot $$ | $$ \neg $$E | 2,3 |
| 5 | 2,3 | $$B$$ | $$ \bot $$ | 4 |
| 6 | 2 | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 3,5 |
| 7 | 7 | $$B$$ | Assump. I |  |
| 8 | 3,7 | $$(A \land B)$$ | $$ \land $$I | 3,7 |
| 9 | 3,7 | $$B$$ | $$ \land $$E | 8 |
| 10 | 7 | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 3,9 |
| 11 | 1 | $$(A \rightarrow B)$$ | $$ \lor $$E | 1,2,6,7,10 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow B) \vdash (\neg A\lor B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \rightarrow B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg (\neg A \lor B)$$ | Assump. I |  |
| 3 | 3 | $$A$$ | Assump. I |  |
| 4 | 1,3 | $$B$$ | $$ \rightarrow $$E | 1,3 |
| 5 | 1,3 | $$( \neg A \lor B)$$ | $$ \lor $$I | 4 |
| 6 | 1,2,3 | $$ \bot $$ | $$ \neg $$E | 2,5 |
| 7 | 1,2 | $$ \neg A$$ | $$ \neg $$I | 3,6 |
| 8 | 1,2 | $$( \neg A \lor B)$$ | $$ \lor $$I | 7 |
| 9 | 1,2 | $$ \bot $$ | $$ \neg $$E | 2,8 |
| 10 | 1 | $$( \neg A \lor B)$$ | RA | 2,9 |

## Transposition

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow B) \vdash (\neg B \rightarrow \neg A)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \rightarrow B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg B$$ | Assump. I |  |
| 3 | 3 | $$A$$ | Assump. I |  |
| 4 | 1,3 | $$B$$ | $$ \rightarrow $$E | 1,3 |
| 5 | 1,2,3 | $$ \bot $$ | $$ \neg $$E | 2,4 |
| 6 | 1,2 | $$ \neg A$$ | $$ \neg $$I | 3,5 |
| 7 | 1 | $$( \neg B \rightarrow  \neg A)$$ | $$ \rightarrow $$I | 2,6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\neg B \rightarrow \neg A) \vdash (A \rightarrow B)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$( \neg B \rightarrow  \neg A)$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 3 | $$ \neg A$$ | Assump. I |  |
| 4 | 2,3 | $$ \bot $$ | $$ \neg $$E | 2,3 |
| 5 | 2 | $$ \neg  \neg A$$ | $$ \neg $$I | 3,4 |
| 6 | 6 | $$ \neg B$$ | Assump. I |  |
| 7 | 1,6 | $$ \neg A$$ | $$ \rightarrow $$E | 1,6 |
| 8 | 1,2,6 | $$ \bot $$ | $$ \neg $$E | 5,7 |
| 9 | 1,2 | $$B$$ | RA | 6,8 |
| 10 | 1 | $$(A \rightarrow B)$$ | $$ \rightarrow $$I | 2,9 |

## Exportation

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \land B) \rightarrow C) \vdash (A \rightarrow (B \rightarrow C))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \land B) \rightarrow C)$$ | Assump. I |  |
| 2 | 2 | $$A$$ | Assump. I |  |
| 3 | 3 | $$B$$ | Assump. I |  |
| 4 | 2,3 | $$(A \land B)$$ | $$ \land $$I | 2,3 |
| 5 | 1,2,3 | $$C$$ | $$ \rightarrow $$E | 1,4 |
| 6 | 1,2 | $$(B \rightarrow C)$$ | $$ \rightarrow $$I | 3,5 |
| 7 | 1 | $$(A \rightarrow (B \rightarrow C))$$ | $$ \rightarrow $$I | 2,6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow (B \rightarrow C)) \vdash ((A \land B) \rightarrow C)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \rightarrow (B \rightarrow C))$$ | Assump. I |  |
| 2 | 2 | $$(A \land B)$$ | Assump. I |  |
| 3 | 2 | $$A$$ | $$ \land $$E | 2 |
| 4 | 2 | $$B$$ | $$ \land $$E | 2 |
| 5 | 1,2 | $$(B \rightarrow C)$$ | $$ \rightarrow $$E | 1,3 |
| 6 | 1,2 | $$C$$ | $$ \rightarrow $$E | 4,5 |
| 7 | 1 | $$((A \land B) \rightarrow C)$$ | $$ \rightarrow $$I | 2,6 |

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

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \rightarrow B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg B$$ | Assump. I |  |
| 3 | 3 | $$A$$ | Assump. I |  |
| 4 | 1,3 | $$B$$ | $$ \rightarrow $$E | 1,3 |
| 5 | 1,2,3 | $$ \bot $$ | $$ \neg $$E | 2,4 |
| 6 | 1,2 | $$ \neg A$$ | $$ \neg $$I | 3,5 |

## Hypothetical Syllogism

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \rightarrow B), (B \rightarrow C) \vdash (A \rightarrow C)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \rightarrow B)$$ | Assump. I |  |
| 2 | 2 | $$(B \rightarrow C)$$ | Assump. I |  |
| 3 | 3 | $$A$$ | Assump. I |  |
| 4 | 1,3 | $$B$$ | $$ \rightarrow $$E | 1,3 |
| 5 | 1,2,3 | $$C$$ | $$ \rightarrow $$E | 2,4 |
| 6 | 1,2 | $$(A \rightarrow C)$$ | $$ \rightarrow $$I | 3,5 |

## Disjunctive Syllogism

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(A \lor B), \neg B \vdash A$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$(A \lor B)$$ | Assump. I |  |
| 2 | 2 | $$ \neg B$$ | Assump. I |  |
| 3 | 3 | $$B$$ | Assump. I |  |
| 4 | 2,3 | $$ \bot $$ | $$ \neg $$E | 2,3 |
| 5 | 2,3 | $$A$$ | $$ \bot $$ | 4 |
| 6 | 6 | $$A$$ | Assump. I |  |
| 7 | 1,2 | $$A$$ | $$ \lor $$E | 1,3,5,6,6 |

## Construction Dilemma

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \rightarrow B) \land (C \rightarrow D)), (A \lor C) \vdash (B \lor D)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \rightarrow B) \land (C \rightarrow D))$$ | Assump. I |  |
| 2 | 2 | $$(A \lor C)$$ | Assump. I |  |
| 3 | 1 | $$(A \rightarrow B)$$ | $$ \land $$E | 1 |
| 4 | 1 | $$(C \rightarrow D)$$ | $$ \land $$E | 1 |
| 5 | 5 | $$A$$ | Assump. I |  |
| 6 | 1,5 | $$B$$ | $$ \rightarrow $$E | 3,5 |
| 7 | 1,5 | $$(B \lor D)$$ | $$ \lor $$I | 6 |
| 8 | 8 | $$C$$ | Assump. I |  |
| 9 | 1,8 | $$D$$ | $$ \rightarrow $$E | 4,8 |
| 10 | 1,8 | $$(B \lor D)$$ | $$ \lor $$I | 9 |
| 11 | 1,2 | $$(B \lor D)$$ | $$ \lor $$E | 2,5,7,8,10 |

## Destructive Dilemma

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$((A \rightarrow B) \land (C \rightarrow D)), (\neg B \lor \neg D) \vdash (\neg A \lor \neg C)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$((A \rightarrow B) \land (C \rightarrow D))$$ | Assump. I |  |
| 2 | 2 | $$(\neg B \lor \neg D)$$ | Assump. I |  |
| 3 | 1 | $$(A \rightarrow B)$$ | $$ \land $$E | 1 |
| 4 | 1 | $$(C \rightarrow D)$$ | $$ \land $$E | 1 |
| 5 | 5 | $$ \neg ( \neg A \lor  \neg C)$$ | Assump. I |  |
| 6 | 6 | $$ \neg A$$ | Assump. I |  |
| 7 | 6 | $$( \neg A \lor  \neg C)$$ | $$ \lor $$I | 6 |
| 8 | 5,6 | $$ \bot $$ | $$ \neg $$E | 5,7 |
| 9 | 5 | $$A$$ | RA | 6,8 |
| 10 | 1,5 | $$B$$ | $$ \rightarrow $$E | 3,9 |
| 11 | 11 | $$ \neg C$$ | Assump. I |  |
| 12 | 11 | $$( \neg A \lor  \neg C)$$ | $$ \lor $$I | 11 |
| 13 | 5,11 | $$ \bot $$ | $$ \neg $$E | 5,12 |
| 14 | 5 | $$C$$ | RA | 11,13 |
| 15 | 1,5 | $$D$$ | $$ \rightarrow $$E | 4,14 |
| 16 | 16 | $$ \neg B$$ | Assump. I |  |
| 17 | 1,5,16 | $$ \bot $$ | $$ \neg $$E | 10,16 |
| 18 | 1,5,16 | $$ \neg D$$ | $$ \bot $$ | 17 |
| 19 | 19 | $$ \neg D$$ | Assump. I |  |
| 20 | 1,2,5 | $$ \neg D$$ | $$ \lor $$E | 2,16,18,19,19 |
| 21 | 1,2,5 | $$ \bot $$ | $$ \neg $$E | 15,20 |
| 22 | 1,2 | $$(\neg A \lor  \neg C)$$ | RA | 5,21 |

# $$F \equiv G$$ Predicate Logic

## Trivial Proof

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall xF(x) \vdash \exists x F(x)$$</span>

| Line | Assumptions | Formula          | Justification | References |
| ---- | ----------- | ---------------- | ------------- | ---------- |
| 1    | 1           | $$ \forall xF(x)$$ | Assump. I     |            |
| 2    | 1           | $$F(c)$$           | $$ \forall $$E  | 1          |
| 3    | 1           | $$ \exists xF(x)$$ | $$ \exists $$I  | 2          |

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

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \neg  \forall xF(x)$$ | Assump. I |  |
| 2 | 2 | $$ \neg  \exists x \neg F(x)$$ | Assump. I |  |
| 3 | 3 | $$ \neg F(c)$$ | Assump. I |  |
| 4 | 3 | $$ \exists x \neg F(x)$$ | $$ \exists $$I | 3 |
| 5 | 2,3 | $$ \bot $$ | $$ \neg $$E | 2,4 |
| 6 | 2 | $$F(c)$$ | RA | 3,5 |
| 7 | 2 | $$ \forall xF(x)$$ | $$ \forall $$I | 6 |
| 8 | 1,2 | $$ \bot $$ | $$ \neg $$E | 1,7 |
| 9 | 1 | $$ \exists x \neg F(x)$$ | RA | 2,8 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x \neg F(x) \vdash \neg \forall x F(x)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \exists x \neg F(x)$$ | Assump. I |  |
| 2 | 2 | $$ \forall xF(x)$$ | Assump. I |  |
| 3 | 2 | $$F(c)$$ | $$ \forall $$E | 2 |
| 4 | 4 | $$ \neg F(c)$$ | Assump. I |  |
| 5 | 2,4 | $$ \bot $$ | $$ \neg $$E | 3,4 |
| 6 | 1,2 | $$ \bot $$ | $$ \exists $$E | 1,4,5 |
| 7 | 1 | $$ \neg  \forall xF(x)$$ | $$ \neg $$I | 2,6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\neg \exists x F(x) \vdash \forall x \neg F(x)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \neg  \exists xF(x)$$ | Assump. I |  |
| 2 | 2 | $$F(c)$$ | Assump. I |  |
| 3 | 2 | $$ \exists xF(x)$$ | $$ \exists $$I | 2 |
| 4 | 1,2 | $$ \bot $$ | $$ \neg $$E | 1,3 |
| 5 | 1 | $$ \neg F(c)$$ | $$ \neg $$I | 2,4 |
| 6 | 1 | $$ \forall x \neg F(x)$$ | $$ \forall $$I | 5 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x \neg F(x) \vdash \neg \exists x F(x)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \forall x \neg F(x)$$ | Assump. I |  |
| 2 | 2 | $$ \exists xF(x)$$ | Assump. I |  |
| 3 | 3 | $$F(c)$$ | Assump. I |  |
| 4 | 1 | $$ \neg F(c)$$ | $$ \forall $$E | 1 |
| 5 | 1,3 | $$ \bot $$ | $$ \neg $$E | 3,4 |
| 6 | 1,2 | $$ \bot $$ | $$ \exists $$E | 2,3,5 |
| 7 | 1 | $$ \neg  \exists xF(x)$$ | $$ \neg $$I | 2,6 |

## Qualifier Unification

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x F(x) \land \forall x G(x)) \vdash \forall x (F(x) \land G(x))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$( \forall xF(x) \land  \forall xG(x))$$ | Assump. I |  |
| 2 | 1 | $$ \forall xF(x)$$ | $$ \land $$E | 1 |
| 3 | 1 | $$F(c)$$ | $$ \forall $$E | 2 |
| 4 | 1 | $$ \forall xG(x)$$ | $$ \land $$E | 1 |
| 5 | 1 | $$G(c)$$ | $$ \forall $$E | 4 |
| 6 | 1 | $$(F(c) \land G(c))$$ | $$ \land $$I | 3,5 |
| 7 | 1 | $$ \forall x(F(x) \land G(x))$$ | $$ \forall $$I | 6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x (F(x) \land G(x)) \vdash (\forall x F(x) \land \forall x G(x))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \forall x(F(x) \land G(x))$$ | Assump. I |  |
| 2 | 1 | $$(F(c) \land G(c))$$ | $$ \forall $$E | 1 |
| 3 | 1 | $$F(c)$$ | $$ \land $$E | 2 |
| 4 | 1 | $$ \forall xF(x)$$ | $$ \forall $$I | 3 |
| 5 | 1 | $$G(c)$$ | $$ \land $$E | 2 |
| 6 | 1 | $$ \forall xG(x)$$ | $$ \forall $$I | 5 |
| 7 | 1 | $$( \forall xF(x) \land  \forall xG(x))$$ | $$ \land $$I | 4,6 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$(\exists x F(x) \lor \exists x G(x)) \vdash \exists x (F(x) \lor G(x))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$( \exists xF(x) \lor  \exists xG(x))$$ | Assump. I |  |
| 2 | 2 | $$ \exists xF(x)$$ | Assump. I |  |
| 3 | 3 | $$F(c)$$ | Assump. I |  |
| 4 | 3 | $$(F(c) \lor G(c))$$ | $$ \lor $$I | 3 |
| 5 | 3 | $$ \exists x(F(x) \lor G(x))$$ | $$ \exists $$I | 4 |
| 6 | 2 | $$ \exists x(F(x) \lor G(x))$$ | $$ \exists $$E | 2,3,5 |
| 7 | 7 | $$ \exists xG(x)$$ | Assump. I |  |
| 8 | 8 | $$G(c)$$ | Assump. I |  |
| 9 | 8 | $$(F(c) \lor G(c))$$ | $$ \lor $$I | 8 |
| 10 | 8 | $$ \exists x(F(x) \lor G(x))$$ | $$ \exists $$I | 9 |
| 11 | 7 | $$ \exists x(F(x) \lor G(x))$$ | $$ \exists $$E | 7,8,10 |
| 12 | 1 | $$ \exists x(F(x) \lor G(x))$$ | $$ \lor $$E | 1,2,6,7,11 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x (F(x) \lor G(x)) \vdash (\exists x F(x) \lor \exists x G(x))$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \exists x(F(x) \lor G(x))$$ | Assump. I |  |
| 2 | 2 | $$(F(c) \lor G(c))$$ | Assump. I |  |
| 3 | 3 | $$F(c)$$ | Assump. I |  |
| 4 | 3 | $$ \exists xF(x)$$ | $$ \exists $$I | 3 |
| 5 | 3 | $$( \exists xF(x) \lor  \exists xG(x))$$ | $$ \lor $$I | 4 |
| 6 | 6 | $$G(c)$$ | Assump. I |  |
| 7 | 6 | $$ \exists xG(x)$$ | $$ \exists $$I | 6 |
| 8 | 6 | $$( \exists xF(x) \lor  \exists xG(x))$$ | $$ \lor $$I | 7 |
| 9 | 2 | $$( \exists xF(x) \lor  \exists xG(x))$$ | $$ \lor $$E | 2,3,5,6,8 |
| 10 | 1 | $$( \exists xF(x) \lor  \exists xG(x))$$ | $$ \exists $$E | 1,2,9 |

## Qualifier Transposition

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\forall x \forall y F(x,y) \vdash \forall y \forall x F(x,y)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \forall x \forall yF(x,y)$$ | Assump. I |  |
| 2 | 1 | $$ \forall yF(c,y)$$ | $$ \forall $$E | 1 |
| 3 | 1 | $$F(c,d)$$ | $$ \forall $$E | 2 |
| 4 | 1 | $$ \forall xF(x,d)$$ | $$ \forall $$I | 3 |
| 5 | 1 | $$ \forall y \forall xF(x,y)$$ | $$ \forall $$I | 4 |

<span class="bg-yellow black" style="text-align: center; font-size:25px">$$\exists x \exists y F(x,y) \vdash \exists y \exists x F(x,y)$$</span>

| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $$ \exists x \exists yF(x,y)$$ | Assump. I |  |
| 2 | 2 | $$ \exists yF(c,y)$$ | Assump. I |  |
| 3 | 3 | $$F(c,d)$$ | Assump. I |  |
| 4 | 3 | $$ \exists xF(x,d)$$ | $$ \exists $$I | 3 |
| 5 | 3 | $$ \exists y \exists xF(x,y)$$ | $$ \exists $$I | 4 |
| 6 | 2 | $$ \exists y \exists xF(x,y)$$ | $$ \exists $$E | 2,3,5 |
| 7 | 1 | $$ \exists y \exists xF(x,y)$$ | $$ \exists $$E | 1,2,6 |

> PDF version can be found at [here](https://github.com/Phoebezuo/Natural-Deduction-Proof/blob/main/Derived_Rules_of_Natural_Deduction_Proof.pdf)
