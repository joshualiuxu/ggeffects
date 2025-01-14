# ggeffects 1.0.1.001

## General

* `pretty_range()` and `values_at()` can now also be used as function factories.

# ggeffects 1.0.1

## General

* Fixed CRAN check issues.
* Added argument `interval` to `ggemmeans()`, to either compute confidence or prediction intervals.

# ggeffects 1.0.0

## New supported models

* `averaging` (package **MuMIn**)

## New functions

* `pool_predictions()`, to pool multiple `ggeffects` objects. This can be used when predicted values or estimated marginal means are calculated for models fit to multiple imputed datasets.

## General

* The function `residualize_over_grid()` is now exported.
* The back-transformation of the response-variable (if these were log- or square root-transformed in the model) now also works with square root-transformations and correctly handles `log1p()` and `log(mu + x)`.
* Since standard errors were on the link-scale and not back-transformed for non-Gaussian models, these are now no longer printed (to avoid confusion between standard errors on the link-scale and predictions and confidence intervals on the response-scale).

## Bug fixes

* Fixed issue for mixed models when predictions should be conditioned on random effects variances (e.g. `type = "random"` or `"zi_random"`), but random effects variances could not be calculated or were almost zero.
* Fixed issue with confidence intervals for `multinom` models in `ggemmeans()`.
* Fixed issue in `ggemmeans()` for models from *nlme*.
* Fixed issue with `plot()` for some models in `ggeffect()`.
* Fixed issue with computation of confidence intervals for zero-inflated models with offset-term.

# ggeffects 0.16.0

## Breaking changes

* Package _insight_ since version 0.9.5 now returns the "raw" (untransformed, i.e. original) data that was used to fit the model also for log-transformed variables. Thus, exponentiation like using `terms = "predictor [exp]"` is no longer necessary.

## New supported models

* `mlogit` (package **mlogit**)

## General

* `plot()` now can also create partial residuals plots. There, arguments `residuals`, `residuals.type` and `residuals.line` were added to add partial residuals, the type of residuals and a possible loess-fit regression line for the residual data.

## Bug fixes

* The message for models with a back-transformation to the response scale (all non-Gaussian models), that standard errors are still on the link-scale, did not show up for models of class `glm` since some time. Should be fixed now.
* Fixed issue with `ggpredict()` and `rlmerMods` models when using factors as adjusted terms.
* Fixed issue with brms-multi-response models.

# ggeffects 0.15.1

## New supported models

* `mclogit` (package **mclogit**)

## Bug fixes

* Fixed issues due to latest *rstanarm* update.
* Fixed some issues around categorical/cumulative *brms* models when the outcome is numeric.
* Fixed bug with factor level ordering when plotting raw data from `ggeffect()`.

# ggeffects 0.15.0

## Changes to functions

* `ggpredict()` gets a new `type`-option, `"zi.prob"`, to predict the zero-inflation probability (for models from *pscl*, *glmmTMB* and *GLMMadaptive*).
* When model has log-transformed response variable and `add.data = TRUE` in `plot()`, the raw data points are also transformed accordingly.
* `plot()` with `add.data = TRUE` first adds the layer with raw data, then the points / lines for the marginal effects, so raw data points to not overlay the predicted values.
* The `terms`-argument now also accepts the name of a variable to define specific values. See vignette _Marginal Effects at Specific Values_.

## Bug fixes

* Fix issues in cluster-robust variance-covariance estimation when `vcov.type` was not specified.

# ggeffects 0.14.3

## General

* Fixed issues to due changes in other CRAN packages.

# ggeffects 0.14.2

## General

* *ggeffects* now requires _glmmTMB_ version 1.0.0 or higher.
* Added human-readable alias-options to the `type`-argument.

## Bug fixes

* Fixed issue when log-transformed predictors where held constant and their typical value was negative.
* Fixed issue when plotting raw data to a plot with categorical predictor in the x-axis, which had numeric factor levels that did not start at `1`.
* Fixed issues for model objects that used (log) transformed `offset()` terms.

# ggeffects 0.14.1

## General

* Reduce package dependencies.
* New package-vignette _(Cluster) Robust Standard Errors_.

## New supported models

* `mixor` (package **mixor**), `cgam`, `cgamm` (package **cgam**)

## Bug fixes

* Fix CRAN check issues due to latest *emmeans* update.

# ggeffects 0.14.0

## Breaking Changes

* The argument `x.as.factor` is considered as less useful and was removed.

## New supported models

* `fixest` (package **fixest**), `glmx` (package **glmx**).

## General

* Reduce package dependencies.
* `plot(rawdata = TRUE)` now also works for objects from `ggemmeans()`.
* `ggpredict()` now computes confidence intervals for predictions from `geeglm` models.
* For *brmsfit* models with `trials()` as response variable, `ggpredict()` used to choose the median value of trials were the response was hold constant. Now, you can use the `condition`-argument to hold the number of trials constant at different values.
* Improve `print()`.

