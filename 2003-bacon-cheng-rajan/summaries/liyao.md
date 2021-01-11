## General comments

This paper shows that GC can be practical for real-time systems.
It presents a technical feat rather than a conceptual idea,
which seems a bit surprising for a POPL paper.

The design of GCs is rife with trade-offs, and this paper carefully
explains how their hybrid approach navigates the space to satisfy
"real-time" criteria. The detailed comparison with existing work
and the rich benchmarking section challenge (apparently) common ideas about
how GCs should be designed and evaluated.

---

## Details

Section 2 presents four main problems with existing designs: fragmentation,
high space overhead, uneven mutator utilization, and inability to handle large
data structures. The least obvious one is uneven mutator utilization.
I'm not sure I get it, but I think the trade-off is that time-based scheduling
leads to tasks taking predictable time regardless of their memory usage,
whereas work-based scheduling means that high-memory tasks
are much slower than low-memory ones, and real-time constraints are somehow not
adapted to that.

Section 3 presents the GC architecture. The individual components don't look
particularly surprising. I would say it's more about the ingenious combination
of techniques to address all of the problems mentioned earlier.

Section 4 gives some formulas to estimate CPU utilization and memory usage
in a GC, under time- and work-based scheduling. I found it very dense because it
isn't clear to me what the various quantities represent exactly (in particular,
I'm constantly second-guessing whether rates are relative to total time or
mutator time or collector time). They're not the kind of formulas you can
blindly input in a calculator, but they do provide some support to think more
rigorously and quantitatively about GC performance.

Section 4.5.3 is a little funny:

> A robust real-time collector should ...
> We have not done this.

The measurement section (Section 7) is the most interesting, the practical
bent of the paper means that the numbers really put everything into
perspective, and the graphs are quite convincing about the "evenness"
of time-based scheduling.
