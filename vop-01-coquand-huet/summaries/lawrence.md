# Summary

The paper introduces a calculus of constructions, about which a few
things which jump out:

- The paper unifies computation at the type and term level (without
  necessarily using this terminology), or at the level of formulas and
  proofs, into one formalism. It seems heretofore this connection was
  not appreciated and there were two strands of lambda calculus:

  + Within the Curry-Howard correspondence lambda terms represent
    proofs of simple propositions

  + Within the simple theory of types lambda terms represent formulas,
    embodying a functional rather than predicate-oriented formulation
    of logic, but with an essentially Hilbert-style proof theory

- The system is impredicative. The authors note

> The main point is that these simple rules give us a complete
> presentation of both the higher-order logic and the higher-order
> functional system of Girard."

# Questions:

- I do not understand at all the fiddling with contexts and the
  insistence that they be "terms formed solely of products over
  `*`". Especially in light of the fact that "We shall usually view
  contexts as lists of terms, with quantification the list
  constructor." Doubly especially in light of the fact that contexts
  already don't have types!

- Even the wording "products over `*`" is confusing to me, since
  "over" * seems to mean the innermost term is *, while quantification
  happens over other things. This wording seems related to
  https://github.com/coq/coq/issues/5342. Generally it is unclear when
  talking about `PI (x:A) y` wether "foo" in expressions of the form
  "<predicate> <foo>" refers to A or B.
