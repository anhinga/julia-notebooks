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
