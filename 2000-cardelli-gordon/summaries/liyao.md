# Summary

This paper presents a modal logic for ambient calculus, a process calculus with a notion of "location".

The two modalities of interest are "somewhere" and "sometime" (dually, we also
get "everywhere" and "everytime"). There are also constructs to talk about
concrete locations (n[_]), but nothing similar for time (which would be very
hard because of all the nondeterminism).

The basic rules of the logic are illustrated via the presentation of
satisfaction and validity.

Some interesting applications are shown:
- Describing guarantees of type systems for ambient calculus
- An example analysis of a specification
- A decidable fragment is defined (for replication-free processes and |>-free formulas).

The logic is compared with others in the literature:
- Relevant and linear logic (I would have expected these two comparisons to be
  next to each other?) My main takeaway is that parallel composition behaves
  like multiplicative linear conjunction: two parallel components consume
  disjoint resources.
- Bunched logic, with "two structural combinators instead of one" (here,
  logical conjunction "/\" and parallel composition "|") .

# Comments

One thing that helped to motivate the definitions a lot was to frame
the explanations from the point of view of security.

But process calculi are annoying because there are a lot of rules,
in particular lots of congruence rules. The reduction rules can also be
hard to grasp. Ambient calculus models "locations" in a very abstract way,
which doesn't help. I think I'm starting to get the point of process calculi
but only after a lot of exposure...

Modalities suck because there are no mnemonics for the notation.

Lozenge = Some, Square = Every
Flat = time, Spiky = where

Rules of the logic. THERE ARE TOO MANY RULES.
The interesting ones are the modality rules.
The two modalities have many rules in common ("S4 modalities").
There are three rules distinguishing them. They make intuitive sense to me.
It's interesting to think about why flipping "TIME" with "WHERE"
breaks the rules.

- SOMETIME(A)|SOMETIME(B) |- SOMETIME(A|B)
- SOMEWHERE(A)|B |- SOMEWHERE(A|T)
- SOMEWHERE(SOMETIME(A)) |- SOMETIME(SOMEWHERE(A))

Are these all the rules?
This question is mentioned in the Future work section.

The example about thiefs and buyers is kinda funny.

Overall it's a pretty dense but clear paper.

The ambient calculus might be pretty fun to mechanize (formalize in Coq) and
animate (use graphical notation). The interplay of time and space has a certain
charm.
