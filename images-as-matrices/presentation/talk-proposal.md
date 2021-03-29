## Multplying monochrome images as matrices: A*B and softmax

---

We can interpret monochrome images as matrices KxM and MxN and combine them via
matrix multiplication. It turns out that results are often visually interesting,
especially if we normalize rows of the left-hand-side matrix and columns of the
right-hand-side matrix with softmax before taking the product.

---

It would be great to understand the properties of matrix multiplication better.
This seems to be particularly worthwhile because matrix multiplication plays
a prominent role in Transformers, a class of machine learning models invented in
2017 and responsible for many recent breakthroughs including GPT-3. Sometimes,
the rows of the left-hand-side matrix are softmax-normalized in order to
use them as probabilities.

One can interpret a monochrome image as a matrix (the size of the matrix depends
on the resolution of the image in question, so one should rescale the image in question
as desired). I decided to explore whether matrix products of monochrome images are
visually interesting. I used JuliaImages packages, Julia LinearAlgebra facilities and 
Julia Jupyter notebooks.

I looked at standard Julia test images, such as "mandrill" and "jetplane",
and discovered that there is plenty of visually interesting information
in the matrix products. I used the scaling of pixel values which is also used
by ImageView.imshow methods.

It turned out that the matrix products were particularly informative and had a lot
of visible fine structure, if one softmax-normalized rows of the left-hand-side matrix 
and columns of the right-hand-side matrix before taking the product. The
images looked slightly toned-down and striped after normalization, but not too different visually, however
the products were drastically different. Note that in Transformer models one usually
applies softmax only on one side, but this turns out to be insufficient for our
visual exploration of matrix products.

I like the resulting images as visual art, and I think this might point to some
interesting novel ways to obtain visual art by mathematical transformations.

I also hope this might eventually be of help as people try to achieve better understanding
and more fine-grained control of our machine learning models.

The markdown file commenting the Julia notebook and elaborating on machine learning connections is posted at 
https://github.com/anhinga/julia-notebooks/blob/main/images-as-matrices/presentation/commentary.md
