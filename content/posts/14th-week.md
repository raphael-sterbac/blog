+++
date = '2026-05-12T09:39:21+01:00'
math = true
title = '14th Week'
+++

# Writing the paper 

I have started writing the extension to other types for the elaboration section, starting with 
sigma types and lists. I am not sure how to continue after this, an approach could be to use the W-types
encoding to have a simple presentation, but with this approach we do not bring home the main advantage of the 
Fuss-Free presentation, which can deal with user-defined inductives in all generality. The issue is that introducing
a theory of signatures and everything would take too much space, and diverges from the point we are making at presenting
a simplifying approach. Maybe presenting the example of W-types formally and then discussing informally a more general approach
to inductive types would be a good balance ?

# Conor's Adapters

Thanks to discussions with Thiago Feliscimo and Meven Lennon Bertrand at TYPES, I have realised that the
coercion operation triggered on our mode switch rule is *exactly* what the original notion of an adapter is,
from Conor McBride's TYPES21 abstract entitled "Functorial Adapters".

In our setting, we only ask for functoriality on negative types to preserve a good behaviour with unification, but we could easily extend this operation to have 
functoriality on more types ! This is exactly what the paper "AdapTT: Functoriality for Dependent Type Casts" does, but the machinery
is quite complicated. I have tried to see if the Fuss-Free hierarchy would help in any way, but this is not likely, and I think rather
orthogonal.

Basically, what we would need is a new rule for `coe` that propagates the coercion functorially on the arguments of an inductive. The paper of Adjedj et al. deals
with the really general case of a any functorial casts, but here our coercions are only a meta-operation that will be implemented as a function during elaboration, so maybe
there is still something to say there. For instance, when writing the functoriality rules for lists, we get a "directed" version of the rules they derive :
\\[ \mathsf{coe}\ \mathsf{nil}_A : A \Rightarrow B \rightsquigarrow \mathsf{nil}_B \\]

Anyway, I think this is still quite interesting and the fact that all those work are somehow interconnected is reassuring : we probably went in a good direction!

# Continuing implementation

This week, I will continue working on implementation, both on my local branch of Pterodactyl and on my
proof of concept implementation of the Fuss-Free hierarchy.

# Types

Last week, I was at TYPES in Gothenburg and this was a lot of fun! I had great discussions regarding my work with Thierry from last year, and my talk went (I think)
pretty well. The talks were overall very interesting and this was also a good experience to have a more global view of what is going on in the field
of type theory.
