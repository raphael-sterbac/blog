+++
date = '2026-06-23T10:52:01+01:00'
math = true
title = '20th Week'
+++

# Normalisation for explicit universe polymorphism

I drafted the proof for normalisation of a theory with universe polymorphism. I am not quite there yet, but I think that what I have written now
should the right thing to do. The notations are a bit shaky and the proof of the relative induction principle is not very precise (but to be fair, the ones in the original paper are not much more detailed...), but with a bit
more work this should be in a good shape. 

There are still a few things were I am a bit uncertain though. For instance, should we ask the higher-order level algebra to be a preorder instead of just a set with a zero and successor ? In the current version, the ordering for levels does not really appear, 
so I wonder if there is something wrong.

# Exploring applications and examples

I have been thinking about finding relevant applications and examples for the smallness of datatypes and records. Of course, category theory
is the primary example that comes to mind, because there are a lot of universes involved. For category theory, the main sources of reference that I found
were the paper "Category theory in Coq 8.5" by Timany and Jacobs, and the paper on universe polymorphism by Timany and Sozeau.

The Agda-Unimath library is also a good reference, and the common thing between all of these is that they define categories with universe levels in the definition. There, doing things at the top
universe and then specialising to small things is of course quite compelling, but for this we actually need a smallness judgement on record types.
This judgement should check that each of the fields of the record are small. In particular, this coincides with the smallness judgement for the encoding of records through Sigmas and Unit types. Hence, we can add a new syntactic 
construction `R @ i` which forms the product with the smallness judgement at level i, so that we are only enable to inhabit this type with something that has small fields.

While trying to find relevant examples, I also come across the Choice tree Rocq library (there was a talk at Cambridge the other day on this!), which has faced several universe constraint issues due to the interaction of multiple libraries. 
I think that this is also a good selling point : by moving universe levels from the definition to the instantiation we should improve the interaction between different libraries. But this also made me realise that things like this will not ever be able to be instantiated as small:

```
data ITree (E : Tp -> Tp) (R : Tp) : Tp where {
  Ret : R -> ITree E R ;
  Tau : ITree E R -> ITree E R ;
  Vis : (X : Tp) -> (e : E X) -> (k : X -> ITree E R) -> ITree E R
} ;
```

Because the `Vis` constructor takes a big type. For this, I thought that maybe we could also add a `D @ i` syntax for datatypes that would "downcast"
the signature of each constructor and create a new associated datatype. Concretely, it would look at the type of each constructor and would put `U i` in place of `Tp` and apply the other relevant changes. In this example, it would create the type: 

```
data ITree (E : Tp -> Tp) (R : Tp) : Tp where {
  Ret : R -> ITree E R ;
  Tau : ITree E R -> ITree E R ;
  Vis : (X : U i) -> (e : E X) -> (k : X -> ITree E R) -> ITree E R
} ;
```

Of course, this is done in the core language so we would need to adapt the decodings of `X` among other things. Actually, this looks a bit like a "two-sortification" where we make everything dependent on a universe.
However, this seems quite evil, and maybe we should not try to do that and accept that in this case we would define `X` to be a universe-polymorphic small type in the definition of ITrees. 

# Implementation 

I continued the implementation, and added record types for category theory. However, the implementation is currently quite all over the place because I tried to implement
this downcasting thing, which was quite tricky and lead to many unsound attempts. But I think that I will arrive somewhere, and this downcasting thing is probably a bad idea in any case. 
