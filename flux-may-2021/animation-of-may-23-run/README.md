# animation of May 23 learning process

File `learning-may-23_step6_fps1.gif` - 38 frames, 20 MB, 1 frame per second, each frame corresponds to 6 iterations of ADAM.

while a large animated gif is loading one can see a frame progression in slower tempo

To obtain the animation one continues https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/flux-may-2021/may-23-switch-to-adam.ipynb

```julia
animation_frames = [Gray.(hcat(large_ms[i], value3(large_ms[i]))) for i in 1:length(large_ms)] 
```

One obtains 227 images. It turns out that ADAM process brings us above 1.0 and below 0.0, and animated gif maker hates that.

```julia
> convert(Float32, maximum(animation_frames[227]))
1.0125469f0
> convert(Float32, minimum(animation_frames[227]))
-0.1082513f0
```

So the process of making this animated gif looks as follows:

```julia
clip_float(x) = max(min(x, 1), 0)

using FileIO

full_imgs = []
for i in 1:6:length(animation_frames)
    push!(full_imgs, Gray.(clip_float.(animation_frames[i])))
end

save("learning-may-23_step6_fps1.gif", cat(full_imgs..., dims=3), fps=1)
```
