# Multiple Facets for Dynamic Information Flow (POPL 2012)

## Summary

This was a great paper! It is part of the line of PL work on information flow security, which aims to prevent secure or private values (e.g., password) from "flowing" into public values through program operations. At the level of single program statements, example flows are assignments (in `x := y`, `y` flows into `x`), arithmetic operations (in `z := x + y`, both `x` and `y` flow into `z`), and any other primitive operation considered, i.e. arithmetic statements, method calls, etc.

An *implicit flow* occurs via the control flow, rather than directly through operations: in `if x { c1 } else { c2 }`, `x` implicitly flows into any variables modified by either `c1` or `c2`, and similarly, in `while x { c1 }`, `x` implicitly flows into any variables modified by `c1`. Surprisingly (to me, at least!) most static and dynamic information flow trackers at the time ignore implicit flows! So the first contribution of this particular work is that they handle implicit flows soundly.

I was only able to understand what implicit flows are (and why they matter) after reading reference 24, which provides a great overview of this problem and empirical study (though it could use a better paper title): *Implicit Flows: Can't Live with 'Em, Can’t Live without 'Em,* Dave King, Boniface Hicks, Michael Hicks, and Trent Jaeger. It turns out that while some true security bugs are due to implicit flows, a huge number of false alarms result from tracking implicit flows. The majority of these false alarms, the authors find, are due to the possibility of throwing exceptions: for example, `if (password is None) throw PasswordNotFoundError` implicitly leaks information about the private variable password. However in most cases, this kind of leakage is acceptable.

Anyway, back to the paper at hand, we just noted that the first problem solved is to handle implicit flows. The second problem solved is to work dynamically. This part is especially about "practical" impact because JavaScript is not statically typed, so retrofitting existing code to be secure requires dynamic solutions.

The proposed solution is very simple to understand (probably contributing to this paper's success): during execution, private values are split into a pair of a private view and a public view. So the values at runtime are something like (I'm making up some ad hoc syntax)
```
type Value = Public(val) | Private(priv_view, pub_viw)
```
and all the operations are lifted to this `Value` type.
The lifting is straightforward: operations are carried out on both private and public views.
Conceptually, a `Public(val)` is just the same as a `Private(val, val)`.
So one could have all values simply be `Private(_, _)`, but the issue is efficiency, the authors do not want a system in which all operations are carried out twice. In case of manipulating purely public values, the operations are only carried out once (see Section 1.1).
I suppose that one could do something slightly fancier like
```
type Value = Public(val) | Private(val) | Diff(priv, pub)
```
where private-only values are also manipulated more efficiently.
This is a dynamic approach because public vs private values are tracked at runtime.
I wasn't sure if the division into `Public(val)` and `Private(priv_view, pub_view)` is also tracked dynamically or if that part is inferred statically.
One could imagine combining both static and dynamic analysis here.

The core technical non-interference property that the paper's system enforces is called termination-insensitive non-interference (TINI) (Section 3.2, Theorem 2). It's a standard property defined in other work, and is a 2-safety property (see section 8) i.e. a hyperproperty, meaning that it is a property of multiple traces: it says that for any two traces which terminate, if they differ only on private values, the public values are the same. This is great, but leaves open the possibility of leaking information via termination. The reference 1 discusses how this leaks more than just a single bit, and you could potentially discover a secret value through observing termination, so this is a serious limitation and important gap for future work. Perhaps there is a technical barrier that makes guaranteeing termination-sensitive non-interference very difficult.

## Questions

1. Why does the paper PDF [on Cormac's website](https://users.soe.ucsc.edu/~cormac/papers/popl12b%20(2011-11-28_16-48-21).pdf) have a big red "0!" written on Figure 4 (page 6, top)?

2. Did I understand the issue with termination-sensitivity correctly? This seems like a serious problem for this approach or for information flow tracking approaches in general (reference 1). Is this unique to this approach? Is it possible to extend this work to be termination-sensitive?

3. In the intro, the paper says that an alternate approach is to "bake security controls into the browser itself" and that "the controls have tended to be fairly minimal." I find this a bit vague. I assume this is talking about essentially sandboxing? What is a representative paper in this approach? Are modern browsers moving in this direction?
(There was a paper at POPL this year on the sandboxing approach to web security: *Isolation Without Taxation: Near Zero Cost Transitions for SFI.*)
