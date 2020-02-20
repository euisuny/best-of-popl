## Obliq: A language with distributed scope

Very nice read! The way I understand it, this is the first (or one of
the first) lexically scoped languages for distributed computation. In
the context of distributed computation, code and data moves around
between different sites over the network. This introduces all sorts of
problems when designing programming languages. Making the language
lexically scoped makes programs predictable and more secure, as
computations that are sent to be executed elsewhere, cannot bind with
variables in the remote site.

Another important property of the language is that it is
network-agnostic, in the sense that a program can be evaluated no
matter where different threads are located. It is not clear if the
language offers any support for network-failures though.

From what I understand they have also developed a compiler for this
language that is pretty efficient with regards to the amount of
resources that it sends over the network.

### Notes/Questions

- The language is prototype based OO and doesn't support
  delegation/hierarchies, since this would really complicate
  implementation.
- It seems to be very difficult to reason about the performance of
  programs in this language, since a local object might lead to
  arbitrarily(?) many redirections and network accesses.
- It feels that their treatment of concurrency issues (like deadlocks,
  races) is not adequate. They offer some simple locks to make objects
  serializable and some protection from deadlocks by restricting what
  one can do with a lock and that's it.
- The programming style in Obliq seems pretty weird. Does anyone know
  of other prior languages that look like that? E.g. the sieve program
  is neat, but pretty weird to come up with.
- I really like that this paper is written completely with examples.
