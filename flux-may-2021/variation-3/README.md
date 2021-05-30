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

Stacktrace:
  [1] error(s::String)
    @ Base .\error.jl:33
  [2] (::Zygote.Jnew{Base.Iterators.ProductIterator{Tuple{UnitRange{Int64}, UnitRange{Int64}}}, Nothing, false})(Δ::Matrix{Tuple{Float64, Float64}})
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\lib\lib.jl:314
  [3] (::Zygote.var"#1723#back#196"{Zygote.Jnew{Base.Iterators.ProductIterator{Tuple{UnitRange{Int64}, UnitRange{Int64}}}, Nothing, false}})(Δ::Matrix{Tuple{Float64, Float64}})
    @ Zygote C:\Users\Fluid3\.julia\packages\ZygoteRules\OjfTt\src\adjoint.jl:59
  [4] Pullback
    @ .\iterators.jl:912 [inlined]
  [5] (::typeof(∂(Base.Iterators.ProductIterator{Tuple{UnitRange{Int64}, UnitRange{Int64}}})))(Δ::Matrix{Tuple{Float64, Float64}})
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface2.jl:0
  [6] Pullback
    @ .\iterators.jl:912 [inlined]
  [7] (::typeof(∂(Base.Iterators.ProductIterator)))(Δ::Matrix{Tuple{Float64, Float64}})
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface2.jl:0
  [8] Pullback
    @ .\iterators.jl:930 [inlined]
  [9] (::typeof(∂(product)))(Δ::Matrix{Tuple{Float64, Float64}})
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface2.jl:0
 [10] Pullback
    @ .\In[3]:17 [inlined]
 [11] (::typeof(∂(apply_warp)))(Δ::Matrix{Float64})
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface2.jl:0
 [12] Pullback
    @ .\In[60]:7 [inlined]
 [13] (::typeof(∂(loss_new)))(Δ::Float64)
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface2.jl:0
 [14] Pullback
    @ .\In[25]:5 [inlined]
 [15] (::typeof(∂(λ)))(Δ::Float64)
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface2.jl:0
 [16] (::Zygote.var"#69#70"{Zygote.Params, typeof(∂(λ)), Zygote.Context})(Δ::Float64)
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface.jl:252
 [17] gradient(f::Function, args::Zygote.Params)
    @ Zygote C:\Users\Fluid3\.julia\packages\Zygote\6HN9x\src\compiler\interface.jl:59
 [18] steps!(x::Matrix{Float32}, y::Matrix{Float64}, loss::typeof(loss_new), opt::ADAM, accum::Vector{Any}, n_steps::Int64)
    @ Main .\In[25]:5
 [19] top-level scope
    @ In[67]:1
 [20] eval
    @ .\boot.jl:360 [inlined]
 [21] include_string(mapexpr::typeof(REPL.softscope), mod::Module, code::String, filename::String)
    @ Base .\loading.jl:1094
```
