---
title: "logic precept 4"
author: Hans Halvorson
---

# Introduction 

Today we develop a different approach to looking at (formal)
arguments. Many of you will already have heard about the notion of a
truth table. What you might not have heard is how truth tables are
related to proofs. We will postpone the deeper conceptual issues until
next week. But this week we will see how to write the joint truth
table for $n$ sentences, and how to interpret the resulting output. We
will then talk about some short-cuts that one might employ -- rather
than writing out a full truth table. In practice these short cuts can
be crucial, as writing a full truth table is incredibly inefficient
for more complex sentences. What's more, writing a full truth table is
a completely mindless (algorithmic) process, whereas there are other
methods that involve interesting strategies. (For you COS people: we
are touching here on the infamous P=NP problem, which is,
unfortunately, too advanced to talk about explicitly in this course.)

# Truth tables

Let's first recall the truth tables for the connectives. 

| P   | ¬P |
|-----|----|
| T   | F  |
| F   | T  |

| P   | Q   | P ∧ Q |
|-----|-----|:-----:|
| T   | T   |   T   |
| T   | F   |   F   |
| F   | T   |   F   |
| F   | F   |   F   |

| P   | Q   | P ∨ Q |
|-----|-----|:-----:|
| T   | T   |   T   |
| T   | F   |   T   |
| F   | T   |   T   |
| F   | F   |   F   |

| P   | Q   | P → Q |
|-----|-----|:-----:|
| T   | T   |   T   |
| T   | F   |   F   |
| F   | T   |   T   |
| F   | F   |   T   |

| P   | Q   | P ↔ Q |
|-----|-----|:-----:|
| T   | T   |   T   |
| T   | F   |   F   |
| F   | T   |   F   |
| F   | F   |   T   |

The bad news is that you just need to memorize these. The good news is
that once you write circa 10 truth tables, you will automatically
memorize them.

The typical task is to write a truth table for $n$ sentences. To do
that, we simply write the sentences together on a line, leaving some
space to the left. On the left, we then add columns for each of the
*atomic sentences* that occurs in these sentences. Then we write out
all possible combinations of assignments of truth values to those
atomic sentences. One easy way to make sure to capture all of them is
to list the atomic sentences in alphabetic order. Then write T in the
first $2^{n-1}$ rows under the first letter, and F in the subsequent
$2^{n-1}$ rows under the first letter. (That makes for a total of
$2^{n-1}+2^{n-1}=2(2^{n-1})=2^n$ rows.) Under the second letter, write
T in the first $2^{n-2}$ rows, and F in the next $2^{n-1}$ rows, then
T in the next $2^{n-2}$ rows, then F in the last $2^{n-2}$ rows. If
you continue with this procedure, then under the last atomic sentence,
you will alternate between T and F. 

Now the tedium really begins. If you want to write out every single
detail, you can now proceed to copying those Ts and Fs under the
atomic sentences as they occur in the original sentences. Then you
proceed outward, assigning T and F to the Boolean combinations of
things that you have already assigned T and F to. (If you are a visual
thinker, you might be able to imagine that T and F are flowing down
the branches of the parse-tree of the sentence, following the rules
given by the truth tables.)

**Exercise.** Write a full truth table for $(P\wedge Q)\vee (\neg
P\wedge \neg Q)$.



**Exercise.** Write a full truth table for $(P\wedge Q)\vee \neg (P\to
Q)$.

**Exercise.** Write a full truth table for $(P\to Q)\to R$.


# Sentence structure 

Each sentence of proposition logic is either atomic, or it has a
**main connective**. This main connective is the last connective that
is added in the construction of the sentence --- a notion that can be
defined more precisely than we have so far. It can be a good idea,
when you are writing a truth table, to circle or highlight thex column
under the main connective so as to be clear about the meaning of the
truth table.

**Exercise.** What is the main connective of each of the following
formulas?

1. $\neg (P\to Q)$

2. $\neg P\to Q$

3. $\neg (P\to \neg Q)$

4. $(P\wedge Q)\vee \neg (P\to Q)$

5. $((P\to Q)\to P)\to P$

## Parse trees

![](tree.jpg)



# Aside for programmers 

A truth table for a sentence is a completely explicit representation
of the values of the set of all truth functions as applied to that
sentence. Given a list $\Sigma$ of propositional constants, a truth
function on $\Sigma$ is just an assignment of T and F to all the
elements in $\Sigma$. Such an assignment then extends naturally to all
sentences built out of the propositional constants in $\Sigma$.

