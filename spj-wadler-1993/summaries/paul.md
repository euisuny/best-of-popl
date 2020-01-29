# Imperative Functional Programming

## Summary

This paper introduces a way of using monads to perform I/O in Haskell.
This is compared with two other popular styles of I/O in pure and lazy languages, dialogues and continuations.
They show that the monadic method is equally expressive as each style.

The heart of the implementation is `ccall`, which calls C functions.
It is implemented as a primitive in the language.
Then IO functions are simply calls to `ccall` with appropriate arguments, and the monadic operations are simple to define in Haskell.
The IO monad carries around a `World`, which makes sure that `ccall` operations in `IO` are sequential.

The paper also shows that a similar approach (using a state monad) can be taken to implement monadic arrays.
A similar interface has also been implemented using continuations, but they show that continuations cannot define the monadic interface, while monads can define the continuation one.

## Notes

There were a lot of typos.
Maybe we should have picked a higher tier conference with better papers.

Was this paper basically just about the state monad?
How prevalent were monads in 1992?

Is `World` completely abstract?
It doesn't actually carry around the state of the world, right?
Is that just a useful intuition?

The comparison with continuations for arrays seems strange.
Is the extra type variable that big a deal?
They ask this themselves in the paper.
