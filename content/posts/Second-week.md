+++
date = '2026-02-15T18:03:24Z'
title = 'Second Week'
math = true
+++

# Elaboration of the universe hierarchy

When elaborating the "fuss-free" universe hierarchy, we need a mode switch for checking neutral types against
the smallness judgement. This might cause unexpected issue to have two mode switch, and will not be well-behaved
with unification and sub-typing (just like the issue for the algebraic hierarchies).

Hence, we need to introduce casts to tell the type checker to try to lift to another universe instead
of trying to unify something. Also, from the elaboration perspective, the "fuss-free" hierarchy is not of a great
help after all. The smallness judgement and code for type connective can be elaborated easily but we have to much
downsides with the smalness judgement needing a mode switch and being not needed anyway.

Still, the new formulation of the hierarchy allows the Kernel not to have to deal with the code for type connectives or lifts
and their relations.

I formulated the new elaboration with the new casting judgement, but I still need to make sure that everything works
well and provide examples for the elaboration. I could probably try to prove some kind of soundness result, even if this would not
be something really important as it only a safeguard stating that we are not doing something which makes absolutely no sense. Hence,
I think that I will be first trying to provide helpful examples that also accounts for the relation between casts and unification. 

# Equivalence between Fuss-Free and Tarksi 

This week, I focused on the expressiveness of the "Fuss-Free" hierarchy and studied how it
relates with a more classical Tarski system with enough equations.

I showed that you can define codes for type connectives and lifts such that all the
coherence rules are derivable from our "Fuss-Free" formulation, proving in the same time that it is as expressive as the
Tarski theory.

Conversely, we can show the injectivity of the decoding map for the Tarski hierarchy, by mean of an
Artin glueing argument and a structural induction. This is really promising to finish the proof of 
syntactic equivalence between the two formulations. Indeed, we would want to define $Small_i A := \Sigma_{a: U_i} (El_i(a) = A)$ and
define the coding function, given $A$ such a small type, as this witness $a$ : $code_i (A) := a$, such that this satisfies $El_i(code_i(A)) = A$.

However, it occured to me that we can't define $Small_i$ like this as we can't "prove" a definitional equality internally,
nor formulate the sentence "there exists a term a such that $El_i(a) = A$". Hence, I wonder how we would really formulate the smallness
proposition. I had thoughts about using an equivalence of type in the definition : $Small_i A := \Sigma_{a: U_i} (El_i(a) \simeq A)$. However,
I think that assuming univalence we could prove directly that this defines a proposition without having to use the injectivity of the decoding map.

So, this must not be the right way to define the smallness judgement, but to me we can't really express the definitional equality like this. Maybe
there is something I am missing there.

However, this thought made me realise that having a univalent universe can be formulated as having a kind of "propositional injectivity" of the decoding map.
I don't know if this is interesting or not, but there is this kind of duality between the syntax and the univalence principle that we are making with
our formulation : making the decoding map both injective propositionally and definitionally.

# The semantics 

The fuss-free hierarchy could have really interesting consequences regarding the semantics, and could be a way to get rid of all the issues
regarding the type connectives and their coherence in the topos semantics, which caused the need for the realignement property.

In the semantics, I tried to state injectivity of the generic family and found interesting remarks in the original paper
of Streicher, where he considers a "classifying family" which verifies a stronger form of injectivity : $El_i(a) \simeq El_i(b) \implies a =_U b$. 
A classifying family is defined just like the generic family, but we ask that the cartesian map $f \rightarrow \pi$ is unique. 
However, this strong property is not even verified in Set, unless we admit the axiom of choice, and I don't think that it can be preserved by
taking things up to presheaves. The main issue is that we have many choices of equivalent presheafs $F$ induced by $f$.

However, the definition of the generic family requires the existence of a cartesian map $q: f \rightarrow \pi$ for all map $f \in \mathcal{S}$. This translates
to the isomorphism $f \simeq q^* \pi$, and this is not an equality like what we had in the syntax. Maybe this has something to do with the previous discussion
on the definition of $Small_i$ in a Tarski theory where I had issue stating the definitional equality. At the moment, I don't know how all this should really
work, and need to clarify all those things.

To state proper definitional injectivity, we need to interpret the codes in a top universe. I will have a look at the local universe construction from
Lumsdaine and Warren during next week, and see if we could hope to have injectivity for this construction.
