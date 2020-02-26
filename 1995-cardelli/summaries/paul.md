# A Language with Distributed Scope

## Summary

This paper discusses a programming language that supports distributed computation. 
The main novelty of the language is that it has lexical scoping, even on remote machines.
This is nice because distributed computations can easily use data at other execution sites, and because lexical scoping restricts access to remote resources that an angent never had access to.

At the end of the paper, the example of object migration nicely combines many of the features discussed earlier, like cloning protected objects using self-inflicted operations.

## Notes & Questions

- A lot of things discussed in the paper feel unsatisfactory, like the treatment of network failures and synchronization, but I guess this is a realistic programming language.
- Obliq has many features that are rare to see in mainstream languages. Were any of these essential in this work, or were they mostly artifacts of the implementation in Modula-3? It seems to me that these features could be brought to other languages with little trouble.
- The sieve example is interesting. I assume this was just to show off the features of the language? 
- The paper felt pretty sprawling (this language is too real!), and it was hard to find the parts that were important. 
