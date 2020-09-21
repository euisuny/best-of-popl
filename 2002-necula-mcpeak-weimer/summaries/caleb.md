# CCured: Type-Safe Retrofitting of Legacy Code

## Summary

This paper presents a framework and tool to ensure pointer- and type-safety of C programs. The main contributions are CCured, the type system which combines different kinds of pointer annotations (e.g., both dynamically and statically checked pointers), and an algorithm for translating C programs into CCured programs. Together, these contributions allow automatically "retrofitting" low-level C code to make it type-safe, although at some cost because there will be additional safety checks at runtime for the dynamically-checked pointers.

The paper is very practical! This is true for both the conceptual ideas and the implementation; the clear goal is to have something that works well enough in practice on real C. A particularly impressive claim by the authors is that the translation actually handles *all* of C, not just a subset (as one would typically expect from a research tool such as this one):

> Our implementation handles the entire C programming language along with most of the extensions in the GNU C dialect

The evaluation shows that CCured is moderately effective for some real pieces of C code: for example, most (approx. 90%) pointer types are inferred statically and so many runtime checks are avoided. The performance overhead of using CCured is up to 2.5 times the original runtime, but typically somewhere in the 1-1.5 range.

Conceptually, the main idea of the type system is to categorize pointers into 3 types: safe pointers (no bounds checks are needed at runtime, although null-pointer check is still needed); sequence pointers (which roughly seems to mean that statically it is known that it points somewhere into an array of values of a particular type, which means that bounds checks are needed at runtime, but not type checks as to what kind of pointer it is), and dynamic pointers (for which, basically, nothing is known, it could be a pointer to anything or a plain integer, and arbitrarily casted between different things).

The paper is well-written and impressive. I must admit though that the results seem a little too good to be true. We know that arbitrary C code can do arbitrarily bad things, so how can they really avoid that without disallowing dynamic pointers entirely or disallowing some subsets of C? (More on this below.)

## Questions

1. When the authors said "Our implementation handles the entire C programming language" is that really true? Does it handle, for example, concurrent C code correctly?

2. I am a bit confused by exactly what kinds of safety are ensured by the type system. Note that, even for "safe" pointers, they still are explicitly allowed to be null pointers and so require dynamic checks at runtime (perhaps this accounts for some of the overhead, given that most pointers are inferred to be of the "safe" kind). The paper is pitched as providing *type* safety for C programs, not *memory* safety. So it must not be as strong as e.g. the Rust type system which provides memory safety. Some more concrete questions:

  - In CCured, if I have a pointer to memory, do I know that the memory contains real data that has not been deallocated?

  - Is it really true that type safety is ensured in general, or are there some caveats? I have in mind the fact that ensuring unique ownership over a memory location is a hard problem for C code. So, let's say I have a "safe" pointer to some memory, but some other unsafe dynamic pointer also can get to that memory and modify it. Now, can't the dynamic pointer cast the memory to be something else? How can I really avoid this statically, in the presence of arbitrary C code?

  - Do safe pointers always have size that is known at compile time?

3. How does the CCured type system compare to the Rust type system? How does it compare to separation logic?
