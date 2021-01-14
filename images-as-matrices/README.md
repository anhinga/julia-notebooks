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
