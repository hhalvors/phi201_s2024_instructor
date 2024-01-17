---
title: "logic precept 1"
author: Hans Halvorson
---

# Introduction

We have to start this course relatively quickly, which means that the
first precept will cover both general concepts, and the first steps
into our formal system of logic. At the end of this week, you should
be comfortable with the various symbols $\vee ,\wedge ,\to ,\neg$ and
how they work to build more complex sentences. You should also be
comfortable writing simple proofs that involve the intro and elim
rules for $\wedge$, the intro rule for $\vee$, modus ponens, and modus
tollens.

The first part of the precept is primarily qualitative: we take
concepts and words that you already use, and we formulate some more
precise definitions. We don't think that we necessarily have the
"right" definitions of these concepts, or that everyone understands
these concepts in exactly the same way. You might rather think of what
we are doing as establishing conventions for a fruitful discussion.

# General concepts 

## Argument identification 

For each of the following paragraphs: (a) State whether or not that
paragraph contains an argument. (Note: by saying that something is an
*argument* is not saying that it is a *good* argument.) (b) If there's
an argument, identify its conclusion and premises. (c) If there's no
argument, explain what's lacking.

1. Professor Plum was in the drawing room. Miss Scarlet was in the
kitchen.  The murderer used the knife and the evil act was committed
in the hall.

2. If Professor Plum was in the drawing room then Colonel Mustard was
the murderer. Professor Plum was in the drawing room. So, Colonel
Mustard was the murderer.

3. Every student of logic is wise and knowledgeable. Anyone attempting this
exercise is a student of logic. Therefore, anyone attempting this
exercise is wise and knowledgeable.

4. I am absolutely sick and tired of getting wet every time it
rains. From now on I will never forget to take my umbrella with me in
the morning.  Even if the weather looks fine when I leave I will
certainly make a point of taking that umbrella.

5. All human beings are mortal. So, it stands to reason that Socrates
is mortal. After all, he is a human being.

6. Professor Plum was obviously the murderer in this instance. For the
murderer used the knife and Professor Plum had the knife. And the
murder was committed in the hall and Professor Plum was in the hall.

## Charitable reading

I real life, the form of an argument can be hidden by various
rhetorical strategies, or simply because it is assumed that all
parties would agree to some premise (and so that premise is not stated
explicitly). What this means is that a good argument analysis will
often involve some charitable re-interpretation of the precise text
that you have in front of you.

## Short answer

1. What are the components of an argument?

2. Which kinds of sentences can be premises or conclusions of an argument?

3. Is a valid argument necessarily a "good" argument? What might a good
argument have that a valid argument doesn't?

4. What's the point of studying the validity of arguments, as opposed
to their goodness?

5. If an argument has true premises and a true conclusion, then is it
valid?

6. If you disagree with the conclusion of an argument, might you still
say that it's a valid argument?

7. According to the definitions given in lecture, which of the following
sentences makes sense, and which do not?

   a. That's a true argument.

   b. That's a true statement.

   c. That's a valid point.

   d. That's a valid argument.

   e. That's a valid reason.

8. Give an example of a valid argument with false premises and a true
conclusion.

9. Give an example of an invalid argument with true premises and a true
conclusion.

10. True or False. Discuss.

    a. If an argument is valid, then you might be able to make it invalid by
       adding further premises.

    b. You can make an invalid argument valid by removing premises.

    c. If a sentence doesn't follow from another, then its denial must.


# Translation

<!-- Pospesel, Lepore, my own problems --> 

1. Draco will apologize or not get dessert, but he won't do
   both. ($A,D$)
   
2. The Quidditch match will be canceled if it rains, unless the field
   can be magically dried. ($C,R,M$)
   
3. If Taylor Swift expresses support for environmental policies, then
    she will also advocate for renewable energy, unless she
    prioritizes economic concerns. ($E,A,P$)
	
4. If Elon Musk innovates in electric car technology or develops new
    space exploration methods, then he will be recognized as a pioneer
    in technology. However, if he fails to achieve progress in either
    field, he will not be recognized as such. ($I,D,R$)
	
5. If it is not sunny then we will not go to the beach. ($S,B$)

6. Either it's sunny or we will not go to the beach. ($S,B$)

7. We will not go to the beach if it's not sunny. ($S,B$)

8. We will go to the beach only if it's sunny. ($S,B$)

9. It's being sunny is a necessary but not sufficient condition for
    our going to the beach. ($S,B$)
	
10. A society does not have free speech unless it allows peaceful
    protests. ($F,P$)
	
11. Professor Plum is the murderer unless the weapon was a candlestick
    or the crime occurred in the library. ($P,C,L$)
	
12. Professor Plum is the murderer only if the weapon was the
    candlestick and the crime occurred in the library, or the weapon
    was the dagger and the crime didn't occur in the
    library. ($P,C,L,D$)
	
13. Provided, but only provided, that the French Fleet is sailed
    forthwith for British harbors, His Majesty's Government give their
    full consent to an armistice for France. ($S,C$)
	
14. For the tenability of the thesis that mathematics is logic it is
    not only sufficient but also necessary that all mathematical
    expressions be capable of definition on the basis solely of
    logical ones.


# First steps in proving with complete rigor




# Putting it all together

One might imagine the complete process of argument evaluation as
follows: 

1. Translate the argument from natural language into symbolic form.

2. Prove that the argument is valid. Or show that it is invalid --
   something that we don't yet know how to do.
   
3. Pass judgment on the original argument.

Nobody really ever does that, and the process would also have several
pitfalls. One of the main pitfalls is the "false negative", i.e. the
symbolic argument is invalid, but the original argument is valid. In
fact, there are good reasons to think that no rigorous symbolic system
could ever capture all the ways in which a natural language argument
could be valid. So, in the first place, take that as a caution about
the range of our methods.

However, it can still be helpful practice to complete the process
described above. The hope is that with sufficient practice, you will
more quickly see the logical structure behind arguments you encounter
in real life. 

Let's undertake the process on a few arguments.

**Argument 1**

1. If Donald Trump wins the upcoming election, then certain policies
   detrimental to international relations will be implemented.

2. If certain policies detrimental to international relations are
   implemented, there will be an increase in domestic social unrest.

3. Therefore, if Donald Trump wins the upcoming election, there will
   be an increase in domestic social unrest.
   
**Argument 2**

1. Universities should encourage diverse viewpoints and free speech is
essential for exposing students to diverse viewpoints.

2. If free speech is essential for exposing students to diverse
viewpoints, then universities should have policies that protect free
speech.

3. Universities should foster a respectful environment. 

4. Universities should have policies that protect free speech and
foster a respectful environment.
