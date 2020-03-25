# Compositional shape analysis by means of bi-abduction

## Summary

This paper introduces a novel method of performing a compositional static analysis, using bi-abduction".
It combines abduction, which infers an "anti-frame", the missing part of the _pre-condition_, with inferring "frames", an extra part of the _post-condition_.
Furthermore, this analysis is done in the context of separation logic, which allows for these specifications to be small and compositional.

There are several steps in the overall analysis.

At the lowest level, there is an algorithm for abduction, defined using a proof system.
This algorithm tries to minimize the footprint of the anti-frame, but doesn't always find the best solution.
For scalability purposes, the anti-frames avoid disjunctions, and they find that this imprecision is acceptable for their purposes.

Next, they combine the abduction algorithm with a standard frame-inference algorithm.
Notably, to compare solutions, the solutions are biased to be ordered by the _anti-frame_ first.
This is due to their application, which is mostly used for inferring preconditions.

Then they introduce the shape analysis itself.
This seemed quite technical and I wasn't sure which parts were novel or important, so I skipped much of it.

The paper ends with several case studies, which seem pretty sweet.
