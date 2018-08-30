---
layout: default
use_math: true
---

# Linear Regression

The linear regression class is implemented in ``lib/linreg.py``.  It utilizes Newton's method rather than gradient descent.  Ng discusses Newton's method in his older grad course lecture [here](https://www.youtube.com/watch?v=nLKOQfKLUks) but seems to have taken it out of his newer series lecture series.

This seems to be an important omission since I found that gradient descent had convergence problems.  Specifically, I generated noise free data using a 3rd order polynomial equation.  When I gave gradient descent the data with a 4th or 5th order polynomial, it was not able to converge to a solution that zeroed out the unecessary 4th and 5th order terms.  Newton's method was able to find the solution in only a few iterations.

Learning curves are generated using ``fake-data/modsel-gauss.py`` for data generated using ``fake-data/xygen-gauss.py``.  The ``modsel`` script allows the polynomial order and regularization parameters to be adjusted in order to find the best model fit.  Interpretation of the learning curve results and techniques for selecting the model order are discussed in Ng's *excellent* videos in Section 10 of his [lecture series](https://www.youtube.com/playlist?list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN).





