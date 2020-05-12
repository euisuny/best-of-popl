This paper presents CompCert, the first formally verified compiler, whose proof
is machine checked, for a "realistic" language.

This paper is surprisingly easy to read.

At the time of publication (2006), the project was already two years old.

Section 2 explains and relatex various approaches to verified compilers.

- Certified compilers (CompCert)
- Certifying compilers, that output code together with a proof of correctness
- "Verified" compilers, that are paired with a verifier of the output code
  (translation validation)

They are all essentially the same modulo Curry-Howard and stuff, but also
represent different approaches to design individual phases of a compiler.

- Cminor (external, then internal)
- RTL (control-flow graphs, nodes are single instructions)
- LTL (register allocation + spilling on an "abstract" stack, CFG nodes are basic blocks)
- Linear (list of instructions with labels and branches)
- Mach (stack is made concrete)
- PowerPC "macro-assembler", with "macro-instructions" which desugar to "canned
  sequences" of PowerPC instructions.

Simulation diagrams and simulation relations are given for each code transformation.

---

I wondered about function pointers.

> We therefore have function pointers as first-class values, but in a “Harvard”
> model where functions and data reside in different memory spaces.

Why is it called the "Harvard" model.

> function pointers are supported, enabling the compilation of object-oriented
> and functional languages.

---

A common theme is that a lot of difficulty is found in parts that informally
appear "straightforward".

> It is folklore that such parallel moves can
> be translated to sequences of individual moves using at most one
> temporary register of each type. Showing the correctness of the
> parallel move compilation algorithm is one of the most difficult
> proofs in this project (...)

> The proofs are however marred by lots of administrative work to
> enforce non-overlapping hypotheses between the various kinds of
> locations, especially between allocatable and temporary hardware
> registers.

---

Evaluation

> the certification is about 8 times bigger than the code it proves.

10 times the code, but bug-free!

Rather, it never miscompiles, but it could still refuse to compile, which, for
practical purposes, is equivalent to the compiler crashing.

> performance only slightly inferior to gcc at optimization level 1

That's surprisingly good.

---

The source uses big-step semantics, which is only meaningful for
terminating programs.

> Reduction semantics (where expressions are rewritten at each execution step)
> do not commute with compiler transformations such as RTL generation

In other words, a source-level small step (e1 + e2) -> (n + e2) would not
translate to Compile(e1 + e2) -> Compile(n + e2) at the RTL-level
(because what changes in the RTL semantics is the program counter, while the
instructions themselves remain fixed).
That's an interesting problem, I wonder how and if it's been solved.
Software Foundations has an exercise about a simplified situation
(compiling arithmetic expressions to a stack machine), and my ITree talk
pretty much started with "operational semantics = BAD"...

---

> We had to develop and prove correct some of our own data structures, but in
> the end were able to implement everything on top of only three data
> structures: finite sets, finite maps and a func- tional “union-fin

He seems to really like how easy it is to verify translation-validation.

> Building such scripts is surprisingly addictive, in a videogame kind of way

> There is no doubt that a Coq expert could have...

---

From the acknowledgements, CompCert is part of a "research action" named
Concert (from what I understood, something like the DeepSpec "expedition",
on a smaller scale in terms of parties involved).

http://www-sop.inria.fr/lemme/concert/ (in French)
