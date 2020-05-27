This paper seems to be a condensed technical summary of Coquand's thesis.

Q: What is the difference with MLTT? (My a priori knowledge is that these systems are all more or less the same)

> Note that our class of terms is almost identical to the one considered in
> Martin-Lof's original theory of types, but our syntactic treatment is
> closer to that of the Automath languages, and particularly to Jutting's.

> In Martin-Lof's system, (forall A : U0, A) is of type U1, and not of type
> U0. Here, (forall A : Type, A) is of type Type.

That only holds for Prop nowadays.

---

Language constructs: `Type` (no `Prop`), `forall`, `fun`, application


---

Conversion rules are restricted to the level of types, to make the proof
of decidability of type inference easier. We have the conversion:

    (fun x => M) N   ->   [x/N]M

only if M is a proposition, i.e., its type is a context, of the form
(M : forall ... , Type)

# Summary

1. Syntax (terms are well-scoped by construction; definitions to
   manipulate DeBruijn-indexed terms)

2. Typing rules

3. Beta-conversion

    - Decidability of type inference

    - (There's a typo here, the second rule is reflexivity)

4. Stripping (type erasure)

5. Denotational semantics

    - WTF is going on

    - This proves strong normalization, and consistency as a corollary

6. Various remarks

    - Constants (`Definition`)

    - Implicit arguments

    - "dynamically extendable parsers", "complex window managers",
      "tacticals", basically Coq.