We could tighten up this definition by first defining the type `WFF`
of well-formed formulas of propositional logic. Here's what the
definition of such a type might look like in the Haskell programming
language:

```haskell
data WFF
    = Var String         -- A propositional variable
    | Not WFF            -- Negation
    | And WFF WFF        -- Conjunction
    | Or WFF WFF         -- Disjunction
    | Imply WFF WFF      -- Implication
    | Iff WFF WFF        -- Biconditional (if and only if)
```

Here's an example of a WFF.

```haskell
exampleWFF :: WFF
exampleWFF = Imply (And (Var "p") (Not (Var "q"))) (Or (Var "r") (Var "s"))
```

This example is clear for a computer, but less clear to a human
eye. We prefer to see something like $(p\wedge\neg q)\to (r\vee s)$.

With the type `WFF` defined, we can then define a type
`TruthFunction`, which uses a type `Env` as an auxiliary. (An
Environment is essentially a truth-valuation, i.e. an assignment of
truth values to atomic sentences.)

```haskell
type Env = [(String, Bool)]
type TruthFunction = Env -> WFF -> Bool

eval :: TruthFunction
eval env (Var x) = case lookup x env of
                    Just val -> val
                    Nothing -> error "Variable not found"
eval env (Not wff) = not (eval env wff)
eval env (And wff1 wff2) = (eval env wff1) && (eval env wff2)
eval env (Or wff1 wff2) = (eval env wff1) || (eval env wff2)
eval env (Imply wff1 wff2) = (not (eval env wff1)) || (eval env wff2)
```

Here `eval` is defined recursively. For example, to determine the
truth value of `(And wff1 wff2)` it gets the truth value of `wff1` and
the truth value of `wff2` and applies the `&&` operation to those
Boolean values.

While we're at it, we can define a function that takes a WFF as input
and returns its **main connective**.

```haskell
mainConnective :: WFF -> String
mainConnective (Var _) = "Variable (no connective)"
mainConnective (Not _) = "Not"
mainConnective (And _ _) = "And"
mainConnective (Or _ _) = "Or"
mainConnective (Imply _ _) = "Imply"
```

The way that WFFs are defined in Haskell makes it easy to read off the
main connective, since it's simply that last constructor that is
applied in the definition of the relevant WFF. For us human beings, we
read strings of symbols, and we somehow -- with practice -- develop
the ability to transform this string into a data structure in our
minds. (We are "parsing" the string.) From this data structure in our
minds, we then "see" what the main connective is. 

One can define an algorithm that takes as input a string, and returns
the main connective (if that string represents a wff). However, this
kind of algorithm is usually pretty ugly, and it's certainly not
something that one recommends students to explicitly follow to find
the main connective of a wff.


# What do truth tables mean?

## For a single sentence


There are only three ways that the truth table of a single sentence
can turn out. The column under the main connective can have:

1. All T, in which case we say that the sentence is a **tautology**.

2. All F, in which case we say that the sentence is an
**inconsistency**.
   
3. Some T and some F, in which case we say that the sentence is a
**contingency**.



Suppose that you are asked to determine if a sentence is a tautology,
inconsistency, or contingency. This kind of problem can always be
answered by writing out a full truth table (and reading off the data
under the main connective). However, sometimes you can solve the
problem more quickly than that --- and in a more satisfying way. For
example, suppose that $A$ is some extremely complicated sentence, and
that $B$ is false on at least one line. Then $A\wedge B$ cannot be a
tautology, no matter what truth values $A$ can take on. Let's look at
a couple of examples.

**Example.** Classify the sentence $P\leftrightarrow (Q\wedge \neg R)$
as tautology, contingency, or inconsistency.

```
It's easy to see that this sentence can be true: when P and Q are true
and R is false, then the sentence as a whole is true. Similarly, since
we can just change the truth value of P to false, this sentence can
also be false. Therefore, this sentence is a contingency.
```

There are more sophisticated, and systematic, ways of doing what I
just did. But for now, I'll just state a few rules of thumb:

1. It's easy to check that a conjunction is false, because you only
need to find a case where one of its conjuncts is false. 

2. For the same reason, it's easy to check that a disjunction is
false.

3. The only way that a conditional can be false is when its antecedent
is true and its consequent is false.

4. The more practice you get, the more quickly you will be able to
identify standard tautologies and inconsistencies. You will also
become more proficient at recognizing logical implications. 
   

