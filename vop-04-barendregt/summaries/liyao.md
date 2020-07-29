# Introduction to generalized type systems

(Nowadays called Pure Type Systems (PTS))

---

One-sentence opinion: After reading this paper, I feel a little more
knowledgeable (having read the main ideas elsewhere) but also left with much
more to think about, unsatisfied from the lack of non-technical, synthetic
discussion.

---

The beginning makes me super curious about the historical context
originally motivating the various corners of the cube.
The three corners of the cube I'm somewhat familiar with are LambdaArrow
(STLC), Lambda2 (System F), and LambdaC (Coq).

But I also find this paper rather dry, partly because I'm not that familiar
with all the systems discussed. It shows a common formalism to compare
a variety of lambda calculi, but doesn't offer much discussion beyond that, so
the reader is left on their own to figure out the ramifications.

---

Section 2

> The reader is invited to carefully study these examples in order to
> gain some intuition for the systems of the lambda-cube.

i.e., here's a bunch of examples, do what you want with it.

I never remember what each tuple of STAR and SQUARE means.

Recap:

> (٭, ٭) terms depending on terms (functions)
> (◻, ٭) terms depending on types (parametric polymorphism)
> (◻, ◻) types depending on types (higher-kinded types)
> (٭, ◻) types depending on terms (dependent types)

The two key rules defined by such a tuple (s1, s2) are:

```
G        |- A : s1
G, x : A |- B : s2
-----------------------
G |- (pi x : A, B) : s2
```

```
G |- A : s1
G, x : A |- b : B
G, x : A |- B : s2
-----------------------------------
G |- (lam x : A, b) : (pi x : A, B)
```

I'm not even sure how to see STLC from (s1, s2) = (٭, ٭):
it clearly contains STLC, but it doesn't seem to explicitly forbid
dependencies.

For (◻, ٭), `A` is a kind, like ٭: (pi x : ٭, B) is
the type of a polymorphic term.

For (◻, ◻), both `A` and `B` are kinds, so we can write the kind (pi x : ٭, ٭) : ◻,
i.e., (٭ -> ٭), therefore we can define and abstract over type constructors.

For (٭, ◻), we can write functions of type/kind (A -> ٭), which are dependent types.

---

Section 3

> the unicity of types does not hold for trivial reasons:
> there may be two axioms c : s1 and c : s2.

If we forbid those, do we recover unicity?

> Note the correspondence between lambda-AUT-68 and lambda-arrow

Uh, yeah, so obvious.

---

Section 4

The syntax of a logic is presented as an elementary language
of terms (atoms and applications of function symbols)
and a first-order language of formulas (relations on terms, connectives,
quantification on values (for predicate logic)).

The translation of terms and formulas to GTS is straightforward because
it is all simply typed.
It's the translation of derivations that really makes use of the expressiveness
of GTS, in particular by forming (dependent) functions.

The "proposition-as-types" correspondence shows that

1. intuitionistic logic is isomorphic to a particular GTS;
2. there is a forgetful morphism from that GTS to one of the corners of the lambda cube

Also, if we distinguish propositional vs predicate logic,
predicate logic corresponds to the four corners with the (٭, ◻) rule
(predicates as dependent types).

Soundness holds (provability of a proposition implies inhabitedness
when viewed as a type), but the converse does not in general, and the given
counterexample is between lambda-C (CoC) and its logical counterpart.
The idea behind the counterexample is that the following proposition
has different meanings when interpreted as a proposition or as a type:

  forall (P Q : Type), (P <-> Q) -> P = Q

The logician's way to read it is that logically equivalent propositions are
equal, which is true in a reasonably large class of models.

The programmer's way to read it implies that all inhabited types are equal,
which is a really bad property to have.

> (definition of all 8 logics)

So in the part of the section before that he was actually specifically
talking about PRED and lambda-P. When generalizing to the remaining logics,
they are actually *defined* as their corresponding GTSs.

It appears that propositional logics actually are identical to their
corresponding lambda calculi.
It is predicate logics that require an extra sort to keep functions
first-order.

A reference mentioned near the end looks particularly intriguing:

> In Leivant (1989) interesting use has been made of the propositions-as-types
> interpretation concerning the representation of data types.

> "Contracting proofs to programs", Daniel Leivant, 1989, in Logic and Computer Science

A few appetizing quotes:

> The main novelties, compared to previous works on extracting algorithms
> from proofs, are the reading of reductions themselves as programs, and that
> instead of a constructive reading of ∃, we use a Leibnitzian view of objects
> as properties.
> (Abstract)

> In defining the [Curry-Howard] isomorphism for quantifiers, Howard was led to
> defining richer type structures, with dependent type operations.
> (...) We pursue a dual approach: rather than enriching the type structure to
> match logic, we impoverish logic to match the type structure.
> (Section 1.2)
