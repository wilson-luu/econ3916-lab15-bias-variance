# The Bias-Variance Tradeoff: Choosing How Flexible a Model Should Be

## Objective
I simulated data from a known nonlinear curve to separate prediction error into bias and variance, compare training error against held-out error across polynomial degrees, and evaluate model selection with k-fold and nested cross-validation.

## Methodology
* Simulated 60 noisy points from a known true curve and decomposed polynomial prediction error into bias squared and variance across 200 fresh samples at six degrees.
* Compared training MSE against held-out MSE on 2,000 new points for polynomial degrees 1 through 15 to locate where overfitting begins.
* Selected polynomial degree using 5-fold cross-validation and inspected fold-to-fold variation alongside the mean error.
* Ran nested 5-fold cross-validation to check whether the smallest CV error gives a fair estimate of out-of-sample error.
* Wrote a reusable `kfold_mse()` function to compute k-fold CV error for any degree and fold count, then checked degrees 4 and 5 using 10 folds.
* Extended the polynomial degree past the interpolation threshold with minimum-norm Legendre fits to observe double descent.

## Key Findings
* In the bias-variance decomposition, variance stayed flat around 0.02 through degree 5 (0.0180 at degree 5) before rising to 0.0994 at degree 15 once bias squared had settled near zero.
* On the 2,000 held-out points, MSE was lowest at degree 5 while training error fell at every step from degree 1 to 15.
* Five-fold cross-validation picked degree 4 with a CV MSE of 0.1401, while nested cross-validation gave a higher estimate of 0.2070 once selection bias was accounted for.
* Using `kfold_mse()` with 10 folds, degree 4 gave a CV MSE of 0.1409 and degree 5 gave 0.1457.
* Past the interpolation point in the take-home challenge, held-out error spiked near 60 parameters and then fell again to 0.3185 under the minimum-norm fit.
