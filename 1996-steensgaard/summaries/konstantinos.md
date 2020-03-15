## Points-to Analysis in Almost Linear Time

This paper proposes a novel and asymptotically faster points-to
analysis. The analysis is interprocedural and flow-insensitive. It is
based on a novel type system that keeps information about the types of
locations each variable could point to.


### Notes

- They seem to be making two assumptions for the soundness of their
  analysis, namely that no pointer is created from scratch (e.g. using
  bitwise operations) and that allocate is portable, meaning that
  every location that it allocates cannot be related to any other.

- They argue that not using equalities in the typing rules allows for
  a less strict analysis. They give an example where using equality
  would be too strict.

### Questions

- I lack intuition about this type system. Can anyone explain how to
  conceptualize it?

- In the beginning of Section 5 they mention "a minimal solution". How
  is minimal defined in that case? It is not clear to me.

- In 5.1 they claim that joining can't make a program ill-typed, but I
  am not sure why this is true. Maybe it has to do with the fact that
  previously un-joined variables that have to be ordered (e.g. y<z in
  z=y) can either be \bot or joined? So because they keep all these as
  possible joins, when a type is \bot, all necessary joins will happen
  in the end, leading to a well-typed program.

- Wouldn't doing an SSA translation before the analysis make it even
  more precise? Now if x is given two completely different values in
  different parts of the program it might lead to unnecessary joins.

- In Section 3 they make a claim that describing each element in a
  composite object (such as a struct) by separate types would make the
  size of the graph exponential. Why is that?

