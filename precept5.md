---
title: "logic precept 5"
author: Hans Halvorson
---

Today we cover three things: (1) meta-rules for proofs, (2) relating
proofs to truth tables, and (3) review for midterm exam.

# Meta-rules for proofs

## Substitution

Since our rules of proof are schematic, changing propositional
constants (i.e. atomic sentences) in a proof preserves validity.

BUT: an invalid argument can be made valid by substitution! Example:
$P\to Q$ is invalid, but $P\to P$ is valid.



## Cut

You don't need to be able to articulate "cut", but it is one important
way that old proofs can be spliced together to make new proofs. Let's
illustrate it with an example.

```
1   (1) p|q        A
2   (2) -p         A
3   (3) p          A
2,3 (4) q          2,3 cut EFQ
5   (5) q          A
1,2 (6) q          1,3,4,5,5 |E
```

```
1   (1) p|q        A
2   (2) -p         A
1,2 (3) q          1,2 cut disjunctive syllogism
```


## Replacement




## Liberal proofs 






# Relating proofs and truth tables 

**Soundness theorem:** If there is a proof of the sequent $A_1,\dots
,A_n\vdash B$, then the corresponding argument is valid. That is, for
any row in their joint truth table, if all of $A_1,\dots ,A_n$ are
true, then $B$ is also true.

*What it means in practice:* If there is a way for all of $A_1,\dots
,A_n$ to be true and $B$ false, then there is no proof of $B$ from
$A_1,\dots ,A_n$. (No correctly written proof with end with $B$ on the
main line, and dependencies $A_1,\dots ,A_n$.)

**Completeness theorem:** If the argument from $A_1,\dots ,A_n$ to $B$
is valid (in the sense of truth tables), then there is a correctly
written proof of the sequent $A_1,\dots ,A_n\vdash B$.

*What it means in practice:* If the truth table for $A_1,\dots ,A_n;B$
says that it's valid, then there is a proof --- no matter how unlikely
it might seem! 

As a special case: if $B$ is a tautology (true in all cases), then
there is a proof of the sequent $\vdash B$. Examples: $P\vee\neg P$,
$P\to P$, $((P\to Q)\to P)\to P$.

**Exercise:** Explain how you know that the following is not a good
proof strategy:

**Exercise:** Can there be a correctly written proof with the
following lines? Explain your answer by reference to 

# Review for midterm exam
