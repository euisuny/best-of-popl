# Formal Certification of a Compiler Back-end

## Summary
The paper describes a formally verified compiler. The compiler seems to be implemented in a fairly standard way, but in Coq!

## Questions
- Did Xavier Leroy do this alone? Why? How? What?
- It's mentioned that in hindsight it would have been better to implement the dataflow analysis in OCaml and only certify the verifier, as was done with the graph coloring algorithm. Though from section 2 the two approaches are in some sense equivalent, I wonder people would have seen it that way. From my view the verified analysis itself was also a great contribution. It looks like they are still doing the verified verifier approach today.
- 
