## Design and history notes

The original warping goes back to the beginning of Project Fluid and to this function:

https://github.com/anhinga/fluid/blob/master/may_9_15_experiment/custom_wave_transform.pde

Then my friend did quite a bit of exploration of these motives in Julia (in the early 2020), 
and also brought quite of bit of **relational programming** motives into play. The images
in the first 3 "exercise" notebooks are all due to him, I've just reproduced their generation in
a different context (Jupyter notebooks and such).

Then I've done further work on this in the first half of 2020.

Some images from the `exercise-2` notebook were used at the Boston demoparty in June 2020: https://demozoo.org/graphics/279210/

I would like to both preserve and make publicly available some of the resulting **visual art**,
preserve the key code fragments and ideas, and refactor some of this code for future use.

---

Refactoring should include two things:

1) the `warp` "inverse map", `(x,y)↦(xnew,ynew)`, should be on the level of coords. The access to `img(xnew,ynew)` should be outside the function.
2) all parameters of "warp" functions should be explicit, global variables should be eliminated.

3) It would be better if signatures of various `warp` functions are the same. But they are not always the same - how should we handle that?

   * Probably, we should adopt a uniform discipline of having one dictionary containing all hyperparameters (just like we used a dictionary containing
     unlimited number of parameters in V-value-based DMMs we implemented in Clojure: https://github.com/jsa-aerial/DMM).

4) We also would like to be able to take meaningful derivatives with respect to those hyperparameters. 

   * In this sense, the fact that our `warp` "inverse maps", `(x,y)↦(xnew,ynew)`, are integers to integers is a problem.

   * These maps should be reals to reals, and taking integer approximations `xlow <= xnew <= xhigh` and `ylow <= ynew < yhigh`,
     the resulting image point should be obtained as a function
     `interpolate(img(xlow,ylow), img(xlow, yhigh), img(xhigh, ylow), img(xhigh, yhigh), xnew, ynew)`, and this can change
     continuously with smooth changes of xnew and ynew.

