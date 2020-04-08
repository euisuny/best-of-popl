# Combinators for Bi-Directional Tree Transformations

## Summary

This paper presents lenses, a function that goes from an concrete tree to an abstract view and a function that goes from an abstract view and a concrete tree to a new, "merged" concrete tree.
The approach is compositional, using PL staples like combinators and types to create lenses for tree transformations.

## Notes/questions
- They say there are no typing rules or a typechecking algorithm, so we are more or less using the well-behavedness predicate, right? I'm kind of confused about this, it seems that even if we didn't talk about types explicitly, designing the combinators would require thinking about this. So were types really that crucial to the formulation of the DSL?
- Perhaps I should just read the papers cited, but I don't really understand the point of bijective and reversible languages. What kind of programs can you write in them if there is a bijection between the source and target?
