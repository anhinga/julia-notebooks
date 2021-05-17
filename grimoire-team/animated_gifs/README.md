### Examples of creating an animated GIF

Julia 1.6. Add packages `FileIO` and `ImageMagick` before doing this.

To create a full-sized animated GIF from the array `imgs3` of images displayed in cell 3 of

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/grimoire-team/exercise-3.ipynb

one writes

```julia
using FileIO

full_imgs3 = []
for i in 1:zsize
    push!(full_imgs3, imgs3[i])
end
for i in reverse(2:(zsize-1))
    push!(full_imgs3, imgs3[i])
end

save("test_full.gif", cat(full_imgs3..., dims=3), fps=30)
```

This is the image itself (I observed some latency before it starts working full-speed, but eventually it does):

![animated_mandrill](test_full.gif)

More animated gifs here:

https://github.com/anhinga/julia-gif-art
