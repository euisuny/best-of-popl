This paper adapts session types to multiple clients in an asynchronous setting.

Session types traditionally describe two-party communication, where one type
can be "dualized" to describe the communication from the opposite point of
view. For handling multiple parties, this paper proposes a model where one
gives a global description of a session which is then "projected" to local
descriptions of the individual parties.

"Asynchrony" refers to the idea that a "send" doesn't need to immediately match
its "receive". Instead, messages are stored in a queue. The typical example is
TCP. In this paper, it's actually not clear to me how the main technical
details relevant to the treatment of asynchrony fit together.

There are constraints imposed on a global type to prevent messages from being
confused with the wrong type. For instance, if, on the same channel, A sends an
integer to B right before C sends a boolean to B too, then B could be receiving
either and could not tell which (this is the "(II) Bad" case in Fig 5).
However this example is "bad" even in a synchronous setting: A and C are racing
to communicate with B either way.

- I'm not even sure how to interpret Fig 5, and more generally what those
  ordering constraints mean exactly.
- What is an example of ordering constraint that distinguishes synchrony from
  asynchrony?

The first requirement of global types is linearity: intuitively, communication
along each channel must be causally ordered. I think I will have forgotten what
that means tomorrow.

The second requirement, coherence, comes from a notion of "projection". Given
a participant name p, we can project a global type G to a local type G^p
describing the behavior of p. This projection (\G -> G^p) is a partial
function, and when G^p is defined, we say that G is coherent.

The two causes of partiality are:
1. in the projection of a choice G = (p1 -> p2 : (G1 + G2)), if p is neither p1
   nor p2, then the projections of all suffixes (G1^p and G2^p) must be equal,
   corresponding to the idea that participant p does not observe directly
   the exchange between p1 and p2.
2. in parallel composition, (G1 || G2), p must appear in at most one of G1 and
   G2, meaning that individual participants in a session behave sequentially.

Another important feature of this system is that it is higher-order,
meaning that a capability (channels corresponding to a session) can itself be
sent to another process, which can continue communicating on the received
session.

The type system looks straightforward. For safety/progress, things become
more interesting with the addition of run-time queues to model asynchronous
message-passing.

Looking at the related work, the approach to "multiparty" communications using
a "global type" seems their most novel contribution. There was previous work on
typed pi-calculus/mobile processes that did offer some notions of "causality"
and probably also models "multiparty" in some other way.
