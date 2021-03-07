# Multiparty Asynchronous Session Types (POPL 2008)

## Summary

This paper introduces the titular concept.
Session types were around for a while before that, not sure how long, but they are typically two-party: there is a duality between the two parties. When the sender sends, the receiver receives, and vice versa; when the sender offers a choice, the receiver makes a choice, and so on.
This paper addresses the question of whether we can extend this to the *multi-party* setting, which is nontrivial because this duality is no longer directly exploitable. It also naturally addresses the challenge of *asynchronous* types because (if I understand correctly) with more than two parties, asynchronous communication becomes inherent to a session, as when two parties are communicating the other party could be doing something else. Whereas with two-party sessions, you can at least think of a correctly executed protocol as synchronous, each party going through the session in lock-step.

This was a very nice read, I really like session types and the idea, contribution, and impact is overall clear. Session types are popular today, I can see exactly why this work would be influential.

## Questions

1. The introduction mentions three crucial theoretical properties to establish for session types (which they also aim to do in the multiparty setting), namely, (1) communication safety, (2) linearity and progress, and (3) session fidelity and predictability.
I would be really interested in understanding the development plain (2-party) session types with these properties in mind, and seeing how to prove them and what assumptions are made.
I am guessing these properties are where some of the key benefits and tradeoffs of session types lie, and would be very relevant for applications.

2. I am not sure I fully understand the role of "asynchronous" in the formalism. Am I correct that this is more crucial with three or more parties, since communications can no longer be thought of roughly in lock step? Or are even two-party sessions really asynchronous?

3. How have multiparty asynchronous session types influenced today's work? Have they been implemented or used in some major tools? (Kenny's work presented in PL club is relevant! I think they were doing two-party session types if I understood correctly.)

4. The syntax for multiparty session types is unfortunately less natural to me than for two-party sessions. Are there any ways to simplify the notation?
