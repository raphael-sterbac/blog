+++
date = '2026-04-07T10:57:04+01:00'
math = true
title = '9th Week'
+++

# Normalisation by Sconing

This week, I have been mostly up to understanding relative induction principles and sconing. The related
papers are quite interesting, and this clarified a lot of stuff related to gluing and GATs for me. Then, 
I wrote the proof of normalisation for the natural hierarchy using this technique. This took me a few days,
but it was not that difficult and simplified \textit{a lot} of things in the end, at least in comparison to
the kind of proof I was used to. 

Yesterday, I found out about Rafael Bocquet's PhD thesis which generalises the paper "For the metatheory of
types, internal sconing is enough" to any SOGAT. This would allow us to cite this thesis and get the exact 
relative induction principle from it, without having the need to say an imprecise thing like :
> "The constructions of Bocquet et al. [10] extend to S, and we notably get the relative induction principle [...]".

He also provides a more detailed example of normalisation for MLTT with a cummulative hierarchy of universes. He uses
universes à la Coquand, so this is still different from our setting, but this allowed me to compare his proof with mine and
see if we did similar things. This was indeed the case, and thus the proof must be good. However, I think that it still needs
more clarity and more reading so that there is no typo or anything that could lead the reader to not understand something.

# Implementation

As discussed last week, I reverted back my implementation to a simpler version where there was no pattern unification. I will 
need to put my code to more tests to see uf there are not any bugs that could have been introduced in the process, as I also
removed the explicit casting. I kept the version with pattern unification in a separate file `Unification.hs`, and I would be
still interested to try implementing the postponement of casting at some point.

However, maybe it would make more sense to implement it in Pterodactyl itself in that case ? As this is something we need
to put to the test in practice, it would make sense to add it to a real system to see how it would behave, whereas it would
be more complicated in a minimal implementation like mine. I don't know if I said this before but I had tried to provide some kind
of elaboration rules for this mechanism, which are in my notes. That was only a sketch though.

I've also seen the progress on the side of patterns for Pterodactyl, and the working examples in general. It looks amazing ! I will
also try to read a bit more about patterns and the implementation this week.

# Cummulativity in toposes 

Last week, I was trying to understand why cumulativity would fail in Mike Schulman's 2019 construction, and more precisely 
trying to figure out why constructing a mono pointwise by looking closely (and maybe adapting a bit) the small object argument would not work.
In the end it seems that this may work, and now I am somehow convinced that it should work. I had worked out some of the details on paper last
week, yet it would be a real challenge to write the thing down properly. I may try to do it at some point, but probably not in the near future.
