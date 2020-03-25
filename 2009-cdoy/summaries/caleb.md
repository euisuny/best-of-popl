## "Summary"

I didn't get past the introduction because I had to read up a bit on separation logic instead. So I will briefly state what is separation logic and then where does this paper fall.

### Separation logic

Separation logic is like Hoare logic but allows for stating properties of the entire heap of memory instead of just properties about a specific state. So, the statement

```
P * Q
```

means that the heap is split into two parts, one where P holds and one where Q holds. Atomic predicates allow saying, for example, that the heap consists of exactly one address with a particular value, or one address with a particular value and the rest of the heap as well. You can also define impliciation

```
P -* Q
```
which says, basically, that if you adjoin some heap satisfying P, then the resulting heap satisfies Q.

I guess there is a difference between "separation logic" and "concurrent separation logic" but I did not get that far.

### This paper

This paper is about a compositional and scalable static analysis built on top of separation logic. 

There are some general points to make about the static analysis approach itself. The *compositional* nature means that you analyze different procedures separately and then combine them. But what makes this really challening is that the authors do not assume any sort of global preconditions or postconditions or annotations provided by the user. You just have to infer, for each procedure, what are the possible pre and post conditions that would make sense. There might be weaker and stronger possibilities under different assumptions about the state of memory when the procedure is called. So that is why this is a challenging problem.

The core idea of the static analysis is an idea called *bi-abduction*. The authors state this idea is new, but in the citation for best of POPL award they said it "re-kindled" interest in this, so maybe it was not really new. Anyway, to understand bi-abduction one first must understand abductive inference in the context of separation logic. The idea is, given P and R, to infer some Q such that

```
P * Q |- R.
```

Then the bi-abduction part is that, instead of just inferring a weak extra condition under which R holds, we also want to infer the co-version of that, I think it would be a strongest condition that must *not* hold, or something.

The ideas in this paper are fundamental to the Infer static analyzer, which has been deployed widely and effectively at Facebook.

### ~~~Questions~~~ Comments

I think I needed to spend more time on this paper, 1 hour was not enough.
