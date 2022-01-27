# Multiple Facts for Dynamic Info Flow

* Faceted values - dynamic mechanism for providing information flow security 
	* benefit of multi-process execution with the efficiency of single-process execution (a novel contribution, since many conjectured prior to this work that the runtime overhead for dynamic info flow would always incur expensive runtime overhead)
	* pair of two raw values that contain low and high confidentiality information
* Existing folklore : dyanmic info flow analysis is not sound in the presence of implicit flow (not true
* Solution to mechanism failures - multiprocess execution - simultaneously execute two copies of the target program

* Projection property - single faceted computation simulates multiple non-faceted computations


## Questions
* Is it possible to bring the benefits to faceted execution to general concurrent programming (since it seems like in certain cases it guarantees better performance)?
* What are other 2-safety properties? 
* Do current browsers employ this technique? If not, what are the current challenges in enforcing info flow security for the web?
