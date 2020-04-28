# JFlow (1999)

## Summary

This paper presents JFlow, a tool built on top of Java that provides static and dynamic typing to track information flow and enforce data privacy.

The "types" used here are based on the *decentralized label model* which was introduced earlier by Myers and Liskov (*A Decentralized Model for Information Flow Control*, SOSP 1997). At a basic level, a system is thought of as having *principals* (users) and *data.* Data values are labeled with annotations which are basically access control policies. Specifically, each policy has the form `{P: S}` where `P` is a principal who owns the annotation, and `S` is a set of principals which `P` has allowed to access the data.

A data value is then labeled with a *list* of such policies, i.e. `{P1: S1, P2: S2, P3: S3, ..., Pn: Sn}`. This allows combining and manipulating data. For example if two values are added together, the label lists would be concatenated.

As one can imagine, these labels (lists of policies) support a natural notion of subtyping. This can then be used to check (statically) whether a particular principal is allowed to access a certain data value.

The new thing in JFlow, compared to the work on the model, is basically extending this and adding a lot of features to make it a practical programming language. That means e.g. integrating the types with Java types (by combining both types, e.g. `int{P1: S1, P2: S2}`), adding different type inference and type checking mechanisms, integrating with classes and class methods, and supporting runtime annotations (I am less convinced of the latter being useful but I guess it probably is necessary sometimes).

## Questions and Comments

- Very cool work! I love the idea that data access control policies are types, and the whole framework is very elegant.

- The core policy language seems to have only two distinguishing types of users, namely *owners* and *readers*. I wonder if there is work on extending this to more complex permissions e.g. the usual *read*, *write* and *execute* from Linux, or even finer distinctions like *view* vs. *read* (the former means you can see that the data exists but not what its value is, while the latter means that you can read the value).

- I am a little bit surprised by the vagueness of some of the claims in the abstract, intro, and conclusion, e.g. that JFlow is the first framework that is "practical" and the first to "allow reasonable programs to be written in a natural manner". I felt that what is meant by this is not really explained very well. I think it would be better writing to explain more precisely how it is better (e.g. integrates with language features X, Y, and Z; incorporates type inference to simplify annotations, etc.).

- As always I am kind of interested to know how this work's impact continues to today. I guess it is a major landmark language for information flow control. What are some modern information flow control languages and how have they built on this? What are some current research topics?

  I would definitely read a blog post called "JFlow 20 years later" or something like that.
