# From Program Verification to Program Synthesis (POPL 2010)

If program verification is "Proofs from Programs" and program extraction is "Programs from Proofs", then program synthesis is "Programs and Proofs from Specifications".
This paper presents an early and influential approach to program synthesis from a functional specification.
The specification is given in three components: a functional spec, a collection of constructs that are allowed to make the program (similar to syntax-guided synthesis), and a bound on the resources allowed.

It's quite interesting to me that it's possible to include a resource bound here. I always think of program synthesis as search-based through all programs, without regard to resource usage. I like the idea of using resource bounds to both make the generated program more useful and the process of finding it more efficient.
