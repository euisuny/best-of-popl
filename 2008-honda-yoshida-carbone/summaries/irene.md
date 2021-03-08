# Multiparty Asynchronous Session TYpes

This paper presents an extension to two-party session types to multiparty asynchronous sessions. Session types are a useful abstraction for conversations between communication-centered applications. Intuitively, a session is a series of interactions that serve as a unit of conversation. These are represented as types over a variant of pi-calculus that has multi-channel processes which support asynchronous communication between multiple parties.

_Global scenarios_ are used to encode error-free conversations between multiparty sessions. The key idea in enabling asynchronous session types is providing a liberal interpretation of the preorder imposed on the prefixes of the communications. In asynchronous communication, messages to channels may not arrive in order, so this sequencing order is imposed only on the actions of the same participant in ordered prefixes. 

For efficient type-checking, local types are used. _Local types_ describe local behavior of processes, and global types are projected onto them. A global type is coherent if it is linear and the projection is well-defined, and coherence is necessary for consistency of the type system.

The Figure 5 (II), (IO) labels feel a little unnecessary because it’s also indicated by the alphabetical labels (A -> B, B -> C, etc.). 

I really appreciated the presentation in the paper, the examples and discourse make the technical contributions intuitive and fun to follow.
