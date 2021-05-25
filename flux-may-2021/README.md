# May 2021 experiments with Julia Flux and machines transforming matrices

### May 23 experiment - use ADAM optimizer to solve an inverse problem

This the Julia notebook in question:

https://github.com/anhinga/julia-notebooks/blob/main/flux-may-2021/may-23-switch-to-adam.ipynb

(If GitHub does not show it, here is this notebook on `nbviewer`:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/flux-may-2021/may-23-switch-to-adam.ipynb)

We consider the following transformation:

```julia
value3(A) = transposed_product(norm_image_columns(x -> x+1, A))
```

`norm_image_columns(x -> x+1, A)` applied to the original monochrome `mandrill`
produces a version with light vertical stripes (cell 13), and then the `transposed_product`
yields our standard pattern (cell 16). At the same time, if we apply `warp3` transform to the
original `mandrill`, we obtain the image at cell 7, and if we apply `value3` transformation
to it, we obtain the image at cell 24.

Now, we would like to start with the original `mandrill` and apply gradient of the difference
between cell 24 and `value3(x)` in the spirit of DeepDream, while hoping to solve the
equation `value3(x) = image at cell 24`.

This is what we tried to do during `second-refactor` exercise here:

https://github.com/anhinga/julia-notebooks/tree/main/transition-to-flux

but we did not have convergence. In the present exercise, we use ADAM optimizer
and we achieve convergence.

Instead of using `train!`, we write a custom-made training loop (cells 37-38):

```julia
import Flux.Optimise: update!

function step!(x, y, loss, opt, accum)
    p = params(x)
    push!(accum, deepcopy(x)) # I am unhappy about the loss of intermediate parameter values
    grads = gradient(()->loss(x, y), p)
    update!(opt, p, grads)
    loss(x, y)
end
```

I don't like the "mandatory mutability" in these Flux functions, and I am trying to mitigate it
by storing all intermediate matrices (of course, this might often be too expensive to do so
in many practical situations; here I am just exploiting the fact that this is a relatively
small problem, and also the fact that it converges after a relatively small number of iterations).

So, if we look at cells 689 to 938, I just perform steps by clicking on cell 934 as many times
as needed (here it was slightly over 200 times), and I inspect all intermediate results at any time,
as I retain all intermediate matrices obtained during this iterative process in `large_ms`.

The system does converge well; it seems that there are multiple solutions to the equation
`value3(x) = image at cell 24` besides the image at cell 7 (which is a known solution).
So, from the viewpoint of `loss` function, it seems that there are many global minima.

The system does find a solution with interesting patterns which is much closer to our starting
point (the original `mandrill`) than cell 7. This solution is in cell 936.

So, with ADAM optimizer we have a reasonable level of convergence, and we do find a solution,
and this solution does have interesting patterns.

For animations of this training process, the loss curve, and colorized visualizations see `animation-of-may-23-run` subdirectory.

We are likely to investigate this setup and its variations further.
