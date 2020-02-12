## Summary

This proposes a memory allocation solution to compile a lambda calculus.

It works by organizing memory into *regions* (or *lifetimes*) which are
allocated and freed in a *stack*-like fashion, contrary to the now dominant
heap-based strategies. In particular, allocation and de-allocation points are
(mostly) determined statically. Only "mostly" so, because the size of regions
may be dynamic. Still however they may be implemented, regions are unallocated
as soon as we leave their scope, freeing all of their contents.

## Thoughts

- What made this paper "most influential"? I'm sad that we don't have the
  award citations prior to 1998.

- I would like to take a closer look at the other stack allocation mentioned
  described on page 2, left column. Also whatever "effect inference" is about.

- The paper is quite abrupt. The main contributions are surrounded by a
  maze of related work on memory management, and the introduction
  ends with an example which is, judging from other comments, explained too
  tersely. Then they pile up notations and things only get more and more
  technical.

- I managed by guessing the technical contents from the abstract, then
  matching the rest with what I expected the paper to be about.

- This scheme is, of course, proved safe, but a notable quirk is that regions
  may be freed while leaving dangling pointers in the other remaining regions. A
  small paragraph mentions that it may be problematic if one wanted to combine
  this with a garbage collector.

+ The translation relation (i.e., the compiler) also defines the type system
  of both the source and target languages. This makes it hard to understand
  the semantics of the target language in isolation.

+ It took me a while to accept dangling pointers as a feature
  of the language and the compiler. (Too used to well-scoped syntax by
  construction.) Rule 13 (dynamic semantics of `letregion`) introduces
  dangling pointers very easily, and I stared very hard at the compiler
  rules (14-20) to see how they prevent that from becoming a problem.

---

## More detailed summary

The source language is a plain lambda-calculus: call-by-value, recursion,
tuples...

The target language is a similar language where every value constructor
(lambdas, constructors, literals) is annotated with a *region name*,
pointing to where it should be allocated.
Region names are bound by `letregion` blocks, and are substituted
with freshly allocated regions during execution.

The compilation ("translation") annotates the source with regions wherever
necessary, and introducing `letregion` blocks where possible. The compiler is
actually defined as a nondeterministic relation, only describing the various
possible allocation methods, and it is up to an implementation to provide a
good inference algorithm.
For example, one can allocate a single region at the beginning and use it to
contain all values ever used by the program, but that is of course very
inefficient.
The paper mentions briefly the inference algorithm they used in their
implementation, and report empirically that it performs well.

The correctness proof doesn't seem too surprising. The most unusual technical
detail is that not all parts of the evaluation of the source program may be
reflected in the evaluation of the target program, if we know that they're not
going to be used.
