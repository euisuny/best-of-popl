JFlow is an extension of Java with a type system for IFC.
The main contribution is to make the system usable:

- static type checking, so types can be erased and thus not lower performance;
- an expressive type system, covering a (I assume) significant fragment of Java
  (objects, exceptions). Section 2.11 discusses limitations.
  (Multithreading, side channels (timing and OOM), the usual culprits.)
- type inference, and carefully designed defaults so annotations are
  unnecessary in simple cases (e.g., where to add implicit label parameters).
  There are examples demonstrating this.
- run-time policy checks are still possibl, which requires the
  system to have dependent types.

Another feature is that it uses a *decentralized label model*, meaning that
principals can declassify their own policies, but not those of other
principals. In a centralized model, there is an entity trusted by everyone to
declassify.

Uses "label polymorphism", inspired by row polymorphism.

---

> (page 4)
> actsFor(p1,p2) S executes the stmt S if the pcpl p1 can act for p2.
> Otherwise the stmt is skipped.

This seems weird because this is a conditional
(desugars to an if, Section 3.6, Figure 16), doesn't it leak information?

---

> various possible termination paths: normal termination, termination through
> exceptions, termination through a return statement, AND SO ON

Terrible language.

> Figure 9

The typing rules are actually pretty readable.

> Section 3.7, Figure 14

Oh no.

---

The translation just erases labels everywhere, except where they are passed as
first-class values.

> important features like objects, inheritance and dependent types make formal
> proofs of correctness difficult at this point.

The last paragraph makes a great point:

> This list of mechanisms suggests that one reason why static
> flow checking has not been widely accepted as a security tech-
> nique, despite having been invented over two decades ago, is
> that programming language techniques and type theory were
> not then sophisticated enough to support a sound, practical
> programming model.
