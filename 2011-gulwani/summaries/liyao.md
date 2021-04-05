This paper presents an algorithm for automatically generating string-processing
programs from input-output examples. It is a precursor of Flashfill now widely deployed
in Excel, a "killer application" for program synthesis.

The main technical ingredient is the design of a programming language that is
sufficiently restricted for synthesis to be tractable, but expressive enough to
handle problems found in practice. The paper is sprinkled with examples
demonstrating expressiveness, and also mentions an "extensive case study
of spreadsheet help forums" that the author performed.

The programming language's main construct is one specialized for finding and
extracting substrings, and the language also imposes a peculiar structure for
conditionals and loops. This allows an efficient representation of the set of
*all* programs which satisfy a set of input-outputs, a representation which is
at the core of the synthesis algorithm.

The focus on usability makes this paper somewhat unusual. In particular,
one key idea is that for the kind of "one-off" applications this work is
primarily aimed at, correctness is only loosely defined, so it's fine if the
generated programs are fragile (the first example is a regex to find a phone number,
which may still match non-numeric strings). Instead, the tool can be used
iteratively: users can provide more examples when the output is not
satisfactory, and the tool also offers additional feedback by highlighting
outputs with "low confidence" in some informal sense.

The abstract ends with this funny excerpt:

> The prototype tool has met the golden test - it has synthesized part of itself,
> and has been used to solve problems beyond author's imagination.

This is supported by some cute anecdotes in the evaluation section.
In particular, the first one (Example 12) formats some data into code
implementing a big lookup table in C#, as part of an extension of the tool itself.
