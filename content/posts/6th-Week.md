+++
date = '2026-03-17T08:59:32Z'
math = true
title = '6th Week'
+++

# Implementing the Fuss-Free hierarchy

I have been continuing my implementation of the fuss-free hierarchy this week, 
Last week, I added synthesis rule for Pi and U, but that is not necessary if we write another function 'checkTy' which corresponds
to a new judgment in the bidirectional typing algorithm, which checks a term against Type. We can also add an optional size to 
this judgement, which tells the elaborator to check it against $Small_i$ and produces a small type. I have implemented all of that,
and it seems to be working! I still need to put my implementation to more tests though.

For the moment, I allow coercions from universes only when the 'cast' keyword is written by the user, keeping in mind that this would 
be needed when adding unification later. However, when we need to check a term against a universe level, and that term is not inferable,
then we are not allowed to cast it directly (because the casting infers the universe level to proceed to the casting...). Hence, we may 
introduce syntactic sugar propagating the cast inside the term, for product type it would look like :
\\[ cast ( (x:A) \rightarrow B \rightarrow C) = (x:A) \rightarrow cast B \rightarrow cast C \\]

# Normalisation

I have clarified my gluing proof from last year, detailing explicitely every computability strucutre and making sure that
everything is "internalised" in the right way. Now it would be a lot easier to rewrite the proof in terms of the sconing of
Bocquet et al.

For instance, to solve the issue I had with propagating the decoding inside the term 
the solution of putting the normal form of the decoding inside the computability structure of $U_n$ allows to define the normal form of
the decoding "inductively" when defining the structures of the codes and lifts. We also need to add the normal form of the lift in the 
computability structure of $U_n$, as we encounter the exact same issue. 

Therefore, this makes my gluing proof more precise and rigorous, and I'm confident that it should be directly adaptable to the sconing.

# Reading about patterns

I have been reading the papers of McBride on patterns *The view from the left* and *Elaborating inductive definitions*. This has been
really interesting, and I have now a more clear understanding of the issues pointed in the blogposts. I still need to read more about
pattern unification without $K$ and nested pattern unification to see how everything plays together.
