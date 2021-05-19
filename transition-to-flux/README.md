### starting transition to Flux-capable matrix machines

In this notebook

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/transition-to-flux/refactor-variation3.ipynb

we refactor `variation-3` notebook from https://github.com/anhinga/julia-notebooks/tree/main/grimoire-team/variations

along the lines of https://github.com/anhinga/julia-notebooks/tree/main/grimoire-team/refactor

We also take into account the `softmax-and-more` study from https://github.com/anhinga/julia-notebooks/tree/main/images-as-matrices

and replace `exp` with `x -> x+1` in softmax (in our case this does seem crisper/better).

We also produce animated gifs reflecting the resulting dynamics (animated gifs are not posted, there is some flicker, but
people who tolerate flicker well should be able to easily reproduce these gifs and see the details of the dynamics).

However, when we start trying to create a function computing some gradients in the cell which follows cell 38, things don't work:

```julia
# This does not explicitly break, but is taking forever
# The next step is to figure out the configuration, where an equivalent of this works
grads = gradient(() -> loss(img_gray, p_with_start_at_one_im3), params(img_gray))
```

The next step is to figure out what needs to change to make this and other gradient computations work.
