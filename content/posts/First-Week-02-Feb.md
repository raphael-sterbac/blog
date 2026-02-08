+++
date = '2026-02-05T18:03:24Z'
title = 'First Week'
math = true
+++

# Subtyping and Parametrised Inductive Types

On Tuesday, which was my first proper day, I focused on the potential issues we could
encounter when adding structural subtyping and Parametrised Inductive types. A typical
and pathological example of the latter is the list datatype $\text{List}(A)$.

If we allow the user to deduce $l : \text{List}(U_{i+1})$ from $l : \text{List}(U_{i})$,
then we would also have both $nil_{i} : \text{List}(U_{i+1})$ and $nil_{i+1} : \text{List}(U_{i+1})$.
However, we wouldn't have $nil_{i}  = nil_{i+1}$, unless we add the equation. This breaks canonicity
for inductive types, and could lead to weird error messages on the user-side such as `Could not unify nil and nil`.

# Elaboration of the universe hierarchy

I've been working on the elaboration of the universe hierarchy, namely translating the user
syntax for universes (close to Russell-style universes) to the core language using the "Fuss-Free universe
hierarchy" with smallness judgement.

To do this, I first got used to bidirectional elaboration as described in *Cosmology of datatypes*, and then
tried to write the specification. First, I specified the definitions for type-connective codes, as it is done
for the product type in the blogpost.

For example, the elaboration should translate $\Pi A B :  U_i$ to $\Pi^i A' B' : U_i$ where $\Pi^i$ is the 
code for product types and $A'$, $B'$ are the elaborated versions of $A$ and $B$.

We can also do that for universes, and I'm currently thinking on how to elaborate lifts/cummulativity and 
generic datatypes or inductive types.

Also, I am not "calling" the unification algorithm at the moment, and I'm not sure to see where it would be needed.

# Injectivity of decoding and lifting

 I spent some time thinking about how to prove injectivity of decoding and lifting. First,
 I was trying to prove it using a normalisation by evaluation method, such as the one for proving
 injectivity of product types. However, it did not seem to be as easy as for products.

 Then, I realised that I may have already proved the result in some sense with Thierry last year. Namely,
 we proved that Russell and Tarski formulations of universes were equivalent. Translating injectivity of lifts
 from Tarski-style to Russell-style amounts to proving that if $\Gamma \vdash a = b : U_j$ and $\Gamma \vdash a,b : U_i$ with $i < j$, then
 we can construct a proof of $\Gamma \vdash a = b : U_i$. This can be proven easily by induction
 on the derivation, *mutatis mutandis*.

 With the equivalence result, we can then convert the judgement $\Gamma \vdash t_i^j(a) = t_i^j(b) : U_j$ back and forth,
 to get directly $\Gamma \vdash a = b : U_i$ in the Tarski theory !


 This proof seems quite elegant and intuitive to me if we think as the Russell theory as a kind of model. The hard work is hidden 
 in the equivalence result. Concretely, 
 the important (and non trivial) result that embodies the injectivity is the "uniqueness up to erasure" result.

**Uniqueness up to erasure.** If $\Gamma \vdash u_0 : A_0$ and $\Gamma \vdash u_1 : A_1$ in Tarski-style, with $|u_0| = |u_1|$ and
$|A_0| = |A_1|$ (syntaxical equality when removing all the lifts), then : $\Gamma \vdash A_0 = A_1$ and  $\Gamma \vdash u_0 = u_1 : A_0$.

To me this indicates that if we can prove normalisation (probably iwth a gluing argument), we could prove the injectivity result directly
with a clever proof by (mutual) induction.

# Strict universes for Grothendieck topoi

I also spent some time reading the paper *Strict universes for Grothendieck topoi*, and tried to get the most out of it.

Something that occured to me is that there is no mention about injectivity of the decoding `El`, which would correspond
to a kind of "injectivity" of the generic family in the model.

Maybe the "injectivity" comes from the universal property of pullback, as if we substitute $a$ and $b$ in $\pi$ and get the same result, by
uniqueness of the pullback we can deduce $a = b$. I'm not sure.
