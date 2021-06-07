In the new notebook

https://github.com/anhinga/julia-notebooks/blob/main/flux-may-2021/variation-3/further-flux-variation-3-experiments.ipynb

(in nbviewer, currently requires flush_cache=true flag (yes, this issue again: https://github.com/jupyter/nbviewer/issues/979 )

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/flux-may-2021/variation-3/further-flux-variation-3-experiments.ipynb?flush_cache=true )

we have successfully run a similar experiment, where we took a warped version, and used gradient descent to eliminate
"grains" in the product.

Then we trying to run a more complicated experiments, taking `apply_warp` inside the composition used to compute derivatives (cell 60):

```julia
loss_new(x, y) = norm(value3(apply_warp(warp3, x, pars)) - y)
```

Something is broken. What we noticed here, and in `transition-to-flux` experiments, is that when things are incorrect from the Flux viewpoint, 
it might take foreever before the diagnostics appear, so one might rerun for a smaller task; in this particular case, the diagnostics was
produced eventually, after a few hours. The cell following cell 66 ended up producing the following diagnostics:

```julia
steps!(m_im0, p_m_im0_warped_norm, loss_new, opt2, matrix_sequence, 1)
```
```
Need an adjoint for constructor Base.Iterators.ProductIterator{Tuple{UnitRange{Int64}, UnitRange{Int64}}}. Gradient is of type Matrix{Tuple{Float64, Float64}}
```

From my further experiments, it seems that the current incarnation of Zygote is unhappy with multidimensional array comprenhesion.

It looks like one should use a one-dimensional array comprehension, and then `reshape` (or, if one feels confident, one can create
a **custom adjoint** for the missing functionality).

---

My experiments indicate that a workaround based on `reshape` does work.

One replaces

```julia
[linear_interpolation(warp(x,y,p)) for x in 1:xsize, y in 1:ysize]
```

in the function `apply_warp` with something like this rather ugly construction:

```julia
reshape([linear_interpolation(warp((i-1) % xsize + 1, (i-1) ÷ xsize + 1, p)) for i in 1.0f0:xsize*ysize], xsize, ysize)
```

(Float32 vs. Float64 is another interesting issue here; I am not quite sure about it yet.)
