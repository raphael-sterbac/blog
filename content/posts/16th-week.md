+++
date = '2026-05-26T10:24:43+01:00'
draft = true
math = true
title = '16th Week'
+++

# Implementing Datatype Descriptions

This week, I have been implementing Dagand's datatype descriptions in my minimal implementation of the Fuss-Free hierarchy. This has
been a lot of fun, and I think I have set up evrything so that the last step remaining is the actual elaboration from the inductive definitions
written by the user to the core language with datatypes descriptions. This is described in chapter 7 of Dagand's thesis, but this will be the part
where I need to be a bit careful with the universes. This will be a bit tricky, but with a bit of care I would be able to finish this in a few days
of focusing. 

This implementation has also been a good excuse to read more carefully some part of the thesis I had skimmed before, and this was quite insightful.
I am now wondering why this approach is not more widely known ! Notably, I now think that presenting datatype descriptions internally
could be a good way to go for structural subtyping on inductives. In AdapTT, they have inductives à la Paulin-Mohring and add type variables to the system, which leads to crazy notations.
Meven told me once that he would have wanted to use universes instead of type variables, but that it was a bit tricky (even if I don't remember all the details...).
Maybe Dagand's datatype descriptions are a good way to internalise all of this, and maybe it would enable us to give a simpler description of all the rules for subtyping on inductives. This is just some
shower thoughts, and there is nothing precise in my head yet (and again, things like this may live at the frontier of Russell/Girard's paradox...).

# Writing the paper

I have also been working a bit on the writing of the paper. I notably tried to step back to have a more global view of the paper, our contributions, and their relation to existing approaches. To summarize the contributions are :

- A simpler (and insightful in some way I would say) presentation for structural, algebraic universes
- Equivalence with the *natural* (made precise in a logical framework) universe hierarchy
- Normalisation of a theory with internal universe levels (and universe polymorphism ?)
- Elaboration algorithm from implicit universes to the fuss-free hierarchy, with an actual implementation
- Simpler account for cumulative inductive types (hopefully with also an actual implementation here!)

One thing that I have also realised by reading Timany-Jacobs and Timany-Sozeau is that they insist quite a lot on the theory of categories (which is not even inductive). The reason is that in their framework with no top-level
of types, the theory of categories should be universe-polymorphic from the beginning:

` Record Category@{i j} :=
{ Obj : Type\[@{i}; Hom : Obj → Obj → Type@{j}; . . . }. (* local constraints: ∅ *) `

This means that we are actually only working on small categories, and that small categories are just really *relatively small* categories:

`Definition Cat@{i j k l} : Category@{i j} :=
{ Obj : Category@{k l}; . . . }. (* local constr.: {k < i, l < i, k ≤ j, l ≤ j} *)`

As said in the original blogpost for the Fuss-Free universes, there is really no need for size constraints in the definition of categories... And the most reasonable place where you would need to do so
is when you need to consider the bicategory of categories or things like that... Thus, one other good thing about the fuss-free hierarchy is that we retain the top-level of types, allowing us to write: 

`theory Category where
  ob: Type
  hom: ob -> ob -> Type
  // operations and axioms...`

And then, specify it to the theory of small categories if needed. There, the fuss-free hierarchy does not really play any important role, as we cannot express the theory of small categories in term of the smallness judgement (and shouldn't anyway).
However, this story for categories can also be done for any inductive. For instance for lists: in Timany-Sozeau they only have small lists (for the same reasons) and make them universe polymorphic such that they ask for the equations $\mathsf{nil}_i = \mathsf{nil}_j$ etc..
I think it would nice emphasize that the good thing of our approach is that we are able to define large inductives, and then specialise them to small ones instead of making them universe polymorphic by default (there is the parallel to categories, and mathematical practice).
Our approach would also probably be way more efficient in term of performance, as having levels everywhere which are subject to constraints solving can get quite expensive in resources...

On top of that, I came across a paragraph in Timany-Jacobs that say :
> To solve these problems, explicit lifting functions, e.g., Lift_Ens: Ensi → Ensj
with i ≤ j, could be used. They allow formation of terms such as the en-
semble of lifted small ensembles. However, we can’t prove, or even specify,
Π(t: T), t = Lift_T t. As a result, working with such lifted values and types
depending on them in particular is very complicated. 

Therefore, the fuss-free hierarchy would be a good solution, as it simplifies the complexity of having lists and coherent codes while retaining a structural approach.

# Preparing slides for HoTT/UF

Over the past days, I have also been working on my slides for HoTT/UF. This also relates to the previous section, as I am trying to have a more global view to explain things
and present them well. I will be doing some practice runs this week with Yufeng who is also presenting there. In any case, this will be fun and I hope we will have nice feedback there !

