This is the seminal paper about lenses, the "PL solution" to the "view update
problem".

The fact that it spans both the database and PL literature is cited as one of
the reasons for it being influential. Studying this paper might be a good
opportunity to think about what distinguishes the "PL" point of view, in
contrast with other domains like databases in this case.
Developing a library of combinators that make it easy (if not free) to
guarantee "well-behavedness" of programs certainly as a very PL flavor. What is
the "database" point of view? Section 8 seems to cover this a bit.

Section 2 consists of a small but quite compelling example of a lens
on a tree structure. The matter of notation of trees is expedited in just the
first paragraph. The example is nicely motivated ("Why would we want this?"),
and takes arguably non-trivial work to handle addition and removal of records,
rather than just field mutation.

Section 3 describes an abstract framework for lenses. It's a bit surprising
to see it use a set-theoretic formalism, defining partial functions on the
Universe of all trees and then considering subsets where they're defined,
rather than saying "here's a function from C to A".

Sections 4 and 5 introduce various combinators. The first interesting one is
`map`, which applies a lens to every child of a tree. The lens laws put a lot
of constraints on how it should behave, notably when putting new names,
and the whole business about "shuffle-closure". I think this is the kind of
design consideration quite characteristic of PL papers.

Sections 6 (conditionals) and 7 (encoding lists) get quite technical, I
only skimmed them.

In Section 8 (Related work), the framework of section 3 is compared to others
studied in the database literature. A later subsection, makes another
interesting point, that others have worked on inferring the *putback* from
a *get*, but this paper constructs both at the same time.

<!-- Aside -->

Notably, it is mentioned how previous work has focused on "update function
translators" (A -> A) -> (C -> C).

I find that quite curious, because later (2008) lenses have been identified
with similar-looking "translators" of the form
(forall F, (A -> F A) -> (C -> F C)) (functions parametric over functors F),
which have been generalized into a whole hierarchy of "optics" on which the
popular *lens* library in Haskell is based. Yet another representation (2017)
is "profunctor optics":
(forall (~>), (A ~> A) -> (C ~> C)) (parametric over (a subclass of)
profunctors (~>)). A little community of category-theorists has been
developing around those latter representations.

- CPS-based functional references (blogpost), 2008, Van Laarhoven: https://twanvl.nl/blog/haskell/cps-functional-references
- Profunctor Optics (paper), 2017, Matthew Pickering, Jeremy Gibbons, Nicolas Wu: http://www.cs.ox.ac.uk/people/jeremy.gibbons/publications/poptics.pdf
- Glassery (blogpost), 2017, Oleg Grenrus: https://oleg.fi/gists/posts/2017-04-18-glassery.html
- Lenses for philosophers (blogpost), 2018, Jules Hedges: https://julesh.com/2018/08/16/lenses-for-philosophers/

This last reference begins with this hilarious claim:

> The earliest discovery of lenses (that I know of) was by Kurt Gödel in 1958

<!-- end of aside -->

Still in Related work, literature on "bidirectional transformations" is
separated in three classes: bi-directional languages (lenses), bijective
languages, and reversible languages. The distinction between the last two is a
bit unclear. The authors seem to characterize bijective languages more
"functionally", and reversible languages more "operationally".

Section 9 (Future work) opens broadly with questions both technical (type
systems) and conceptual (expressiveness of bi-directional programming).
