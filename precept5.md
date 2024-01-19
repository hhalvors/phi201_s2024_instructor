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

**Definition.** Let $A$ be a propositional logic sentence. We say that
$A'$ is a **substitution instance** of $A$ if $A'$ results from
uniformly replacing propositional constants in $A$ with sentences.

This definition is not precise; but a more precise definition would
require that we talk explicitly about the definition of a type `WFF`
of well-formed formulas of propositional logic --- and this definition
is recursive. Here's what the definition of such a type might look
like in the Haskell programming language:

```haskell
data WFF
    = Var String         -- A propositional variable
    | Not WFF            -- Negation
    | And WFF WFF        -- Conjunction
    | Or WFF WFF         -- Disjunction
    | Imply WFF WFF      -- Implication
    | Iff WFF WFF        -- Biconditional (if and only if)
```

In that case, we could define a function that substitutes a formula
`newP` for `P` as follows:

```haskell
substituteP :: WFF -> WFF -> WFF
substituteP newP = go
  where
    go (Var "P") = newP  -- Substitute newP for Var "P"
    go (Not wff) = Not (go wff)
    go (And wff1 wff2) = And (go wff1) (go wff2)
    go (Or wff1 wff2) = Or (go wff1) (go wff2)
    go (Imply wff1 wff2) = Imply (go wff1) (go wff2)
    go (Iff wff1 wff2) = Iff (go wff1) (go wff2)
    go wff = wff  -- In the case of Var not equal to "P", return as is
```


## Cut

Cut is one way that old proofs can be spliced together to make new
proofs.[^1] It is not a *new* rule in the sense of allowing us to
prove things that we couldn't already prove. Instead, it is a way to
shorten proofs by referring to things that have already been proven.

Let's illustrate cut with an example. We first prove EFQ: $P,\neg
P\vdash Q$.

```
1   (1) p      A
2   (2) -p     A
3   (3) -q     A
1,2 (4) p&-p   1,2 &I
1,2 (5) --q    3,4 RA
1,2 (6) q      5 DN
```

We now want to use EFQ inside another proof. Here we will prove
Disjunctive Syllogism: $P\vee Q,\neg P\vdash Q$. 

```
1   (1) p|q        A
2   (2) -p         A
3   (3) p          A
2,3 (4) q          2,3 cut EFQ
5   (5) q          A
1,2 (6) q          1,3,4,5,5 |E
```

Look at lines 2 and 3. They are identical to lines 1 and 2 from the
proof of EFQ above. So we could literally just have copied that proof
in. But instead, we just write its conclusion on the next line and
cite the proof of EFQ that we have already given.

To use cut, it is *not* essential that the lines in the new proof are
*identical* to the lines in the old proof. For example, we could also
invoke EFQ in the following proof.

```
1  (1) p&-p     A
1  (2) p        1 &E
1  (3) -p       1 &E
1  (4) q        2,3 cut EFQ
```

Here lines 2 and 3 are not assumptions, as they were in the proof of
EFQ. But this use of cut is still legitimate, since line 4 has the
dependencies of both of the cited lines.






## Replacement

There are some proofs that seem like they should be really simple, but
they turn out to be annoyingly complex. One example is a proof of the
sequent $P\vee Q\vdash P\vee \neg\neg Q$. You know that $\neg \neg Q$
and $Q$ are equivalent. Yet, to derive $P\vee\neg\neg Q$ from $P\vee
Q$ requires setting up a full or-elimination. Surely, you might think,
we should have a rule that allows us to simply replace any subformula
of a formula with a logically equivalent formula! 

We do *not* take a rule like that to be basic. The main reason we
don't take it to be basic is because we don't have to: it follows, as
a logical consequence, from the rules we already have! That is, you
*can* simply replace subformulas with logically equivalent formulas,
and I promise you that another more patient (or more skeptical) person
could get the same derivation just by using the other rules.

**Exercise.** Walk through the following series of equivalences
(designated by the equality sign), citing the sequents that were
used. 

```
-(p<>q) = -((p>q)&(q>p))
        = -(p>q)|-(q>p)
		= (p&-q)|(q&-p)
```

**Exercise.** Use replacement to argue that $(P\wedge Q)\vee (P\wedge
\neg Q)$ is equivalent to $P$.




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

[^1]: The nature of the cut rule is actually a subject of serious
inquiry in mathematical logic (proof theory) and philosophical logic.
