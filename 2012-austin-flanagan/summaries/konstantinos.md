## Multiple Facets for Dynamic Information Flow

I started reading this paper in hopes that I will be able to get some lessons 
for my research related to the shell, since the shell is also very dynamic in nature,
and therefore it is not possible to statically analyze its behavior.

I am not sure it is that applicable, but the following key points seem generalizable and valuable:

- False positives in dynamic analysis (or uncertainty whether there is a violation),
  are THE WORST, since they require fail-stop, which is terrible and cannot be used in practice.
  No one would add a dynamic analysis to their system if it has false positives and can fail-stop.

- Hyperproperty monitoring requires simulating many worlds in general. In their case they found an
  optimization that gives the same results as simulating many worlds, but is much more efficient.
  I don't think they have worst-case complexity improvement over the 2^n case though.

- I didn't understand their theorem in detail, but it seems important in those cases to prove that
  whatever monitoring you do is equivalent to simulating all the worlds (otherwise the analysis will have false-positives/negatives).

- Unrelated Q: What are other hyperproperties that could be checked dynamically? Does anyone have any idea?
