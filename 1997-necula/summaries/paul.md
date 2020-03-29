# Proof-Carrying Code

## Summary

This paper describes a method for binaries to carry along a proof of its safety, according to some _safety policy_. 
Most of the paper is devoted to a case study of ensuring the safety of foreign functions---written in assembly---in a run-time for SML.
Here, the safety policy is that foreign functions represent data properly, e.g. pairs are pointers to 2 words, lists are linked lists, etc.
The foreign functions are represented as a list of assembly instructions, along with invariants for loops and preconditions. 
Since invariants are already included, verification conditions can be easily generated from the functions. 
Both the producer and consumer of the code can generate the VCs, so we just need to attach a proof of the VC predicate with the code.
Thus, a proof cannot be faked by changing the code afterwards. 

The predicates and proofs are encoded in (a fragment of) LF, which handles the proof checking. 
The actual proofs are generated using a logic programming language (which is based on LF). 
This is possible because the VCs are fairly simple in their experiments. 

They also show a second case study of safe packet filters.
Since the code is just assembly, it can be optimized and thus runs much faster than many other works.
The proofs are fairly small and proof verification is very fast. 
Notably, you only need to verify once, and run the code as many times are you like after that. 

## Notes/questions

- TIL what PCC is
- Finding proofs isn't really the focus of this, you can write them by hand if you like. 
- Language extensions refers to foreign functions, right?
- Is this work being used widely today?
- While looking for a searchable pdf, I found [this](http://infocomp.dcc.ufla.br/index.php/INFOCOMP/article/view/189). Is this just straight plagiarism? He cites Necula though...
