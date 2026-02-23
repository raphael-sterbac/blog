+++
date = '2026-02-23T12:52:43Z'
title = 'Third week'
math = true
+++


# Equivalence between Fuss-Free and Tarksi 

When showing that we can translate from a strict Tarski hierarchy to the Fuss-free
formulation, we can't define $Small_i$ as a proper type internally. To solve this issue,
we can show this direction of the equivalence result by a semantics argument, showing
that the syntactic category with family (CwF) $\mathcal{T}_T$ of the strict Tarski theory
is a model of the fuss-free hierarchy. To do this, we define $Small_i$ as the characteristic
map of the monomorphism $\text{El}_i$. Then, this satisfies the smallness rules of the fuss-free formulation,
and we can define the coding map as a pullback map of the cartesian square defining the characteristic map $\text{Small}_i$.
So now the equivalence result is completely proven!

Also, we can now identify with more clarity the different problems related to universe hierarchies. Notably, our work can
be summarized with the following equivalences:

\\[ \text{[StrictLift, StrictEl]} \Longleftrightarrow \text{[InjLift, InjEl]} \Longleftrightarrow \text{Fuss-Free}\\]

This equivalence result shows that the usual strict Tarski hierarchy is equivalent to our more concise and still
algebraic Fuss-Free presentation. More interestingly, this result legitimates the study of injective (but not necessarily strict!)
hierarchies of universes in (infinity)-topos models.

I also had a quick idea of how this could already be used to justify the Streicher construction for sheafs universes. Indeed,
while sheafification does not preserve realignement, the construction might be enough to present a hierarchy with injective lifts (and decodings).
Indeed, Hoffman-Streicher construction on presheafs preserves cummulativity in the following sense. If we have a sequence of Grothendieck universes
\\[ \mathcal{U}_0 \subset \mathcal{U}_1 \subset ... \\]
then we have a cummulative hierarchy in presheaves, using the functoriality of the defined generic map:
\\[ \mathcal{V}_0 \rightarrowtail \mathcal{V}_1 \rightarrowtail ... \\]

More precisely, this give rise to a sequence of cartesian squares of the corresponding generic maps. This 
argument is given by Awodey in p.11 of "On Hofmann-Streicher universes". Then, I do not see how the same argument
would fail when passing everything to sheafs, as we are only intersecting the universes $\mathcal{V}_i$ with the
sheaf topos, and we consider the generic family $i^* \pi$ which will also be functorial, given that $\pi$ is. Maybe I am
getting something wrong here, and it is only some recent thoughts. 


# On the practical side: a conservativity result 

Our result is interesting, but if one wants to use it practically, then we should provide a kind of conservativity
result that would enable someone reasoning on the strict type theory to relate it to the given models of the weak type
theory.

We can provide a translation from the strict theory to the weak theory given by normalisation, but this result may not be
really interesting in practice as the translation is non functorial and may do "weird" things.

Hence, we can try to find some kind of "homotopical" results stating things such as:
for every weak thing X there is a homotopic weak thing X' where X' is strictly equivalent to X in the strict language

This statement does not seem quite right in this formulation, and it would always hold by taking $X' = X$. I thought that maybe what we want is to characterise a simpler subset 
of "homotopy normal forms" such that we have the following: For every weak thing $X$ there is an homotopy normal form $Hnf(X)$ which is homotopic to $X$, and such that $Hnf(X) = X$ in the strict theory.
Hence, the homotopy normal forms would correspond to the "reflection" of the strict theory inside the weak theory.

Maybe we can simply ask that $x = y$ in the strict theory should imply an equivalence
$x \simeq y$ in the weak theory, and then one could take $Hnf(x)$ to be the image of normal forms, and this would relate to our normalisation result of earlier. 

# Elaboration of the universe hierarchy

I formulated the complete system rigorously, trying not to forget any
rules. Then, I stated the soundness lemma for the casting judgement, which I 
proved by direct induction. With this, I proved the soundness lemma for the 
bidirectional typing judgement, also by a direct induction. Those were easy results
that are only safeguards, as said in the previous blogpost.

I still need to provide examples for the elaboration and the casting judgements, showing
how it would work in practice.
