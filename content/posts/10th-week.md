+++
date = '2026-04-14T10:17:24+01:00'
math = true
title = '10th Week'
+++

# Elaboration of cumulative universes

This week, I have been reviewing the rules I had written a while ago for the elaboration to the Fuss-Free hierarchy. Those
rules had evolved quite a bit over the past few months, as we introduced an explicit casting mechanism to get rid of the problems
related with unification. However, now that we went back to a system with no explicit casts, and with the experience of implementing
the elaboration in practice, I think that we needed to revisit the rules. 

Indeed, because of the explicit casts, we had decided not to bother with judgements like \\[ \mathsf{Small}_i \ni A \rightsquigarrow A'\\]

and to only work on the universes. For instance, we would directly elaborate to the code of a dependent product like this: \\[U_i \ni \Pi(A,B) \rightsquigarrow \pi^i(a,b)\\]

where $\pi^i$ is a notation for $\mathsf{Code}(\Pi(\mathsf{Decode}(a), \mathsf{Decode}(b)))$. However, when we implement the thing in practice, we need to deal with things
like the let binding, for which we need a CheckTy judgement, which checks a raw term against $\mathsf{Type}$. If we have to write such a function anyway, we should take advantage
of it and add an optional parameter $i$ which correspond to checking against $\mathsf{Small}_i$, or $\mathsf{Type}$ (alternatively, we can see $i$ as in the type of level extended
with a top element, and that makes all the condition involving $i$ to work out of the box).

Then, the rules of CheckTy adapts rather directly to that new size parameter, which correspond
in the end to our judgement $\mathsf{Small}_i \ni A \rightsquigarrow A'$. Now, we can take advantage of this with a rule : \\[U_i \ni A \overset{\mathsf{chk}}{\rightsquigarrow} \mathsf{Code}(A')\\]
when $A \overset{\mathsf{chkty}}{\rightsquigarrow}_i A'$.

Funnily enough, this is what I had implemented, and this seems to work quite well and to be simpler! I have written all of this properly 
using bidirectional rule in the style of *cosmology of datatypes*, and started to sketch the "lower-level" explanation. Also, I tried
to write a remark on the interplay with unification, by citing Andras' talk at WITS26 and work on heterogeneous unification. Indeed, the latter
was already the conbination of a homogeneous unification problem with a coercion, which in their case is OTT coercion. Hence, our proposal
correspond at generalising that coercion to allow lifts (i.e. cummulativity). I think that this is a good perspective, and I also cited AdapTT, which
makes the parallel between OTT coercions and sub-typing.

# Reading some papers

This week I've read most of the paper *Implementing a modal dependent type theory*, mainly to have an idea of how 
to write a description of an elaboration algorithm and its implementation. But the content was really interesting as well, as
I was not that familiar with modal type theory, this was a good introduction which made me want to learn more about it. I'll surely
have time for that in Aarhus is summer !

I've also been reading about patterns, and trying to get used to Pterodactyl's codebase (there's a lot to digest!). That is
a really instructive experience, and I am feeling more an more confortable with concrete implementation of proof assistants.

# Cummulativity in toposes

As a bit of a side-thing, I started writing down properly (i.e. in latex) my proof sketch for cummulativity in $\infty$-toposes. I figured
out some details that were bothering me. Those were due to the bicategorical nature of Mike Schulman's construction, something I am not particularly
used to. However, it seems like there is nothing complicated there in the end, and I think that everything works out (quite surprinsingly?) easily, unless
I am wrong somewhere. I will try to finish writing this down, but this takes quite some time if I want it to be somehow self-contained, or at least
to a certain extent.

# Preparing for my Sandwhich talk

Also, this weekend I have been writing slides and preparing for my Sandwhich talk of yesterday, on work
from my last year internship with Thierry Coquand. I learnt a lot
by doing this, and had a lot of fun! Especially, this was a good practice run for Types (even if the format is completely different). 
