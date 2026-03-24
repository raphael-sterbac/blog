+++
date = '2026-03-22T16:33:36Z'
title = '7th Week'
math = true
+++

# Formulating natural universe hierarchies

I've been working on finding a concise way to formulate the *natural* universe hierarchy,
such that all the structural rules follow from functoriality and naturality condition. The idea
is to work in a logical framework to specify the signature of our theory in a categorical way. This
was a lot of fun ! Maybe there are also interesting ideas to get from the paper *A Generalized Algebraic
Theory for Type Theory with Explicit Universe Polymorphism*, that I should probably try to read at some point.

In the end, the formulation is quite concise : our universe hierarchy is a functor from the category of levels $\mathbb{L}$ to
the "polynomial category" associated with our representable map $\pi : \mathsf{Tm} \rightarrow \mathsf{Ty}$. Then, codes $\Pi^\bullet$ and $u_\bullet^\bullet$
are simply natural transformations between well-chosen functors that embeds their input. With this, we recover the structural equations
by unfolding the definition : we get a map along with a coherence diagram and a naturality diagram.

I think this is quite nice! Now I could start thinking on how to formulate the Fuss-Free hierarchy 
in this way, or also try to phrase the Sconing proof for normalization.

# Postponed casts and unification  

This week, I've also been thinking about handling implicit coercions and unification properly. The heart of 
the problem is *scheduling*: making progress on unification can solve a postponed coercion problem, and vice versa.
Andras Kovacs last talk at WITS 2026 present an algorithm that aims at handling more of those postponed unification problem,
using ideas from observational type theory.

That is already a step towards a more reliable unification, but it would be still unreliable when coupled with implicit coercions.
One idea is that instead of having conflicting coercion *and* unification mechanism, we would want to have only one algorithm to handle
both at the same time.

I think that this idea is also related to the paper "AdapTT: Functoriality for Dependent Type Casts", which presents a unified framework
for *both* subtyping and OTT's coercion mechanism! Then, one good idea would be to generalise Andras' algorithm to produce general *coercion problems*,
which would try to coerce from one type to another (using cumulativity/subtyping), and inferring more information on the structure of the type we are
coercing. This process should ultimately produce a unification problem if such a coercion couldn't be found.

I was also re-reading the related post on this topic, and came across this previous post on Mastodon:

>   1. *Types* should not be subject to unification, but rather to resolution of coercions. 
>   2. *Terms* are subject to unification.
>
>   Of course, many types are of the form el(A) when A:U is a term of universe type. The principles above give us a pretty simple rule of thumb: the coercions from el(A) to el(B) for neutral A and B must always be identities, induced by a definitional equality between A and B. This means, in short, that we should call the unifier HERE but NOT when A,B are headed by a constructor. 

This is quite funnily related to our Fuss-Free hierarchy and its injective decoding map ! I'm still unsure of what to say from all of this. But to me, 
the fact the core of the problem is *postponing*, and that Andras deal with it using observational equality, which is in the end a casting mechanism, should
indicate that extending the algorithm with a general "adapter" may be a good idea (using AdapTT terminology).

I am not proposing to use full structural and functorial rules such as what is done in AdapTT, and I think this would be dangerous. 
We should restrict ourselves on a casting mechanism which is functorial only on negative types, and surely not on parametrised inductives like list for example.
One question that arises is now : how does that behave with universe hierarchies ? 

To summarize, I think that this is really going in the good direction! We would still need to see how it behaves in practice,
as those posponement issues are hard to evaluate without implementing the thing in a real system. I've started to read both Andras'
and Pterodactyl code, and I will try to start adding this algorithm to my implementation at some point.
