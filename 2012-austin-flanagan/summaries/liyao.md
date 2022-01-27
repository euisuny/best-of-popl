Summary

This paper presents a dynamic approach to track information flow,
using *faceted values*, which store together private and public versions
of a value. Faceted evaluation simulates multi-process execution while
being relatively more performant and gracefully handling situations where
previous approaches get stuck.

A faceted value is a triple (k ? V : W) where k is a principal ("one URL"),
V is the private value seen by observers who have access to k, and W is the
public value for unprivileged observers.
When evaluation inspects a faceted value, evaluation branches for each facet,
and the results of all branches are joined together into a faceted value
at the end.

The key theorem is the Projection Theorem: faceted evaluation simulates
regular evaluation for every view.

It is also shown that faceted evaluation generalizes previous semantics
such as no-sensitive-upgrade and permissive-upgrade.
Faceting also supports a form of robust declassification.

---

- More people should use the adjective "mercurial" to talk about security.

- How would

        if x then { y = 1 } else { y = 2 }

  appear to public observers? -> The execution is split and the results are merged afterwards.

- Can't a faceted value contain one facet for every view?
- Does faceted evaluation take each branch only once?
  I guess there are corner cases where we need one execution per view.
