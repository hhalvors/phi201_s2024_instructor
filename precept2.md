---
title: "logic precept 2"
author: Hans Halvorson
---

# Introduction 

This week finds us in the thick of things with learning how to write
formal proofs. The new complication is that we now use dependency
numbers, and the primary focus of today's precept is developing your
familiarity and proficiency with this approach. The biggest challenge,
without a doubt, is the rule of or elimination. In fact, it is the
most complicated inference rule that we will learn all semester.

We will also do a bit more translation work in order to draw on the
intuitions that you already have from using logic with natural
language.

# Old proof rules in new form

Let's first see how to use our old rules (from last week) while
incorporating the use of dependency numbers.

**Exercise 2.5** ($\wedge$E, $\wedge$I, $\vee$I, MP, MT, DN)

1. $P\wedge (Q\wedge R)\:\dashv\vdash\: (P\wedge Q)\wedge R$ 

```
1  (1) p&(q&r)   A
1  (2) p         1 &E
1  (3) q&r       1 &E
1  (4) q         3 &E
1  (5) r         3 &E
1  (6) p&q       2,4 &I
1  (7) (p&q)&r   6,5 &I
```

Here we see, among other things, that and introduction tells us to
combine dependencies, but that we don't need to include
redundancies. In particular, we write just `1` as dependency in lines
6 and 7 instead of `1,1` or `1,1,1`.

2. $P\:\dashv\vdash\: P\wedge P$

3. $P\to \neg Q,Q\: \vdash \: \neg P$

4. $\neg \neg P\: \vdash \: \neg \neg P\wedge (P\vee Q)$

5. $\neg (P\wedge Q)\to R,\neg R\:\vdash \: P$

6. $P\to (Q\wedge R),A\to \neg R,P\:\vdash\: \neg A$

7. $\neg P\to\neg Q,Q\:\vdash \: P$

8. $P\:\vdash \: \neg \neg (P\vee Q)$



# New proof rules 

## Conditional proof

Recall that a **conditional** is a statement of the form $A\to B$. The
rules MP and MT allow us to reason *from* a conditional, while the
rule CP allows us to reason *to* a conditional. The general pattern of
CP is: to prove $A\to B$, one assumes $A$ and proves $B$.

**Exercise 3.1** Prove the following sequents. (You should not use
reductio ad absurdum in any of these problems, although you might be
tempted to do so in 3.1.8, 3.1.9, and 3.1.10. The hints explain how
the other rules can be used to derive the same things as RA, albeit in
a much more roundabout way. For the philosophically minded: MT is an
"impure" rule since its application requires the presence of different
connectives.)

1.  $P\:\vdash\: Q\to (P\wedge Q)$

2.  $(P\to Q)\wedge (P\to R)\:\vdash\: P\to (Q\wedge R)$

3.  $P\to (Q\to R)\:\vdash\: Q\to (P\to R)$

4.  $P\to Q\:\vdash\: (Q\to R)\to (P\to R)$  (Hint: this will seem
    easy once you assume the antecedent of the conclusion.)

5.  $P\to (P\to Q)\:\vdash\: P\to Q$

6.  $P\to (Q\to R)\:\vdash\: (P\wedge Q)\to R$

7.  $(P\vee Q)\to R\:\vdash\: P\to R$

8.  $\neg P\:\vdash\: \neg (P\wedge Q)$ (Hint: For any sentences
$\phi$ and $\psi$, if you can derive $\psi\vdash\phi$ then you can
derive $\neg\phi\vdash\neg \psi$. Indeed, apply CP to $\psi\vdash\phi$
to derive $\vdash \psi\to \phi$. Now assume $\neg \phi$ and apply MT.)

