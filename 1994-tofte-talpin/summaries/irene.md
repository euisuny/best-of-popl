### Region-based Memory Management

Tofte and Talpin provide a compilation scheme from a polymorphic CBV lambda calculus to a _region_-based calculus. 
Points of region allocation and de-allocation are inferred automatically using _effect inference_.

- **Regions** provide a way to do memory allocation in a stack-like manner, 
- **Explicit region polymorphism** is used to obtain separation of lifetimes. 
- **Effect inference** (inspired by _effect masking_) delimits regions of memory and their lifetimes.

Translation from the source to target language introduces `letregion` blocks based on an inference algorithm. 
The resulting language may have "harmless" dangling pointers (Why?).

The correctness of compilation is defined as a consistency relation defined with respect to an effect.


This paper is a promising candidate for CIS 700's Poorly Written Influential Papers.
