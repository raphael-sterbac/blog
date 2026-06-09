+++
date = '2026-06-09T09:22:39+01:00'
math = true
title = '18th Week'
+++

# Implementing Datatype Descriptions

Other the past week while I was in Denmark, I continued my implementation of Dagand's datatype descriptions and I managed to end up with something
that seem to be working ! It allows the user to write code like this:

```
data Nat : U 0 where {
  zero : Nat ;
  succ : Nat -> Nat
} ;
```

that gets elaborated in terms of Dagand's descriptions, extension functor etc... It also generates the eliminator such that you can write recursive programs like this:

```
let add : Nat -> Nat -> Nat = \a b.
  elimNat (\_. Nat)
    < \p ihs. b ,
    < \p ihs. succ (fst ihs) ,
    * > >
    a ;
```

As expected, this was quite tricky, and I am still debugging things notably with how universe levels are handled. In fact, I made the sort of types representable just like in Pterodactyl,
allowing the user to write large inductives with `Tp` everywhere instead of `U i`. For instance we can write code like this:

```
data Nat : U 0 where {
  zero : Nat ;
  succ : Nat -> Nat
} ;

data List (A : Tp) : Tp where {
  nil : List A ;
  cons : A -> List A -> List A
} ;

let TypeList : Tp = List (U 0) ;

let types1 : TypeList = cons (U 0) Nat (nil (U 0)) ;

let types2 : TypeList = cons (U 0) (List Nat) types1 ;

let getHead : TypeList -> U 0 = \l.
  elimList (U 0) (\_. U 0)
    < \p ihs. Nat ,
    < \p ihs. fst p ,
    * > >
    l ;

let mySmallList : getHead types2 = cons Nat zero (cons Nat (succ zero) (nil Nat)) ;
```

I have implemented the smallness check in terms of the extension of the description, though I am not sure that
this is the right way to do it for a practical implementation. It may be better to check smallness recursively on the description, I am not sure. In either case, what I implemented seem to be
working quite well, and I have several working examples along with a few non-examples. I have even tried the implementation to do a tiny bit of category theory using inductives with one constructors
in place of proper record types, and it seems to be working.

# HoTT/UF and Writing the paper

Last week, I also gave my talk at HoTT/UF and I think that it went quite well ! The feedback were quite positive,
and was mostly consisting of "this is a good approach, I wonder why nobody presented universes like that before !". 

One of the most important question I have got was if the approach relates to the new implementation of universe polymorphism
implemented in Rocq, based on the paper of Bezem, Coquand, Dybjer and Escardo. Of course our approach is perfectly compatible 
to this work (actually we prove normalisation for it and use level judgements like they do !). I think that I did not put enough
emphasis on this in my presentation but we should do so in the paper, and mention that this approach has been implemented in Rocq
recently. I need to get back to writing, now that I have taken a step back and have a better idea of the global picture, with the implementation
now being at a good stage.

Another fun thing was that the [next talk](https://hott-uf.github.io/2026/abstracts/HoTTUF_2026_paper_10.pdf) after me was about formalising category theory in Cubical Agda and faced many issues related to levels
and universe polymorphism. Actually the talk even cited the original blogpost on Fuss-Free hierarchies ! This is the second time that this happends, with Owen Lynch also using the Fuss-Free approach in some way.
He even expresses it in terms of modalities, described in his [slides](https://types2026.cse.chalmers.se/slides/34/7.html). I do not know if this formulation gives anything interesting, but it might be worth looking at.

Actually, I have been recently wondering if it would be possible to express the Fuss-Free hierarchy as a kind of reflective localisation of the universes, which might be related to a formulation in terms of a modality. More concretely,
the pair of the coding and decoding map looks like the adjoint functors of a reflective localisation, and the decoding map "localises" the universes in the sense that it sends lifts to equal types in a natural/functorial way.

