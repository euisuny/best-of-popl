Screw Dialogues, here cometh IO monads to perform input/output actions in Haskell. Here, we view monads as an abstract structure modeling effectful continuations, where Haskell users, using the do notation, can write code that is stylistically similar to imperative languages. 

One thing that I would have liked to find in this paper is some discussion about the theoretical necessity for the “dark side of the IO monad,” namely the _unsafePerformIO_, _inlinePerformIO_, and _unsafeInterleaveIO_.

Also, since modern industrial-strength languages such as the Rust programming language have affine types (and thus compiler-writers and language-designers are used to writing languages with substructural types..), would linear types be a more feasible alternative for I/O now? 

