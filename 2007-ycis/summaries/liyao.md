This work explores provably safe protections against malicious code in
JavaScript.

JavaScript is notable for being used by everyone, and its peculiar execution
model via interaction with the DOM.

They propose to instrument JavaScript code in order to detect potentially
dangerous operations, so that for example the user can be prompted to continue
or stop the execution. One challenge is that JavaScript programs may generate
HTML embedding JavaScript code, so instrumented code must call the
instrumentation function at run time.

The instrumentation is made flexible by making it parametric over a security
policy given as an "edit automaton".
In order to prove the correctness of their solution, the paper presents
a formal model of JavaScript, CoreScript.

The theoretical contribution seems a bit underwhelming for a POPL paper:
the proofs are actually straightforward lock-step simulations.
The instrumentation is not very sophisticated: it only ensures that all
relevant actions pass through the policy module, which is where the
security checks happen, but is treated as a black box.

From reading its award citation, this paper seems more notable for being an
early contribution to the ambitious enterprise of formal methods in browser
security.

I'm surprised this wasn't already a bigger problem in 2007.

---

Dumb questions (after reading the intro and background):

- Is it really necessary to change the code, as opposed to the environment
  that runs it (i.e., have the interpreter intercept functions that can access
  or leak sensitive information)?

- What is an "edit automaton"? What do policies look like?

---

Operational semantics

Good old small-step semantics. The steps are labeled with the actions taken by
the program (e.g., manipulating windows, making requests, modifying cookies).

Q: In rules (5) and (8), why does it make sense to erase variables?

A: This is because the "value actions" produced by that transition relation serve
as labels for the final step relation, but do not actually play a role in the
rest of the semantics. The step function defined in Figure 7 uses those variables.

---

Security policies

An edit automaton takes a word as an input (like a standard automaton)
and also produces a word as an output, symbol by symbol: at every step
the automaton consumes a symbol from the input and produces an edited output,
which may be the same symbol in the common case (no edit), a different one
(edit), or no symbol (deletion).

Such an automaton can be interpreted as an validation function (a valid
word/sequence of actions is not modified by the automaton) or as a rewrite
function (mapping words to words satisfying the policy).

Some examples of policies are given: limiting the number of pop-ups,
and controlling URLs when cookies are used.

I think the "automaton" terminology gave me the wrong expectations.
The point is that it is a trusted function that intercepts actions performed
by a page and may do additional checks and actions, and even refuse to
perform the required action. In their implementation it is an arbitrary
JavaScript function.

---

Instrumentation

> The task of the rewriting process is to (...) redirect all actions through
> the policy module.

It seems a simpler way of doing this is to modify the execution environment to
intercept those actions, but the issue is probably that it requires control of
the browser.

---

Correctness

The two theorems are soundness: the instrumented program respects the policy,
and transparency: programs that already respect the policy have their behavior
unaffected by instrumentation.

The instrumented program is just the original program with some substitutions
of operations, and this relation holds in lock-step throughout execution.
