## Combinators for Bi-Directional Tree Transformations

This is a pretty well-written and interesting paper. I like that it is
driven with examples of combinators of increasing complexity. However
after some point it became slightly too dense for me.

The main idea is that they define a semantic framework for working
with bi-directional transformations and then they define specialized
combinators for bi-directional transformations on trees.

### Notes/Questions:

- Does anyone know what happened to this Harmony project?

- Does anyone know anything about the problem of inverting joins? (It
  is posed as an interesting problem in the introduction)

- I don't understand why the approach is linguistic...

- Why is the footnote in page 2 important (about not needing a trace
  of modifications). It would seem that in order to have an "undo"
  functionality (e.g. when editing an XML document) one would like to
  have a trace of modifications.

- I don't understand the remark about recursive lenses not being
  total.

- About `prune`. It seems that an empty tree that is pruned will end
  up having the child that was pruned after putback. That doesn't seem
  intuitive. Is there any reason for that?

- About `hd` and `tl`. It seems that the way they are written, after
  the putback the tree will have the whole tree `d` in tail or head. I
  probably misunderstand something.

- Can we follow the filter putback evaluation example together? It
  seems too complicated with all this notation.

- In the previous from last paragraph of the conclusion they make a
  claim that questions about expressiveness tend to have trivial
  answers when phrased semantically. I don't understand this claim.
