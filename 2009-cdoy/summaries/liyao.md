This paper presents a program analysis technique.
As they explain (and emphasize in a recent retrospective on the SIGPLAN blog),
a central challenge they wish to address to make their work scale to large
programs (> thousands LOC).

The main ingredient of this work is *bi-abduction*, which is to infer
an "anti-frame" and a "frame" to complete an entailment
"Δ * anti-frame |- H * frame".

They present an algorithm for bi-abduction decomposed into "abduction"
("anti-frame inference") and "frame inference":
first solve "Δ * anti-frame |- H'" (where H' = H * true),
and then, having found an anti-frame, solve "Δ' |- H * frame"
(where Δ' = Δ * anti-frame).

They then show in detail how to use bi-abduction for shape analysis.
Using numerous examples throughout the paper, they demonstrate
that the results of that algorithm are "good"
(it can really only be evaluated empirically).
