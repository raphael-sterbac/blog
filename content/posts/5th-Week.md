+++
date = '2026-03-10T09:44:43Z'
title = '5th Week'
math = true
+++

# Implementing the Fuss-Free hierarchy

I have been tinkering with implementation a bit this week, reading Andras Kovacs elaboration zoo code and trying to
understand bidirectional elaboration and evaluation in practice. This lead me to try modifying his implementation of 
implicit cumulative universes to work with the Fuss-Free hierarchy in the core, thus elaborating the implicit user syntax
to the fuss-free hierarchy.

This was simply an implementation of the elaboration rules I previously wrote on paper, but I got to see how this would 
work in practice. For example, in the practical implementation, it appears that a synthesis rule is needed for Pi and U, to
infer types in things like : 'let f : U 1 -> U 1 = \\A. A', where we need to infer the universe level of 'U 1 -> U 1'. To do this,
I wrote infer rules giving the code of the corresponding type in the smallest universe possible. However this is only needed  
for the 'let' case, so maybe this is ok.

# Normalisation

I wanted to clarify the need for [StrictLift] to show [InjEl] using the gluing technique. In fact, I think
normalisation would still go through, even if it would lead to quite strange normal forms. The issue appears
when we try to prove the injectivity of the decoding map by an induction on the normal form of the code. Without
the strictness of the lifts, those "normal" forms can be quite degenerate, and it is important to emphasize that there
*every* functoriality and naturality rule should play some role (as part of the normalisation process or the induction).

Therefore, it will be important to comment this and write this induction proof down clearly. I've done that in my notes,
but I still need to work more on the gluing argument itself. In my previous internship, I had a bit overshadowed the topos or
internal language part of the gluing argument, and thus I am currently reading more about it with Jon's thesis and the new technique
of Bocquet, Kaposi and Sattler.

# Thinking about the semantics of the fuss-free hierarchy

We've seen over the past few weeks that injectivity would not likely be an improvement on the semantics side. However, 
I have been thinking about the interpretation of the Fuss-Free hierarchy as a way to understand it better. For example,
we have seen last week that thinking about the small fibrations classified by a universe was not exactly the good way 
to think about it, even if there is a striking resemblance. This is due to the "strictness" issue when we interpret decoding
with pullbacks, we get only things up to isomorphism.

I've been thinking a bit, and if I get it right, being Small in our syntax would correspond to being a display map
(as in being one of the chosen "canonical" pullbacks $p_A$) in the model. This is due to the
fact that we can't deduce : \\[ A \  Small, \   A \cong B \implies B \  Small\\]
Otherwise $Small$ would be interpreted as the
whole class of small fibrations. Hence, in that sense, the injectivity of the decoding map would amount to say that \\[p_A = p_A' \implies A = A' \\]
which is already way more reasonable than asking the uniqueness of the bottom pullback map for any fibration.

This is only thoughts of course.
