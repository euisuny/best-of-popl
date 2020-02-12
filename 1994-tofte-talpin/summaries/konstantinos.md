## Summary

This paper proposes a translation of polymorphically typed
call-by-value λ-calculus to a language with explicit region
information. This is supposed to improve the memory consumption of a
program even without garbage collection. They prove that their
translation is safe, meaning that the two source and target programs
return the same value, and that the target program doesn't access
invalid memory.



## Questions/Concerns

- Is this really used now? What is the state-of-the art?
- The way I understand it, without garbage collection, there is
  "leaked" non-live memory that is left behind by their
  implementation.
- Could a static analysis be designed for this intermediate
  representation to estimate memory usage using the region
  information?
- What difficulty does polymorphism introduce?
- Does someone have some intuition about why they couldn't prove that
  they couldn't find a consistency relation that is preserved and
  rather that consistency is monotonically decreasing?
- Exactly before the conclusion the give a hint regarding integration
  with garbage collection. Why are dangling pointers a worry? Aren't
  dangling pointers just pointers that point to unallocated space?
  Also they say that precision is affected. Does anyone know if there
  is indeed some useful program that cannot typecheck even though it
  should?
