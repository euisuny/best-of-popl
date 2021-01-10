# A Real-time Garbage Collector with Low Overhead and Consistent Utilization

## Summary

This work presents a tool for hard real-time garbage collection in Java, and experimentally evaluates the technique. The motivation is that garbage collection is infeasible for hard real-time systems, but could be done more intelligently to try to conform to real-time requirements. One challenge is to limit copying (to keep time overhead minimal), but not to eliminate it entirely (since copying is needed to avoid fragmentation to make space overhead manageable).

## Questions

1. This question is both the most basic and a bit confrontational. This paper is from 2003. Since then, in 2020, the status quo is that for hard real-time and embedded systems, garbage collection is just a no-go and people are only willing to stick with languages like C/C++ or Rust. Why did this research direction fail to reach the mainstream? One possible answer is that the memory overhead (1.6-2.5), while impressive, is just not good enough for hard real-time and that people want complete control over memory (0 overhead).

2. One of the core motivating discussions it that GC without copying suffers from high memory overhead due to fragmentation. What is going on here in more detail, how does copying in a typical GC work?

3. What does it mean for GC to be provably real-time? I imagine it means that you can put a provable bound on GC time-per-call, or something like that. However, is it possible that there is a "failure case" where either garbage grows exponentially (garbage collector fails to clean up), or the garbage collector fails to satisfy the time bound? Does such a failure case exist for any garbage collection procedure?

Actually you could always just allocate a ton of memory and cause any GC to fail (run out of space), so I am not sure the question is well-defined, in current form, but it is interesting.
