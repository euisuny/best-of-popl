#  Compcert (2006)

## Summary

Great paper! It contains a readable, non-technical overview, not just of the CompCert development efforts, but of how it fits into the broader world of verified software and approaches to verified compilation.

CompCert (not named in this paper) is a verified (technically: certified) compiler for a subset of C. This paper reports on the development of the back-end, so technically the input is C-minor, not C. Everything was at the time under development, and continued to be improved in the following years; I don't know of the current status of CompCert and its coverage today.

I especially recommend Section 2. It clearly identifies a definition of a *certified* compiler (a compiler which comes with a verified correctness theorem), and relates it to the related concepts of *certifying compiler* (a compiler which generates proof-carrying code) and *translation validation* (a verifier that tries to prove that the generated code is equivalent to the original). The upshot is basically that implementing a certified compiler encompasses the other approaches.

One high-level insight is that all compilers can fail if presented with invalid or unsupported code; therefore, what really matters is the theorem that *if* code is generated, *then* it is equivalent to the source program semantics. This may not seem as good as full verification, however, there are many reasons why a compiler needs to have the option to fail, and as long as this occurs rarely, it seems to strike a good balance to allow it.

It is also quite interesting to read many of the anecdotes about developing CompCert (different things that go wrong, challenges, and design choices) in Section 6 and elsewhere.

## Questions

1. It is quite surprising that the sole author, Leroy, would complete all of this work on his own. Does anyone know why he did not choose to develop this with a team of researchers and programmers?

2. Another great paper, "Finding and Understanding Bugs in C Compilers" (PLDI 2011), has some comments about the development version of CompCert:

  > The striking thing about our CompCert results is that the middle-end bugs we found in all other compilers are absent. As of early 2011, the under-development version of CompCert is the only compiler we have tested for which Csmith cannot find wrong-code errors. This is not for lack of trying: we have devoted about six CPU-years to the task. The apparent unbreakability of CompCert supports a strong argument that developing compiler optimizations within a proof framework, where safety checks are explicit and machine-checked, has tangible benefits for compiler users.

  However, they distinguish between the "middle-end" bugs and "front-end" of CompCert, and they do find a number of bugs (at the time) in the "unverified front-end". Does anyone know what this means precisely? Does it just mean the translation from (a subset) of C to C-minor?