**Exercise.** Classify the following sentences as tautology,
inconsistency, or contingency. 


1. $P\vee \neg P$

2. $(P\to \neg P)\to \neg P$

3. $(P\to Q)\vee (Q\to P)$

4. $(P\wedge (Q\wedge \neg R))\vee (\neg P\wedge (\neg Q\wedge R))$

5. $(P\leftrightarrow Q)\leftrightarrow R$

6. $((P\to Q)\to P)\to P$


**Exercise.** Show that if $B$ is a tautology, then $A\wedge B$ is
logically equivalent to $A$.

**Exercise.** Show that if $B$ is an inconsistency, then $A\vee B$ is
logically equivalent to $A$.


## For $n>1$ sentences

If we now put $n>1$ sentences side by side in a truth table, then we
can answer questions about the *semantic relationships* between those
sentences. For example, if sentences $A_1,\dots ,A_n$ can be true
simultaneously, then we say that they are **consistent**. Similarly,
if $A_1,\dots ,A_n$ cannot be true simultaneously, then we say that
they are **inconsistent**.

For two sentences, $A$ and $B$, we say that $A$ **implies** $B$ just
in case $B$ is true whenever $A$ is. We say that $A$ and $B$ are
**equivalent** just in case $A$ implies $B$ and vice versa. Thus, $A$
and $B$ are equivalent just in case they have the same truth value in
all rows of their joint truth table.

**Exercise.** What is the semantic relationship between $P\to Q$ and
$\neg P\vee Q$?

| P   | Q   | P → Q | ¬P ∨ Q |
|:---:|:---:|:-----:|:------:|
| T   | T   | T     | T      |
| T   | F   | F     | F      |
| F   | T   | T     | T      |
| F   | F   | T     | T      |

These two sentences always have the same truth value, thus they are
logicall equivalent.

**Exercise.** Show that $\neg (P\to Q)$ logically implies $P\wedge
\neg Q$.

```
Suppose that -(p>q) is true. In that case p>q is false, which means
that p is true and q is false. But in the case, p&-q is true.
```


**Exercise:** What is the semantic relationship between $(P\wedge Q)$
and $\neg (P\to Q)$?


**Exercise:** If $\phi\wedge\psi$ is a contingency, then can you say
anything about $\phi$ and $\psi$?

**Exercise:** If $\phi$ is a tautology, then what are the
possibilities for $\phi\wedge\psi$? What are the possibilities for
$\phi\vee\psi$?


## For arguments

An argument consists of $n\geq 1$ sentences: a conclusion, and $n-1$
premises. (Yes, we can also have arguments with zero premises.) We can
set these sentences side by side and build a joint truth table, and
here is how to interpret such a truth table:

1. If, in every row in which all the premises are true, the conclusion
   is also true, then the argument is said to be **valid**.

2. If there is some row in which all the premises are true but the
   conclusion is false, then the argument is said to be **invalid**.
   
If we let $\psi$ denote the conclusion, and $\phi _1,\dots ,\phi
_{n-1}$ denote the premises, then the argument $\phi _1,\dots ,\phi
_n;\psi$ is valid just in case $\phi _1,\dots ,\phi _{n-1},\neg \psi$
forms an inconsitent $n$-tuple of sentences. In other words: the
argument is invalid just in case $\phi _1,\dots ,\phi _{n-1},\neg
\psi$ is consistent, i.e.\ there is a row in the truth table in which
they are all true. Such a row of a truth table is called a
**counterexample** to the argument's validity.


**Exercises.** Determine whether the following arguments are valid or
not. Explain your answer by showing the existence of a row of a truth
table, or by pointing to a full truth table, or something of the
sort. Your answer should be articulated in English prose so that it
can convince anyone else who is familiar with truth tables.

1. $P\to (Q\to R)\:\vdash \: (P\wedge Q)\to R$

2. $P\to R\:\vdash (P\vee Q)\to R$



# Philosophical issues

Our target in this course is the notion of logical validity. But we
now have *two* different explications of this concept: one in terms of
provability, and one in terms of semantics (truth tables). Is one of
these two notions more basic than the other? What does it *really*
mean to say that an argument is valid? 




# Extra credit (fun)

1. How many possible truth tables are there for sentences that contain
only the atomic sentence $P$?

2. For sentences with just the atomic sentence $P$, show that every
truth table is represented by a sentence whose only connectives are
$\wedge$ and $\neg$. 
   
