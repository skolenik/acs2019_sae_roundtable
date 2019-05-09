# Small Area Estimation

**Materials for the small area estimation roundtable at ACS 2019 Data Users Group meeting**

In many social, behavioral or health studies, there may be interest in obtaining estimates for small subgroups of population

- National studies: estimates may be desired for
  * states
  * counties
  * school districts
  * metro areas 
- Statewide studies: estimates for counties, cities, health service areas
- City-wide studies: estimates for neighborhoods
- Establishment sureys: detailed industry by size by region classifications

Given the low sample sizes for small areas (sometimes _n_ = double digits,
sometimes _n_ = single digits, sometimes _n_ = 0), can any reasonable
estimates be obtained? If yes, can any reasonable measures of precision be
attached to these estimates?
Since survey means/proportions may not be available, or are of insufficient accuracy, 
demographic or statistical models have to be used, and weaved into complex survey estimation.

## Concepts

_Small area_

_Direct estimate_

_Synthetic estimate_

_Composite estimate_

## Examples

- Census Bureau: Small Area Income and Poverty Estimates
  * States, Counties, School districts
  * http://www.census.gov/did/www/saipe/
- National Cancer Institute: Small Area Estimates for Cancer Risk Factors and Screening Behaviors
  * States, Counties
  * Combines BRFSS and NHIS (Raghunathan et al. 2007)[https://www.jstor.org/stable/27639878]
  * http://sae.cancer.gov/
- National Center for Health Statistics: NHIS phone use data
  * https://www.cdc.gov/nchs/data/nhis/earlyrelease/Wireless_state_201712.pdf

## Methodologies

### Ratio estimation

Groupwise ratio estimator

### Weighting/calibration

In this method, the estimiates are obtained by (re-)weighting the sample data to the socio-demographic
characteristics of the area of interest. Estimates can be expected to be biased unless the weighting variables
fully account for both sample selection and outcome variation. With a single weighting variable, the method
becomes the group-wise ratio estimator described above.

A strengthed version of the method is due to 
(Lehtonen and Veijanen (2019))[http://isi-iass.org/home/wp-content/uploads/Survey_Statistician_January_2019.pdf].
In their approach, they fit a model (based on the survey data) to the outcome using predictors available 
for the whole population (assuming availability of the population register), obtain predictions,
calibrate the sample to predictions (i.e. reweight the sample so that the weighted sample total of predictions
is equal to the population total of predictions), and obtain calibrated estimates based on the sample
with the actual outcomes.

### Area models

### Unit models

### Multilevel regression with post-stratification

This method (MRP) originated in political science 
((Park, Gelman and Bafumi 2004)[http://www.stat.columbia.edu/~gelman/research/published/parkgelmanbafumi.pdf]),
and has also become popular in health sciences. In this method, a multilevel/mixed model 
of the following structure is fit to **unweighted** survey data:

- random effects are specified at the area level;
- the unit-level (demographic) predictors are only those for which fully interacted population counts
(census tables) are available;
- area level predictors can, but do not have to, be used

Once that model is fit, predictions are obtained that include integration over random effects:
empirical Bayes for frequentist/REML/ML mixed modeling approach, posterior draws in Bayesian/MCMC approach.
These predictions are finally post-stratified by the population counts to the small area estimates of interest.

MRP thus combines ideas of multilevel unit models with the (re)weighting approach.

A possible simplification of the model is to forgo the multilevel modeling, and/or empirical Bayes prediction of random effects.

## Online resources

### Conferences

## Primary references

Book length treatments:

Rao, J. N. K. (2003) _Small Area Estimation_. Wiley. (Amazon)[https://www.amazon.com/Small-Area-Estimation-J-Rao/dp/0471413747]

Rao, J. N. K., and I. Molina (2015). _Small Area Estimation_: 2nd edition. Wiley. 
(Amazon)[https://www.amazon.com/Small-Estimation-Wiley-Survey-Methodology/dp/1118735781]

Longford, N. T. (2005). _Missing Data and Small-Area Estimation: Modern analytical equipment for the survey statistician_.
Springer. (Amazon)[https://www.amazon.com/Missing-Data-Small-Area-Estimation-Statistician/dp/1852337605]
 
Pratesi, M. (editor) (2016). _Analysis of Poverty Data by Small Area Estimation_. Wiley.
(Amazon)[https://www.amazon.com/Analysis-Poverty-Estimation-Survey-Methodology/dp/1118815017]
