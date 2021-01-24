# Abstractions from Proofs

## Summary

Take with a grain of salt as this is just my understanding and I didn't have time to read the paper too carefully.

This is a paper about program analysis using model checking. The basic framework is that we have a program (perhaps large, and not necessarily finite-state, i.e. a real program lol) and a specification, and we want to report program traces which violate the specification. The typical tradeoff is that lightweight and scalable analysis techniques work well on large programs but report many false positive traces, while heavyweight techniques (such as exploring a large part of the state space exhaustively) report few false positives but are prohibitively expensive for even moderate-size programs. This paper addresses this problem.

The goal is that while model checking a large program we should only track small amounts of information at each point in the program, hopefully only "local" invariants and not a lot of global invariants.

The insight is in the title: Abstractions from Proofs. Given a candidate trace violating the specification, it is assumed that one can construct a formula phi that encodes whether or not the trace is satisfiable. If the trace is unsatisfiable, then one can construct a proof that it is unsatisfiable, which can then be used to generate a smaller/minimal formula (kind of like an unsat core) that implies the trace is unsatisfiable. This is done via something called Craig interpolation, which (according to the POPL blurb) was previously only feasible in the finite-state setting, and this paper was the first to achieve it for infinite-state programs. This is done at a specific cut-point of the program trace, to give rise to a formula that should be true at that trace. This minimal formula is used as the local invariant at that point in the program to be passed back to the program analysis.

## Discussion

1. How does the step of going from a candidate trace to a formula work? I am a bit rusty on this.

2. Is this provocative idea, "Abstractions from Proofs", a more general phenomenon or specific only to program analysis and model checking?
