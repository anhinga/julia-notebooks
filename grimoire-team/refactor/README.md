### The first refactor according to design notes.

---

Strangely enough I might have a workaround for the GitHub bug in rendering Jupyter notebooks (see https://github.com/anhinga/github-tests). 

When I said "duplicate tab", the resulting notebook was shown!

This needs to be investigated further.

(**Remark:** this effect observed last night does not reproduce today.)

---

Meanwhile, the usual workaround:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/grimoire-team/refactor/refactor-exercise2.ipynb

This is the first attempt at refactor according to https://github.com/anhinga/julia-notebooks/blob/main/grimoire-team/design-notes.md

This works nice, although `LinearInterpolation` does seem to produce a tiny bit of smoothing for better or for worse 
(`ConstantInterpolation` should just more or less reproduce what we had before, but without meaningful derivatives).
