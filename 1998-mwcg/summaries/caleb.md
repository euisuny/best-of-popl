# From System F to Typed Assembly Language (1998)

## Summary

This paper is nicely written and easily digestible. It proposes Typed Assembly Language (TAL), which is exactly what it sounds like, and describes how to compile a standard functional calculus (in this case, System F) to TAL. This is done in a series of transformation stages through progressively more low-level lambda calculi; the end result is assembly language code (complete with registers, the heap, and statements such as `malloc`, `add`, `jmp`, and `mov`) that is completely annotated with types.

The benefits of having types at the assembly language level are twofold: 

- First, types (like other static information) often enable compiler transformations and optimizations that would not otherwise be possible. This is of course a trade-off because the types might also disallow other optimizations, but the authors argue that this is empirically minimal: they say that the typing places "almost no restrictions" on certain low-level optimizations of interest (and this is echoed in the Most Influential POPL Paper Award citation). This first benefit is not unique to an assembly language, but rather applies to any compiler IR.

- Second, types provide a form of safety that allows foreign code to be trusted by the execution environment even if it was not compiled on the same machine. For more on this benefit, see the discussion on Proof-Carrying Code (Best of POPL 1997).

## Questions

1. This paper has a lot of citations. What has been the bulk of the impact? What do people usually cite it for?

2. This paper lacks a Related Work section :(

    It would seem that the Proof-Carrying-Code from 1997 is an important piece of related work, as well as typed *intermediate* languages like TIL. Also, in the intro it claims that prior work has been unable to produce code which is 100% typed, and instead only 80% of it is typed.

3. How does WebAssembly relate to this?

    A brief look: the paper on WebAssembly discusses in the related work both "typed intermediate languages" and "typed assembly languages", and cites TAL as an example of the latter. But in regards to TAL, it claims that there is too much overhead:

    > The modelling of complex types imposes a severe burden on compilers, requiring them to preserve and transform quantified types throughout compilation and avoid optimizations that break the type system.

    I would be interested in understanding this better.
