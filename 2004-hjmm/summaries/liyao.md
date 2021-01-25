This paper is about predicate abstraction in model checking.

In a counterexample-guided analysis, given some overapproximation of the
executions of a program, and a counterexample (a trace in the overapproximation
which is not actually a valid behavior of the program), the problem is to
refine the approximation so it does not include the trace, and to do so efficiently.

The key idea is to use *Craig interpolation* to find relevant predicates to refine
the abstraction. The paper presents a technique to obtain interpolants that
only refer to the current values of variables at a particular point in time,
rather than past or future values. It is useful to avoid state space explosion,
since only few predicates are relevant to track at any point in time.

---

The general introduction (Sections 1 and 2) gives some good intuitions.

One limitation seems to be that Craig interpolation does not work in all theories.
