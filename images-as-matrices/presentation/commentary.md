## Commentrary to "Multplying monochrome images as matrices"

We obtained images like

![symmetric](symmetric.png)

and

![asymmetric](asymmetric.png)

via matrix multiplication.

View the Julia Jupyter notebook in question via this link:

https://nbviewer.jupyter.org/github/anhinga/github-tests/blob/main/Untitled.ipynb

(The notebook itself is at https://github.com/anhinga/github-tests/blob/main/Untitled.ipynb
there is a github bug preventing some Jupyter notebook from rendering correctly, so
one has to use `nbviewer` or its equivalent.)

This is the first notebook in this study, it was created on December 8, 2020 with Julia 1.5.2
on Windows 10. I verified that all this still works with Julia 1.6.0 (but much faster, and
the warning in cell 1 is gone, which is good).

The sketch of the talk proposal itself is at https://github.com/anhinga/julia-notebooks/blob/main/images-as-matrices/presentation/talk-proposal.md

Cell 3: read "mandrill" standard test image

Cell 4: make it monochrome

Cell 5: `im1 = 1*img` - a hack to convert this to `Array{Gray{Float32},2}`

`im1 = convert(Array{Gray{Float32}, 2}, img)` would produce the same result

Cell 8: transposed "mandrill"

Cell 42: `normalize_image` is doing the same transform as `ImageView.imshow` methods

Cell 43: multiply transposed "mandrill" by "mandrill", and show the normalized result (plenty of information in that product, but not an "excessively artistic" image)

Cell 45: read standard "jetplane" test image

Cell 51: remove alpha channel, and make it `Array{Gray{Float32},2}`, as in cell 5 above

Cell 53: multiply "jetplane" by "mandrill", and show the normalized result (plenty of information in that product, but not an "excessively artistic" image)
