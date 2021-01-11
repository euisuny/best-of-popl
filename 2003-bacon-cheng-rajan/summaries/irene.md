
This paper introduces a real-time garbage collection for the JVM, with an incrementing, _mostly non-copying_ hybrid collector, and also presents a case for time-based scheduling.
It notes several problems with previous work, such as fragmentation, high space overhead, and uneven mutator utilization.
This is each avoided by 1) (Fragmentation) the use of arraylets and appropriate sized classes, (2) (Space) mostly non-copying algorithm (3) (Uneven mutator utilization) a time-based scheduling policy, and (4) (Large data structures) use of arraylets

Definitely a notable feat during its time, but how fashionable is such methods at this point (how do generational/concurrent GC's scheduling policies usually work?)

Also seems more like a PLDI paper.
