# Proof-Carrying Code (PCC)

## Summary

Proof-carrying code is basically what it sounds like: a pair

    (C, P)

where C is an executable (machine-code) function and P is a proof that the function satisfies some safety property S. The code producer is responsible for compiling C and producing a correct proof P. The code consumer then just has to run a checking algorithm that P is a correct proof of S for C, and does not need to worry about inspecting the source code or coming up with the proof from scratch. Once P is checked to hold, P may be used any number of times, as the consumer soundly knows that C satisfies S on every execution.

The above description is abstract -- we haven't said what language C, P, and S are written in. In this paper, C is written in standard ML. S is written in first-order logic (with some predicates for useful things specific to safety).

## Unhelpful Paper Structure

I am not a fan of this paper structure where the body sections are titled "Case Study", with important definitions and theorems hidden inside. It makes it difficult to navigate if I just want to find, for example, a self-contained definition of the language they are using to write safety properties.

## Questions

- This paper is not the first by Necula to use the term "proof-carrying code". When was this term introduced originally, and what is the history?

- I was not clear on how tied their techniques are to the particulars of ML and the machine code generated here. What are the assumptions needed about C for this to work?

- What safety properties do their methods work for? Type safety and memory safety?

- Minor: what do they mean in the abstract and intro about using "external authentication and cryptography" to verify some untrusted code?

- Minor: what is meant by the end of intro, first paragraph? "extremely expensive mechanisms (such as sockets and processes) are employed" how do these mechanisms solve the type checking problem for dynamically provided code?
