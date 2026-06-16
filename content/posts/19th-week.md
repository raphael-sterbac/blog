+++
date = '2026-06-16T13:33:12+01:00'
math = true
title = '19th Week'
+++

# Refactoring my implementation 

Last week, I have continued working on my implementation, and this is now at a quite good stage. Notably, the source files are now structured
and not monolithic as before, and I tried to refactor a bit my code so that it is more readable. I still have a few TODOs notably regarding the dataypes elaboration, for things
that I am a bit unsure of, or that can probably be simplified. In fact, as this is the first time that this has been concretely implemented (and also the first
time I implement such a big piece of type theory!), the code could surely be done in a better way. So this is not quite finished yet, but I am still quite happy with what the current result!

# Writing the paper

I have also been at work on writing the paper last week, and did many changes to the last section. Notably, I inverted the
two subsections on elaboration and evaluation, as it would make much more sense to talk about the latter before discussing type-checking.
I also added many definitions that were missing, such as de Bruijn levels and indexes, environments etc... This section is probably still perfectible
but the full picture has now been written down. 

Now that this is slowly coming together, there are a few questions that I was asking myself regarding the scope and directions of the paper. 

- Should we include a subsection on the implementation of Fuss-Free datatypes ? 
- Should we move section 5,6,7 before section 4, or before ? So that the reader is presented first with syntax and implementation before the difficult metatheory.
- If so, maybe we should also move section 2.3 and 3.1 together with section 4 ?
- Should we include universe polymorphism ? If so, I think that the relative induction principle is not the difficult part, and its proof would be in appendix ?

# Writing the draft for cumulativity in $\infty$-toposes

In the meantime, and in the evenings, I have been working on the draft of my idea for adapting the ideas of
the paper "Strict universes for Grothendieck toposes" to the construction of Schulman in $\infty$-toposes. This is also
starting to get in pretty good shape and should be enough to have a good overview of the approach. Most of the proofs 
of the results of the two papers that I need are left blank for now, but I gave a more precise version of the construction of
Schulman, and constructed the appropriate monomorphisms between the universes. 
