+++
date = '2026-03-31T09:55:03+01:00'
title = '8th Week'
math = true
+++

# Postponed casts and unification  

Last week, I continued reading about pattern unification and tried to figure things out by reading Andras'
code for "Observing definitional equality". I am slowly trying to integrate it to my code, but for now this 
is clearly at an early stage, and I am a bit struggling to figure things out from Andras' code as there is a lot
going on there, with a lot of features implemented all at once. I will continue working on this more thoroughly this week.

# Reflecting on the Fuss-Free hierarchy  

This week, I discussed with Meven about things related to my last internship with Thierry. We discussed
adding other type constructors or general inductives to "Tarski" universes (without strucutral subtyping),
and the need to add the naturality and functoriality rules for those. For instance, with lists we need
\\[list_j(t_i^j(a)) = t_i^j(list_i(a))\\] We were discussing this because adding all those rules was needed
to get the equivalence result between Tarski/Russel universes. He suggested that we could recover all those
equations easily using the framework of AdapTT.

This made me realise properly that our Fuss-Free hierarchy also allow us to recover those rules for *all* type connectives that we could add. The
only rule to add is the closure under smallness !

This means that we could take advantage of this to allow the user to write something like `t : UserDefinedType(...)@small(i)`
which would mean that we want a term of the associated small type. This was already the kind of things that were presented in the original blogpost with the theory of small categories,
but I think we had deviated a bit from this original idea. Of course, the fuss-free hierarchy adds nothing that we were not able to do before,
but makes the presentation (and implementation) a lot simpler.

In a similar way, our naturality definitions for the natural hierarchy should extend for all new types. Maybe we could emphasize this
in the paper : we only need to add the natural transformation \\[ (\mathsf{input},\lambda\ \mathsf{input}. \ \mathsf{constructor}(\mathsf{input})) \Rightarrow (El(U_\bullet),El_\bullet) \\]
for each new type.

# Reading 

Last week I also did a lot of reading: I'm currently reading *Sheaves in geometry and logic* in order to consolidate my
knowledge on toposes (which right now was only acquired "on the fly"). I am also trying to understand more
of Schulman's 2019 paper, one thing I am notably trying to understand is why cumulativity fails there. As his universe
satisfies realignment, the only thing we need to do should be to construct a mono $\pi_\alpha \rightarrowtail \pi_\beta$ 
for regular cardinals $\alpha < \beta$. But for his construction in appendix, he is only able to define an arrow, which is not a mono.

However, I can't really see why a similar argument from the one in GSS22 could not work here, using the fact that we are taking 
colimits on the level structure ("big enough" regular cardinals) which should be directed anyway, so we should have the descent property and
this would allow us to construct the mono pointwise. I feel like there is something I am missing there.
