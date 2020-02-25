# Summary for *A Language with Distributed Scope,* Luca Cardelli, POPL 1995.

This paper presents Obliq, a minimal yet general-purpose object-oriented programming language designed to support concurrent applications. Note that the paper chooses to frame itself as a language for *distributed* applications (i.e. processes which communicate over a network) but it does not consider the typical issues that we associate with that term today, such as tolerance to node failures and network partitions. (See end of section 2: "There is no automatic recovery from network failures.") The fundamental issues addressed seem to be rather about concurrency, and so I prefer to see this paper as a concurrent programming framework.

The basic primitive in Obliq is an *object*. Objects consist of data fields and methods, which are all mutable and dynamically typed. Objects stand on their own, in the sense that they contain copies of their methods (rather than e.g. being instances of a class which provides their methods). However, they are not self-contained because methods are allowed to reference and alias into other objects. So, for example, calling one method on an object may cause it to try to access another object that is located somewhere else.

As far as I can tell, there seem to be two main technical contributions in this work:

1. The first is to apply *lexical scoping* in the concurrent setting. Today lexical scoping is second-nature in most languages, but in the past, it was not obvious: many languages used *dynamic scoping* where the referent of a variable could not be determined statically from the syntax of the language, but rather was determined dynamically by whatever it was bound to at runtime. The idea of this paper is that lexical scoping for concurrent objects allows more predictable and controllable behavior, as opposed to when variable names might refer to anything (somewhat unpredictable) at runtime. I hope I am not saying anything too egregiously wrong :)

2. The second is the treatment of concurrent access to objects. It is assumed that multiple objects may be executing concurrently, and so one object may then try to access the methods of another object while it is executing, and so on. So the language provides a number of ways of to make sure that concurrent data structures and operations can be implemented correctly, without deadlocks, data races, or breaking data invariants (see Sections 2.4-2.7). The primary feature of note here is the *serialized* keyword. It is a modified form of a mutex to guarantee that objects are accessed in an atomic manner. But the implementation cannot simply have one mutex for the object, because that would result in deadlock if one method calls another method. So the choice that is made is that external calls to an object always require the mutex, whereas interal calls (the object calling itself) do not require access. Another keyword is *protected,* which makes sure that a method is immutable so that other threads (e.g., clients) cannot overwrite the method, thus destroying the application.

# Questions

- Am I correct to assert that the issues in this paper are about concurrency, not distribution? At the time in 1995, was it not clear to people that concurrency and distribution were different? How have these terms evolved?

- Typing in Oblique is dynamic, and it is even the case that you can override methods of objects at runtime. So my question is, does that negate the benfits of lexical (static) variable scoping? What does lexical scoping really buy us, anyway, concretely? I am not sure I got that from the paper.

- I also had trouble understanding the introduction and the "bottom line"; I only felt I started to understand once I read Section 2 and the example programs in Section 4.

- What fields of PL did this paper influence? What are some things today that can be traced back to the ideas of this paper?
