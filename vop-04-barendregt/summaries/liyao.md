# Introduction to generalized type systems

(Nowadays called Pure Type Systems (PTS))

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

For (◻, ٭), `A` is a kind, like ٭, and (pi x : ٭, B) is
the type of a polymorphic term.

For (◻, ◻), both `A` and `B` are kinds, so we can write (pi x : ٭, ٭),
i.e., (٭ -> ٭), therefore we can define and abstract over type constructors.

For (٭, ◻), we can write functions of type (A -> ٭), which are dependent types.

---

Section 3

> the unicity of types does not hold for trivial reasons:
> there may be two axioms c : s1 and c : s2.

If we forbid those, do we recover unicity?

> Note the correspondence between lambda-AUT-68 and lambda-arrow

Uh, yeah, so obvious.


