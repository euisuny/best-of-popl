## Summary

### Separation logic

When I was reading the introduction I realized that I needed a crash course on separation logic. So, here is a very rough summary, based on looking briefly at the following papers:

- 2001 best paper (Ishtiq and O'Hearn, one of the foundational papers in separation logic)

- Papers suggested by Irene and Yannick:

  - John Reynolds' Survey: https://www.cs.cmu.edu/~jcr/seplogic.pdf

  - Introduction to this paper: https://www.chargueraud.org/research/2020/seq_seplogic/seq_seplogic.pdf

  - Reynolds' Notes: https://www.cs.cmu.edu/afs/cs.cmu.edu/project/fox-19/member/jcr/www15818As2011/ch1.pdf (I didn't get to this one).

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

Then the bi-abduction part is that, instead of just inferring a weak extra condition under which R holds, we also want to infer the co-version of that. Given P and R, we want to infer both Q and S such that
```
P * Q |- R * S.
```

The ideas in this paper are fundamental to the Infer static analyzer, which has been deployed widely and effectively at Facebook.

### Questions

- The proof rules for solving bi-abduction questions does not give the "minimal" answer, as the author's admit. I'm curious what can be said about the method in terms of expressiveness and completeness.
