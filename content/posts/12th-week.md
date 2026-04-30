+++
date = '2026-04-29T22:01:31+01:00'
math = true
title = '12th Week'
+++

# The Fuss-Free hierarchy and more general types

I have been reflecting about the Fuss-Free hierarchy and how to use it on general Inductives, or
even on user defined types. My original idea was to allow the user to do things like $\mathsf{UserDefinedType}(...)@i$ to indicate
that we are asking for the corresponding small type, which we can elaborate in the fuss-free hierarchy by coding and decoding. 
For instance, if we define a type of lists, then $\mathsf{List}(A)@i$ is a small type, given that $A$ is one. Pushing this further,
we can effectively do this for virtually *any* type, and we only have to add the corresponding rule for closure under smallness, which
mimicks the formation rule with the smallness predicate instead of the well-formed type judgement.

This works well, but it might be too rigid for more complicated types. The user might want to have things like $\mathsf{Foo}(A,B)$ which
should be small if A is small at level $i$ and $B$ at every level $j < i$, or something like this. I am currently not sure about all of this, and
I am more and more thinking that this is a notation problem, and is completely orthogonal to the Fuss-Free hierarchy. Also, it might be related to 
universe polymorphism in some sense, allowing to express constraints on generic universe levels like this.

# Reading about patterns and HITs

Since the discussions of my last meeting, I have been reading (again) about patterns, but this time also about Higher Inductive
Types ! Notably, I have read in diagonal the paper describing how cubical Agda deals with higher inductives and patterns on them. This
have been quite interesting.

Also, I have read in "Dependent patterns without K" that they use homogeneous equations instead of the heterogeneous ones of the original algorithm.
I now wonder how this relates to Andras' algorithm on postponed unification, where he introduces OTT coercions one one side of the equation, which is in some sense
a kind of heterogeneous equation. Is this possible that his algorithm depends on axiom K ?

# Going back at implementation

This week I went back to my implementation, while continuing to write the implementation section of the paper.
Notably, I tried to make sense of my abandoned unification tests, and this is quite a mess... This does not matter,
as we decided not to include it in an artifact to keep things as simple as possible, but I wanted to finish the implementation to
make sure I understand it.  

Anyway, I thought it might be a good idea to try to implement it directly in Pterodactyl. I am now quite comfortable with the code, and will try
to do that on a local branch and test it there, also adding proper small types (that seem to have been left as a TODO, unless I am looking at the
wrong place). Indeed, it is quite related anyway as I only need to implement the "coe" or "cast" judgement of the paper.


# Refreshing holidays

Last week I was on holidays, back to my hometown in France, this was really nice to get some fresh
air out of Cambridge's bubble and to take a step back from the internship and my work. Still, I did a bit
of writing there, aiming at getting out a preprint of the work of my previous internship before my talk at Types.
In the end, I don't know if this will be feasible, but at least know I have a *complete* draft of a paper, that
is way better written than my internship report (writing papers is hard!).

Going back, I stopped by Paris to meet Meven there for things related to the work with Thierry as well, and this was
really interesting. Apparently, they are going to try to prove a very similar result to what I have proven to relate
Tarski and Russell universes, but in the general framework of AdapTT. There, the lifting operation would be an adapter $$\uparrow_i^j : U_i \Rightarrow U_j,$$
which satisfies the corresponding functoriality rules of the general framework. Then, you should be able to prove that if $\Gamma \vdash t,t' : A$ and $|t| = |t'|$
then $\Gamma \vdash t = t'$.
