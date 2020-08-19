safe = not stuck

Logical relations (Kripke and vanilla) are better described by the term
"operational-denotational semantics" (that she mentions somewhere).

"Operational" because the relations are defined in terms of the operational semantics.
They are defined in a way that "safety" is an obvious consequence.

Thm 1: "All terms in the logical relation are safe."

"Denotational" because they're denotational semantics for derivations of the
syntactic typing judgement "C |- e : t", viewing the typing rules as the real
"constructors" of the language. The domain consists of proofs of the semantic
judgement "C |= e : t" (which is the "logical relation").

"denote   :   C |- e : t   ->   C |= e : t"
Thm 2: "All well-typed terms satsify the logical relation."
("denote" IS a proof of Thm 2)

Thm 1+2 imply "All well-typed terms are safe."

Compared to more classical denotational semantics, this approach is
interesting for not having to come up with any fancy domain for the denotations.
It's a pretty natural solution once you know it.
I always thought "logical relations" was a more alien thing.

---

The "Kripke possible worlds" model introduces an auxiliary state.
The state changes over time, and to account for those changes an
"accessibility relation" is introduced, and a "monotonicity" theorem
is required:

Monotonicity:
  if (S,e) -> (S',e')
     and S' is accessible from S
     and (S,e) satisfies the logical relation
  then (S',e') satisfies the logical relation

The accessibility assumption is then discharged from the fact
that all the rules defining the logical relation are of the form
"if (S,e) satisfies the logical relation,
    (S,e) -> (S',e') and irred(e')
 then S' is accessible from S (and more stuff)"

---

By definition, a type is a set of world-value (resp. state-value) tuples (w, v)
closed under accessibility (resp. state extension).

---

Impredicativity: In typed closure conversion, the existential type must be
impredicative because the closure may capture itself.

Fuel: Step-indexing is really a fuel-based approach.
Interestingly, the world is no longer a store S, but a store typing Ψ
together with fuel k. The fuel serves to avoid circularity.
A type must consume some fuel before referring back to itself.

Another interesting detail is that instantiating universals and
existentials should take zero steps, but this creates a problem because
in the definition of the types, the instantiation must consume fuel
to ensure a stratification requirement. This is resolved by only allowing
"well-founded" type functions F to be quantified, (forall x, F x),
where "well-founded" means that if t is a type up to approximation k,
then (F t) is a type up to the same approximation k.

---

Coinduction vs step-indexing: The mentioned issue is that coinduction
is foundationally nontrivial.

---

Deallocation: the idea is that locations are assigned not just to types t,
but to type-region pairs (t, r), where a region is an abstract identifier,
and at any time, at most one region for each type is "live".
