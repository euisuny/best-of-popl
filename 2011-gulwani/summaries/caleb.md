# Automating String Processing in Spreadsheets Using Input-Output Examples (POPL 2011)

More program synthesis! Probably 2012 will be a new topic :)

This is the now-famous paper about FlashFill, which has become
the prototypical success story in program synthesis research.
The paper is well-written and I think it is especially famous because
of the clear practical use case, real end users, and production deployment (integration into Excel).
Before reading this paper, though, I was less familiar with the actual
techniques used in the synthesis algorithm, which were nice to read about.
In particular the design of the string processing language plays a key role in the contributions:
i.e. what string processing operations are allowed
and how string transformations are built up compositionally.

The language used builds on standard operations like regular expressions and substrings, but ends up very general (esp. because it includes looping).
It probably lies outside the scope of most formal classes studied by the formal languages community.
It includes length indexing (length constraints)
and if-then-else operations.
I wonder if the language's formal expressiveness has been studied;
is it even less than Turing complete?
Subsets of these operations (e.g. string constraints with substring, replace, regular expressions) have been identified
in SMT as theories with various partial and complete decision procedures available.
Probably looping has not been looked at in that context.

I find spreadsheets as a programming paradigm fascinating, because they
differ fundamentally from the programming that we are used to, yet are widely adopted
and hugely popular in various industries.
Many things about spreadsheet programming are quite unsafe (e.g. types
are vague and often inferred from the data), and we could imagine improving
with a more principled spreadsheet language.
But one thing about spreadsheet programming that seems very useful for
end-users is that it's very visual, and the program doesn't exist as a separate
object from its execution. In other words, you write a formula, and then immediately see its evaluation on the input data, so you can kind of debug your formula at the same time as you are writing it, and all the intermediate computation steps exist as cells in your spreadsheet rather than just as internal states of your program.

The paper at times gets a bit excessively grandiose:
"The prototype tool...has been used to solve problems beyond author’s imagination."
"General purpose computational devices, such as cell-phones, computers, are becoming accessible to people at large at an impressive rate. In the future, robots will become house-hold entities."
In my opinion these sentences detract a bit from the paper.

The acknowledgments section is excellent.
“For the first time, we understand what your research is about."

## Questions

1. What work has been done in the PL community on "visual" programming (for lack of a better term) ala Excel, where your program is executed on data and the intermediate results are also present as cells (acting as a visual trace of your program)?

2. Is the string processing language described in the paper Turing-complete?

3. Was Conjecture 1 (completeness of the synthesis algorithm) ever resolved since this paper was published?

4. Comparing with traditional automata/regex synthesis work (in particular Angluin-style learning) the paper states:

  > Work on learning concepts such as deterministic finite state automata [1], or regular transducers [20] from examples is not applicable in our setting because it requires making many more queries to the user, and most string processing tasks described in this paper are more expressive than what can be expressed by these concepts.

  I definitely buy the second reason: the string processing language is clearly more expressive. But the former reason I would like to understand better. Why do these techniques require more queries? In principle, shouldn't they require *fewer* queries because the space of programs is not as expressive, thus less room for many different programs to have the same input-output behavior on a small number of examples?

5. What is the relation between this paper and the 2010 best paper, both by Gulwani (et al) on program synthesis? From the paper, it doesn't say a lot, but hints that the techniques used might actually be very different.
