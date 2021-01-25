#AFP


## Short Summary
This paper introduces a predicate abstraction based on Craig interpolation, 
taking advantage of locality to give a precise and scalable technique.
The key idea is that in a counterexample-guided program analysis, focusing
on defining and localizing a precise cut where one can identify where the 
unsatisfiability was induced is important.
This precise cut is retrieved by the notion of Craig Interpolation, and 
this paper introduces a way to mine a proof of unsatisfiability to build the 
interpolant which indicates the cut point of the trace. 

Their experimental results show that the technique seems to indeed scale
well and lead to smaller proof trees.


## Questions
- If we take the approach of turning all predicates to a dependently typed
proposition, what is the propositions-as-types correspondence to the Craig
Interpolation / definition of cut?

- Can Craig Interpolation also be used for blaming?