## Bug fixes

* Fixed issue with `clmm`-models, when group factor in random effects was numeric.
* Raw data is no longer omitted in plots when grouping variable is continuous and added raw data doesn't numerically match the grouping levels (e.g., mean +/- one standard deviation).
* Fix CRAN check issues due to latest *geepack* update.

# ggeffects 0.13.0

## Breaking Changes

* The use of `emm()` is discouraged, and so it was removed.

## New supported models

* `bracl`, `brmultinom` (package **brglm2**) and models from packages **bamlss** and **R2BayesX**.

## General

* Updated package dependencies.
* `plot()` now uses dodge-position for raw data for categorical x-axis, to align raw data points with points and error bars geoms from predictions.
* Updated and re-arranged internal color palette, especially to have a better behaviour when selecting colors from continuous palettes (see `show_pals()`).

## New functions

* Added a `vcov()` function to calculate variance-covariance matrix for marginal effects.

## Changes to Functions

* `ggemmeans()` now also accepts `type = "re"` and `type = "re.zi"`, to add random effects variances to prediction intervals for mixed models.
* The ellipses-argument `...` is now passed down to the `predict()`-method for *gamlss*-objects, so predictions can be computed for sigma, nu and tau as well.

## Bug fixes

* Fixed issue with wrong order of plot x-axis for `ggeffect()`, when one term was a character vector.

# ggeffects 0.12.0

## Breaking Changes

* The use of `ggaverage()` is discouraged, and so it was removed.
* The name `rprs_values()` is now deprecated, the function is named `values_at()`, and its alias is `representative_values()`.
* The `x.as.factor`-argument defaults to `TRUE`.

## General

* `ggpredict()` now supports cumulative link and ordinal *vglm* models from package **VGAM**.
* More informative error message for *clmm*-models when `terms` included random effects.
* `add.data` is an alias for the `rawdata`-argument in `plot()`.
* `ggpredict()` and `ggemmeans()` now also support predictions for *gam* models from `ziplss` family.

## Changes to Functions

* Improved `print()`-method for ordinal or cumulative link models.
* The `plot()`-method no longer changes the order of factor levels for groups and facets.
* `pretty_data()` gets a `length()` argument to define the length of intervals to be returned.

## Bug fixes

* Added "population level" to output from print-method for *lme* objects.
* Fixed issue with correct identification of gamm/gamm4 models.
* Fixed issue with weighted regression models from *brms*.
* Fixed broken tests due to changes of forthcoming *effects* update.

# ggeffects 0.11.0

## General

* Revised docs and vignettes - the use of the term _average marginal effects_ was replaced by a less misleading wording, since the functions of **ggeffects** calculate marginal effects at the mean or at representative values, but not average marginal effects.
* Replace references to internal vignettes in docstrings to website-vignettes, so links on website are no longer broken.
* `values_at()` is an alias for `rprs_values()`.

## New supported models

* `betabin`, `negbin` (package **aod**), `wbm` (package *panelr*)

## Changes to functions

* `ggpredict()` now supports prediction intervals for models from *MCMCglmm*.
* `ggpredict()` gets a `back.transform`-argument, to tranform predicted values from log-transformed responses back to their original scale (the default behaviour), or to allow predictions to remain on log-scale (new).
* `ggpredict()` and `ggemmeans()` now can calculate marginal effects for specific values from up to three terms (i.e. `terms` can be of lenght four now).
* The `ci.style`-argument from `plot()` now also applies to error bars for categorical variables on the x-axis.

## Bug fixes

* Fixed issue with *glmmTMB* models that included model weights.

# ggeffects 0.10.0

## General

* Better support, including confidence intervals, for some of the already supported model types.
* New package-vignette _Logistic Mixed Effects Model with Interaction Term_.

## New supported models

* `gamlss`, `geeglm` (package **geepack**), `lmrob` and `glmrob` (package **robustbase**), `ols` (package **rms**), `rlmer` (package **robustlmm**), `rq` and `rqss` (package **quantreg**), `tobit` (package **AER**), `survreg` (package **survival**)

## Changes to functions

* The steps for specifying a range of values (e.g. `terms = "predictor [1:10]"`) can now be changed with `by`, e.g. `terms = "predictor [1:10 by=.5]"` (see also vignette _Marginal Effects at Specific Values_).
* Robust standard errors for predictions (see argument `vcov.fun` in `ggpredict()`) now also works for following model-objects: `coxph`, `plm`, `polr` (and probably also `lme` and `gls`, not tested yet).
* `ggpredict()` gets an `interval`-argument, to compute prediction intervals instead of confidence intervals.
* `plot.ggeffects()` now allows different horizontal and vertical jittering for `rawdata` when `jitter` is a numeric vector of length two.

## Bug fixes

* Models with `AsIs`-conversion from division of two variables as dependent variable, e.g. `I(amount/frequency)`, now should work.
* `ggpredict()` failed for `MixMod`-objects when `ci.lvl=NA`.
