## Multplying monochrome images as matrices

We are trying to explore properties of matrix multiplication in depth, 
and in connection with that we are interpreting monochrome images
as matrices and exploring the structure of the resulting matrix product.

The initial study was done in October 2020 and published as a Julia notebook
in December 2020 in this repository:

https://github.com/anhinga/github-tests

As one can see, a matrix product of two images interpreted as an image does
have an interesting structure, and this structure is particularly rich,
if one normalizes rows of the left matrix and columns of the right matrix
(e.g. by `softmax`).

---

The `scale-invariance.ipynb` tests that the effects are invariant with
respect to image rescaling. Because of the bug described in

https://github.com/anhinga/github-tests

use the following link to view this notebook:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/images-as-matrices/scale-invariance.ipynb

A bit more scale-invariance tests in `scale-2.ipynb` (in particular, making sure that
`softmax` and rescaling commute). Use the following link to view this notebook:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/images-as-matrices/scale-2.ipynb

if it does not work, then:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/images-as-matrices/scale-2.ipynb?flush_cache=true

---

See also the new experiments at

https://github.com/anhinga/julia-notebooks/tree/main/grimoire-team/variations

---

Exploring whether `softmax` normalization can be replaced with a simpler one:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/images-as-matrices/softmax-and-more.ipynb

We see that when in `f.(x) ./ sum(f.(x))` we use `identity` instead of `exp` as `f`, the quality deteriorates
(too dark, less contrast). 

However, if we use `x -> x+1` instead of `exp`, the result is no worse
(perhaps, even slightly better, but that's in the eye of a beholder). So what's important is that
the range of values should start with 1 and not with 0, and the shape of the curve is less important.

So, if one worries about the cost of computing a lot of `exp` functions here,
this cost can be avoided.

---

A resolution study. We rescale the image, and obtain a 512x512 matrix by multiplying 512xN and Nx512 matrices:

https://nbviewer.jupyter.org/github/anhinga/julia-notebooks/blob/main/images-as-matrices/resolution.ipynb

Interestingly enough, there is not much difference between N=512 and N=256 (which probably tells us something
about the true resolution of the original image (with a jetplane in `scale-2` notebook above we did not see
much difference even between N=512 and N=128, so `jetplane` is probably of an even lower true resolution).

Anyway, here we explore N=256,128,64,32,16,8,4,2, and even 1.

