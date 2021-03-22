This paper introduces the notion of a proof-theoretic synthesis, i.e. where 
program synthesis is interpreted as generalized program verification. 
Usuaully, in program verification, the program proofs are synthesized via 
inductive invariants for partial correctness and ranking functions for 
termination. The key idea is that a synthesis problem can be encoded as a 
verification problem, where program guards and statements are logical facts that
need to be discovered. The authors claim that this is the first technique to 
automatically synthesize proofs alongside their programs. 

There are three ingredients necessary to the synthesis: (1) functional 
specificaiton, (2) domain constraints (program expressions and guards), and (3)
resource constraints (flowgraph structure, stack template, and computation
template).

The soundness of the synthesized program is guaranteed by the _well-formed_
_condition_, which ensures that the programs are non-trivial and valid.
One technical point that seems critical in making this work is using transition
systems to represent acyclic fragments of the code.

A case study of several algorithm shows that this method works pretty well for 
non-trivial algorithms.

Question : 
In the program structure, it assumes that the program that we have is a
high-level enough program that we have looping structures as a primitive 
language construct. How would this work for assembly instructions that uses 
jumps and branches? Would the problem be easier if we used higher-order 
operators such as map, foldl, etc. instead?
