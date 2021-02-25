### Repository for various Julia Jupyter notebooks

To use Julia within Jupyter notebooks, one needs 
  * to have Anaconda installed (for Jupyter)
  * to have a version of Julia installed
  * and then to add `IJulia` package:

https://github.com/JuliaLang/IJulia.jl

Then when one creates a new Jupyter notebook in a browser, one would have an option to create it in Julia.

If one adds `IJulia` package for multiple co-existing versions of Julia, one would be able to choose among those versions each time one creates a new Jupyter notebook in a browser. 

(One might need to `build IJulia` in addition to adding it, if things don't "just work", and while 1.4.1 and 1.5.2 co-exist nicely, 1.5.3 replaces 1.5.2 instead of co-existing, one can `build IJulia` inside 1.5.2 to get it back as an option instead of 1.5.3 - all this is observed on Windows 10.) 

### Displaying Jupyter notebooks in GitHub

Sometimes, GitHub does not render Jupyter notebooks correctly. If you encounter this problem, use `nbviewer`.

See https://github.com/anhinga/github-tests for details.
