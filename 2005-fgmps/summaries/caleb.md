# Lenses (2005)

## Summary

This paper introduces *lenses,* a compositional approach to bidirectional programming. *Bidirectional programming* refers to a programming paradigm where we want to manipulate two forms of data at the same time, and have them remain consistent. For example, suppose we are creating a document using LaTeX. Then we might want to modify the compiled PDF and have those changes propagated back to the LaTeX source code. Alternatively, perhaps our references are stored both as an XML file and as a .bib file, and we want to be able to modify either of those forms and have the changes propagated to the other.

In these examples, however, it is likely that one view of the data has more information than the other: for example, we probably cannot reproduce the source file of a document solely from the PDF. For this reason, the problem is formalized as the *view update problem* where we distinguish the *concrete* view (e.g. LaTeX source file) from the *abstract* view, which may contain less information. This is an asymmetric formulation: the concrete data can be easily updated without consulting the abstract view, but in order to update the abstract view we need to know the prior concrete view, not just the current abstract view.

A lens is just a pair of functions going back and forth between the two views: a *get* function and a *putback* function that must satisfy some commutativity laws. As stated earlier this is asymmetric: if C is the concrete view and A is the abstract view, then we have

    get: C -> A
    putback: C x A -> C.

The rest of the paper is defining a bunch of combinators for constructing these objects, including complex constructions using recursion.

## Questions

1. Is there a formulation of the view-update problem for bidirectional programming that is *symmetric* instead of asymmetric? Although it is clearly a useful abstraction, it strikes me as a bit odd that the concrete views C and abstract views A are treated differently. I wonder if there is a way to think about transformations betewen arbitrary objects that don't have this asymmetry.

2. I do not understand the insistence on a universe U in the paper, where C and A must be subsets of U, and the *get* and *putback* functions are functions on U. Did anyone see why they formalize things this way?

----

(The last question can be ignored, since I answered it myself, below.)

3. In the introduction, they say there is a tradeoff between expressiveness and robustness, and suggest they make some compromises on expressiveness. But then the actual framework for lenses seems very general, it even has recursion so you should be able to do practically anything. So what do they mean?

**Answer to my own question 3:** I think what they mean by expressiveness isn't severe limits like not having recursion, but rather how restrictive we make the laws that lenses must satisfy. So, because lenses must satisfy a get-put and put-get law, that means some transformations are not allowed. Moreover, requiring the put-put law would mean that even more transformations are impossible to write (like *map*). So this is the tradeoff they are talking about.