9.  $\neg (P\vee Q)\:\vdash\: \neg P\wedge\neg Q$ (Hint: If you can
prove $\neg (P\vee Q)\vdash \neg P$ and $\neg (P\vee Q)\vdash \neg Q$
individually, then you can use $\wedge$I and you're done. )
	  
10. $P\to \neg P\:\vdash\:\neg P$ (Hint: First prove that $P\vdash
(P\to \neg P)\to \neg P$, resulting in a proof with first line "$1\:
(1)\,P\: \mathrm{A}$" and last line "$1\: (n)\,(P\to \neg P)\to \neg
P$". Now use line 1 again to derive $\neg\neg P$ and apply MT.)
	  
11. $P\to (Q\to R),P\to Q\:\vdash \: P\to R$

12. $P\to (Q\to R)\:\vdash\: (P\to Q)\to (P\to R)$

13. $P\to Q\:\vdash \:\neg Q\to\neg P$ 

14. $(P\wedge Q)\to R\: \vdash \: P\to (Q\to R)$

15. $P\to (Q\to R)\:\vdash\: P\to (\neg R\to \neg Q)$

16. $P\to (Q\to R)\:\vdash\: \neg R\to (Q\to \neg P)$

17. $(P\to Q)\to P\:\vdash\: (P\to Q)\to Q$ (Hint: Not as difficult as
it looks. Assume $(P\to Q)\to P$ and $P\to Q$. The latter can be used
both as the antecedent of a conditional, and as a conditional itself.)


**Exercise 3.2** Prove the following sequents. (Do not use reductio ad
absurdum, which is only introduced in a subsequent section.)

1.  $\vdash\:(P\wedge Q)\to (Q\wedge P)$

2.  $\vdash\:(P\wedge Q)\to P$

3.  $\vdash\:Q\to (P\to Q)$

4.  $\vdash\:Q\to (P\to P)$ 

5.  $\vdash \:P\vee \neg P$ (Hint: This *can* be proven with the rules
    we have so far! One possibility is to use 3.1.10, but replace $P$
    with $P\vee \neg P$. In particular, use the fact that $\neg (P\vee
    \neg P)\vdash P$ to derive $\vdash \neg (P\vee \neg P)\to \neg\neg
    (P\vee \neg P)$.)
	
6. $\neg P\: \vdash \: P\to Q$ (Hint: Prove $\neg P\vdash \neg Q\to \neg P$
   and then use the contrapositive maneuver.)
   
7. $\vdash\: (P\to Q)\to (\neg Q\to \neg P)$

8. $(P\to Q)\to P,Q\:\vdash \: P$	
	
9. $(P\to Q)\to P\: \vdash \: \neg P\to P$








## Or elimination

**Exercise 3.3** Prove the following sequents. (Still do not use
RA. It is good to learn to prove directly when you can!)

1.  $(P\to R)\wedge (Q\to R)\:\vdash\: (P\vee Q)\to R$

2.  $P\vee (Q\vee R)\:\dashv\vdash\: (P\vee Q)\vee R$

3.  $P\vee Q,\neg P\:\vdash \: Q$ (Hint: Recall that $\neg P\vdash
    P\to Q$.)

4.  $P\wedge (Q\vee R)\:\dashv\vdash\: (P\wedge Q)\vee (P\wedge R)$

5.  $P\vee (Q\wedge R)\:\dashv\vdash\: (P\vee Q)\wedge (P\vee R)$

6.  $\neg P\vee Q\:\dashv\vdash\: P\to Q$

7.  $\neg P\vee \neg Q\:\vdash\: \neg (P\wedge Q)$


**Exercise 3.4** Prove the following sequents.

1.  $P\to Q\:\vdash\: \neg (P\wedge \neg Q)$

2.  $\neg (P\wedge Q)\:\vdash\: \neg P\vee \neg Q$

3.  $\neg (P\to Q)\:\vdash\: P\wedge \neg Q$ 

4. $\vdash (P\to Q)\vee (Q\to P)$ 

5. $P\to (Q\vee R)\:\vdash\: (P\to Q)\vee (P\to R)$

6.  $(P\wedge Q)\to \neg Q\:\vdash\:P\to \neg Q$

7. $P\wedge\neg Q\:\vdash\: \neg (P\to Q)$

8. $\vdash\: ((P\to Q)\to P)\to P$ (Hint: One possibility is to first
   prove $\vdash P\vee \neg P$, and then argue by cases. The first
   case is easy if you remember "positive paradox". For the second
   case, remember "negative paradox", i.e. that $\neg P$ implies $P\to
   Q$.)
   
9. $P\to (Q\vee R)\:\vdash \: \neg R\to (\neg Q\to \neg P)$

10. $P\to \neg Q\:\vdash\: (P\wedge Q)\to R$

11. $P\to \neg Q\:\vdash\: P\to (Q\to R)$

12. $\neg (P\to Q)\:\vdash \: P\to \neg Q$

13. $P\:\dashv\vdash\: (P\wedge Q)\vee (P\wedge\neg Q)$

14. $P\to (Q\to R)\:\dashv\vdash \: (P\to Q)\to (P\to R)$

15. $P\to\neg P\:\dashv\vdash\:\neg P$

16. $P\to (Q\to \neg Q)\:\dashv\vdash\: P\to \neg Q$
	  
17. $(P\to Q)\to (P\to \neg Q)\:\dashv\vdash\: P\to \neg Q$	  

18. $P\:\dashv\vdash\: P\wedge (Q\vee\neg Q)$

19. $P\:\dashv\vdash\: P\vee (Q\wedge\neg Q)$

20. $(P\to Q)\to Q\:\vdash\: (Q\to P)\to P$

21. $(P\to Q)\to R\:\vdash\: (P\to R)\to R$

22. $(P\to R)\to R\:\dashv\vdash\: P\vee R$ (Hint: it's easy to derive
$\neg P\to R$ from the sentence on the left.)
	
23. $(P\to Q)\to P\:\dashv\vdash \: P$ (Hint: assume $\neg P$ and
derive $P\to Q$.)


# Strategy summary and tips 

## Conditional proof

Conditional proof is relatively easy to execute, and to check for
correctness. However, you sometimes have to have a very good eye
indeed to see how to set up a conditional proof. Here are some rules
of thumb:

First: A step of conditional proof almost never happens "by
mistake". That is, you shouldn't ever just see two previous lines in
your proof and decide to apply conditional proof to them. Instead, you
should apply conditional proof only when you have decided (in advance)
that you want to prove a conditional, and you have assumed that
conditional's antecedent with the specific intention of using CP. One
way to enforce this upon yourself is by making an (optional)
annotation to your assumptions. For example, in the proof of $P\to
Q,Q\to R\vdash P\to R$:

```
1     (1) p>q     A
2     (2) q>r     A
3     (3) p       A (goal: r)
1,3   (4) q       1,3 MP
1,2,3 (5) r       2,4 MP
1,2   (6) p>r     3,5 CP 
```

Second: Sometimes CP seems too good to be true, in particular, for
proving conditions that have logically strong antecedents. Consider,
for example, the proof of $P\to (Q\to R)\vdash (P\wedge Q)\to R$.

```
1   (1) p>(q>r)    A
2   (2) p&q        A (goal: r)
2   (3) p          2 &E
1,2 (4) q>r        1,3 MP
2   (5) q          2 &E
1,2 (6) r          4,5 MP
1   (7) (p&q)>r    2,6 CP
```

I assumed `p&q` on line 2 precisely because my goal was to obtain the
conditional `(p&q)>r`. So I assumed the entire antecedent of that
conditional, which gave me what I needed to apply modus ponens twice.

## Or elimination

In contrast to CP, it can be very tricky to get the dependencies right
in an application of or elimination. However, if your understand the
strategy behind or elimination, and if you only use assumptions that
you have made as part of this strategy, then you will usually not make
mistakes with calculating the dependencies.




# Evaluating proofs 

**Exercise** Which of the following proofs with CP is correct? If a
proof is not correct, explain what is wrong with it, and say whether
there is a simple fix, or whether it is fatally flawed. (The following
"proofs" use a slightly different notation -- one that is easier to
input via keyboard. Hopefully the relation between the two notations
will become clear from the context.)

```
1   (1) p&q     A
1   (2) p       1 &E 
1   (3) q       2 &E 
    (4) p>q     2,3 CP
```

```
1  (1) q     A
2  (2) p     A
1  (3) p>q   2,1 CP
```


**Exercise** Which of the following proofs with or-elimination is
correct? If a proof is not correct, explain what is wrong with it, and
say whether there is a simple fix, or whether it is fatally
flawed. (The following "proofs" use a slightly different notation --
one that is easier to input via keyboard. Hopefully the relation
between the two notations will become clear from the context.)

```
1  (1) p|p    A
2  (2) p      A
1  (3) p      1,2,2,2,2 |E
```

```
1   (1) p|q    A
2   (2) p      A
3   (3) q      A
2,3 (4) p&q    2,3 &I
2,3 (5) p      4 &E
1   (6) p      1,2,2,3,5 |E 
```





