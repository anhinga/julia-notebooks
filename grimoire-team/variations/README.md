### combining `grimoire` warps with multiplying images as matrices

Compare cells 11 and 16 in

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/grimoire-team/variations/variation-3.ipynb

with cells 43 and 82 in

https://nbviewer.jupyter.org/github/anhinga/github-tests/blob/main/Untitled.ipynb

Note that the effect is much more pronounced with softmax normalization.

---

A longer exploration, composing this fixed set of operators more and exploring the expressive power of that a bit:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/grimoire-team/variations/variation-4.ipynb

There is some code duplication, because I have not done refactoring which I suggested in

https://github.com/anhinga/julia-notebooks/blob/main/grimoire-team/design-notes.md

The beginning starts with the content of the `variation-3` notebook, as I decided it is the easiest to include it here.
