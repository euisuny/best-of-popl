## Proof-Carrying Code
### or how not to live dangerously when executing low-level code in your ML

This is a very interesting read, and I guess it was the first paper to
properly introduce this idea of code that comes together with a
certificate that shows that the code satisfies some property.

### Questions/Notes

- It seems that some for Proof-carrying code to make sense in practice
  the following requirements must hold. Is that true?
  + Code verification is a hard problem
  + Validation (checking a proof and its associated code) is an easy
    problem
  + PCC is executed more than once (to account for the additional
    cost)

- I understand Figure 3 as a specification of the relation between
  ML-types and the low-level memory state.
  + It seems that if one would like to extend this to more than memory
    safety properties, e.g. functional correctness, they would also
    have to extend these typing judgements.
  + I don't exactly understand how these typing judgments are used in
    the proof.

- In order for someone to use this technique they have to prove the
  soundness of the rules (like the ones in Figure 3). For example in
  the case study of 4, the typing judgements should be different and
  there should be a soundness proof.

- I would expect that the "Safety Proofs" section would also establish
  how a validator checks a proof and a program for
  consistency. However, it seems that this section only includes
  information about how to encode the proof. (Did I miss something?)
  + On a similar level, I don't exactly understand how the proof is
    connected with the code. Is it because the proof contains a
    sequence of proofs (between Pre-INV, INV-INV, INV-Post), and the
    code contains the same INVs?

- I am not sure what Theorem 3.2 means.

- In the discussion at the end of the paper it is mentioned that this
  technique can be extended to different properties. Does anyone know
  what are extensions of this work? I have personally heard of Kedar
  Namjoshi's work on self-certifying optimizing compilers that
  producer a proof that an optimization is sound when they perform it.

