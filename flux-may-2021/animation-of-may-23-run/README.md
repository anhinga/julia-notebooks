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

---

To obtain the loss curve, run

```julia
xrange = 1:length(large_ms)
yrange = [loss(large_ms[i], p_m_im0_warped_norm) for i in xrange]

using Plots

plot(xrange, yrange, fmt = :png)
```

Note that one needs `fmt = :png` if one wants to be able to save the resulting image and use it.
Otherwise, the default "in-page svg graph" works just fine.

See the resulting graph at `loss-curve.png`. Note that we stopped doing steps when the
loss stopped confidently decreasing, so we did not know if it would go all the way to zero.

At the same time, at the loss level we have achieved, the target image `Gray.(p_m_im0_warped_norm)`
have been visually indistinguishable from `Gray.(value3(m_im0))` (the method used to compare
two very similar images visually is to display them rapidly one after another, then
changes should be visible, even when they are not visible side-by-side; I have not
detected any differences between these two images using this method).

---

File `learning-may-23_step6_fps1_colored.gif` - a colorized version of the same animation in false colors
(light purple - delta color above the original image, the lighter the purple, the further above the original image the delta is;
dark green - delta color below the original image, the darker the green, the further below the original image the delta is). 
38 frames, 18 MB, 1 frame per second, each frame corresponds to 6 iterations of ADAM.

---

A Julia Jupyter notebook `visualization-drafts-for-may-23-switch-to-adam.ipynb`: a rather huge notebook (45 MB),
containing all kinds of visualization experiments in a rough draft form (including making of both animations
presented here):

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/flux-may-2021/animation-of-may-23-run/visualization-drafts-for-may-23-switch-to-adam.ipynb

Of particular note are the following cells:
  * Cells 942, 979: making the `learning-may-23_step6_fps1.gif` animation.
  * Cell 1038: the delta between the learned pattern and the original amplified to the maximal contrast.
  * Cells 1041, 1043, 1066, 1071: colorization of the learned pattern
  * Cell 1068: the delta between the warped pattern and the original amplified to the maximal contrast.
  * Cells 1075, 1078: colorization of the delta between the warped pattern and the original.
  * Cells 1081, 1082: the delta between the warped and learned pattern, and its negation, amplified to the maximal constrast.
  * Cells 1083, 1084, 1085, 1086: colorization of the above.
  * Cell 1090: a beautiful mistake (bugs are the best for a digital artist :-)).
  * Cell 1092: the delta between the target product pattern and the original product pattern amplified to the maximal contrast.
  * Cells 1093, 1097: the colorization of the above.
  * Cells 1098, 1103, 1122: making the `learning-may-23_step6_fps1_colored.gif` animation in false colors.
