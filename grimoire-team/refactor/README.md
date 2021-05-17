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

---

Note that we can get rid of `Interpolations` package if we feel like it. E.g. to interpolate array `c` something like
the following function would work:
```julia
function h_c(x,y)
    dx=mod(x,1)
    dy=mod(y,1)
    x_left = floor(Int,x)
    y_left = floor(Int,y)
    x_right = x_left + 1
    y_right = y_left + 1
    c[x_left,y_left]*(1-dx)*(1-dy) + c[x_left,y_right]*(1-dx)*dy + c[x_right,y_left]*dx*(1-dy) + c[x_right, y_right]*dx*dy
end
```

---

This is the refactor done with our our linear interpolation and in a more functional way.

At the moment GitHub even seems to render it OK:

https://github.com/anhinga/julia-notebooks/blob/main/grimoire-team/refactor/refactor-exercise1.ipynb

(`nbviewer` rendering works now as well, the link is below; was: whereas the `nbviewer` seems at the moment to suffer from

https://github.com/jupyter/nbviewer/issues/979)

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/grimoire-team/refactor/refactor-exercise1.ipynb

---

Continued here (refactor 2 of exercise 2):

https://github.com/anhinga/julia-gif-art/tree/main/exercise2
