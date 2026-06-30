+++
date = '2026-06-30T10:22:14+01:00'
math = true
title = '21th Week'
+++

# Implementing universe polymorphism 

Over the past week, I have been implementing explicit universe polymorphism in the style of BCDE. This was a bit more involved and subtle
than what I thought, but I am slowly getting there and currently testing my code. 

However, the elaboration algorithm itself is really easy to describe in theory and I already added the rules in the paper. One thing that I am a bit uncertain of is the
raw user notations that I currently use : $\forall \alpha\mathpunct{.} A$ for the level products and $\Lambda l \mathpunct. u$ for the level abstraction, with $u \{l\}$ for the level application.

The next things that I must do now after finishing testing my code is to add the corresponding functions to the tutorial implementation section (Sect.7). However, I am a bit worried that this might complicate quite a lot this section,
and it will also take some more (precious) space. However, now that universe polymorphism is a more central piece of the paper, this makes sense to integrate it like this. Hopefully, it will not take too much space.

# Normalisation for universe polymorphism and conservativity  

This week, I also merged together my extension for universe polymorphism with the main normalisation proof. In the end, it doesn't add much complexity to the proof, and we get a really cool result !

With this, I am now wondering on proving that the theory with level polymorphism is conservative over the one without. My original idea was to extend the fact that we map level variables to zero in the normalisation proof to write a translation function. The translation would be the
following, mapping from normal terms and types:

+ We map $\langle \alpha \rangle u$ to $u(\alpha/0)$ and $[\alpha]A$ to $A(\alpha/0)$
+ We map $u\, i$ to $\uparrow_0^i(|u|)$ where $|u|$ is the translation of $u$
+ For everything else, we propagate the translation structurally

Then, I think that we would be able to prove that this preserves derivation. However, this seems a bit weird, and we crucially have to map from normal terms such that in $u\, i$, $u$ is necessarily a neutral. I have been looking at the Lafont-style gluing proofs for conservativity,
which amounts at proving that a certain functor $\mathsf{MLTT} \rightarrow \mathsf{MLTT Poly}$ is fully faithful. However, I do not yet have the global view of this technique, and thus struggle to see what this functor should be and what we should do next... 

# Writing the paper

More generally, this week I have mostly been up to writing the paper, doing a bit of wording and formatting here and there. This takes a lot of time and effort as this is my first proper paper, but I feel like I am slowly getting better at it!
