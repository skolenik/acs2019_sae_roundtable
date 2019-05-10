# Small Area Estimation

**Materials for the small area estimation roundtable at ACS 2019 Data Users Group meeting**

<img src=ACS_2019_SAE_roundtable.png height=200>

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

_Small area_: a subpopulation, a domain, a subset of the overall population of a survey that may 
have insufficient data / number of observations to support (accurate) statistical inference.

_Direct estimate_: an estimate for a small area based only on the survey data in that small area, 
e.g. weighted mean

_Synthetic estimate_: an estimate for a small area that is based solely on a statistical model,
typically a regression or a generealized linear model.

_Composite estimate_: an estimate that combines both a direct estimate and a synthetic estimate.

## Examples

- Census Bureau: Small Area Income and Poverty Estimates
  * States, Counties, School districts
  * http://www.census.gov/did/www/saipe/
- National Cancer Institute: Small Area Estimates for Cancer Risk Factors and Screening Behaviors
  * States, Counties
  * Combines BRFSS and NHIS [Raghunathan et al. 2007](https://www.jstor.org/stable/27639878)
  * http://sae.cancer.gov/
- National Center for Health Statistics: NHIS phone use data
  * https://www.cdc.gov/nchs/data/nhis/earlyrelease/Wireless_state_201712.pdf

## Methodologies

### Ratio estimation

Groupwise ratio estimator applies means or proportions of the outcome in a population group 
to the population of the small area of interest.

1. Split large sample into groups (e.g., age-gender-education), _g_ = 1; ... ;_G_
2. Estimate the nationwide mean outcome in each group y<sub>g</sub> = weighted mean in this group.
3. Apply the small area proportions of all groups as weights to obtain the SAE estimate

This produces a synthetic estimate, i.e., the one that is based only on the aggregate data.
The implicit statistical model is that the outcome is constant within cells defined by the groups.

### Weighting/calibration

In this method, the estimates are obtained by (re-)weighting the sample data to the socio-demographic
characteristics of the area of interest. Estimates can be expected to be biased unless the weighting variables
fully account for both sample selection and outcome variation. With a single weighting variable, the method
becomes the group-wise ratio estimator described above.

A strengthed version of the method is due to 
([Lehtonen and Veijanen (2019)](http://isi-iass.org/home/wp-content/uploads/Survey_Statistician_January_2019.pdf)).
In their approach, they fit a model (based on the survey data) to the outcome using predictors available 
for the whole population (assuming availability of the population register), obtain predictions,
calibrate the sample to predictions (i.e. reweight the sample so that the weighted sample total of predictions
is equal to the population total of predictions), and obtain calibrated estimates based on the sample
with the actual outcomes.

_Data requirements_: 
- Survey data:
  + Outcome of interest _y_ 
  + Identifiers of the small areas
  + Weighting variables _x_
- Population data:  
  + Identifiers of the small areas
  + Population counts in categories of _x_

### Area models

Area SAE models fit regression models to the area-level direct estimates, thus smoothing them.

_Data requirements_: 
- Survey data:
  + Outcome of interest _y_ 
  + Identifiers of the small areas
- Population data:  
  + Area-level predictors
  + Identifiers of the small areas


### Unit models

Unit SAE models fit regression or generalized linear models to the outcomes observed at the person level:

_Data requirements_: 
- Survey data:
  + Outcome of interest _y_ 
  + Predictors _x_ (e.g., demographic variables)
  + Identifiers of the small areas
- Population data:  
  + The same predictor variables _x_ for the small area as those used in the SAE model in the large data set
    **for everybody in the population**
  + Identifiers of the small areas

Both unit-level (i.e., person level) and area-level (e.g., county level) predictors are typically used.

In some approaches (e.g., [Pierannunzi et. al. 2016](https://www.cdc.gov/pcd/issues/2016/15_0480.htm)),
instead of using the full population data, a high quality large sample size survey is used: in their example,
the model is fitted to BRFSS data while the predictions are obtained on the ACS data. Standard error computations
should account for the sampling error in the second survey, as well.

### Multilevel regression with post-stratification

This method (MRP) originated in political science 
([Park, Gelman and Bafumi 2004](http://www.stat.columbia.edu/~gelman/research/published/parkgelmanbafumi.pdf)),
and has also become popular in health sciences. In this method, a multilevel/mixed model 
of the following structure is fit to **unweighted** survey data:

- random effects are specified at the area level;
- the unit-level (demographic) predictors are only those for which fully interacted population counts
(census tables) are available;
- area level predictors can, but do not have to, be used

Once that model is fit, predictions are obtained that include integration over random effects:
empirical Bayes for frequentist/REML/ML mixed modeling approach, posterior draws in Bayesian/MCMC approach.
These predictions are finally post-stratified by the population counts to the small area estimates of interest.

MRP thus combines ideas of multilevel unit models with the (re)weighting/groupwise estimation approach.

A possible simplification of the model is to forgo the multilevel modeling, and/or empirical Bayes prediction of random effects.

## Online resources

1.	This is a good technical intro once you get the basics and can handle some minimal math:
https://researchoutput.csu.edu.au/ws/portalfiles/portal/25229570/A_Review_of_Small_Area_Estimation.pdf
2.	National Academy of Sciences workshop on the future of federal surveys: 
https://www.nap.edu/read/13174/chapter/7#62. 
You can read this online, or you can register on their website and download the pdf file.
3.	JNK Rao keynote address at the 2013 Eurostat conference: 
https://ec.europa.eu/eurostat/cros/system/files/9A01_Keynote_Rao-v2_0.pdf 
4.	A conceptual discussion with applications to health: 
https://ncvhs.hhs.gov/wp-content/uploads/2014/05/130501p02.pdf

### Conferences

## Primary references

Book length treatments:

Rao, J. N. K. (2003) _Small Area Estimation_. Wiley. [Amazon](https://www.amazon.com/Small-Area-Estimation-J-Rao/dp/0471413747)

Rao, J. N. K., and I. Molina (2015). _Small Area Estimation_: 2nd edition. Wiley. 
[Amazon](https://www.amazon.com/Small-Estimation-Wiley-Survey-Methodology/dp/1118735781)

Longford, N. T. (2005). _Missing Data and Small-Area Estimation: Modern analytical equipment for the survey statistician_.
Springer. [Amazon](https://www.amazon.com/Missing-Data-Small-Area-Estimation-Statistician/dp/1852337605)
 
Pratesi, M. (editor) (2016). _Analysis of Poverty Data by Small Area Estimation_. Wiley.
[Amazon](https://www.amazon.com/Analysis-Poverty-Estimation-Survey-Methodology/dp/1118815017)

Review papers:

Ghosh, M., and J. N. K. Rao (1994). Small Area Estimation: An Appraisal. 
[_Statistical Science_, 9 (1), 55--76](https://projecteuclid.org/euclid.ss/1177010647), doi:10.1214/ss/1177010647.

Pfeffermann, D. (2007). Small Area Estimation --- New Developments and Directions. 
[_International Statistical Review_, 70 (1), 125--143](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1751-5823.2002.tb00352.x),
doi:10.1111/j.1751-5823.2002.tb00352.x.

Lehtonen, R., and A. Veijanen (2009). Design-based Methods of Estimation for Domains and Small Areas.
[Chapter 31 in _Handbook of Statistics 29B_, 219--249](https://www.sciencedirect.com/science/article/pii/S0169716109002314).
Elsevier/North Holland, doi:10.1016/S0169-7161(09)00231-4.

Datta, G. S. (2009). Model-Based Approach to Small Area Estimation.
[Chapter 32 in _Handbook of Statistics 29B_, 251--288](https://www.sciencedirect.com/science/article/pii/S0169716109002314).
Elsevier/North Holland, doi:10.1016/S0169-7161(09)00232-6.

Pfeffermann, D. (2013). New Important Developments in Small Area Estimation. 
[_Statistical Science_, 28 (1), 40--68](https://projecteuclid.org/euclid.ss/1359468408), doi:10.1214/12-STS395.

Best known framework papers:

Fay, R. E., and R. A. Herriot (1977). 
Estimates of Income for Small Places: An Application of James-Stein Procedures to Census Data.
[_Journal of the American Statistical Association_, 74 (366), 269--277](https://amstat.tandfonline.com/doi/abs/10.1080/01621459.1979.10482505),
doi:10.1080/01621459.1979.10482505.

Battese, G. E., R. M. Harter and W. A. Fuller (1988). 
An Error-Components Model for Prediction of County Crop Areas Using Survey and Satellite Data.
[_Journal of the American Statistical Association_, 83 (401), 28--36](https://amstat.tandfonline.com/doi/abs/10.1080/01621459.1988.10478561),
doi:10.1080/01621459.1988.10478561.

Ghosh, M., K. Natarajan , T. W. F. Stroud and B. P. Carlin (1998).
Generalized Linear Models for Small-Area Estimation.
[_Journal of the American Statistical Association_, 93 (441), 273--282](https://amstat.tandfonline.com/doi/abs/10.1080/01621459.1998.10474108),
doi:10.1080/01621459.1998.10474108.

Datta, G. S., and P. Lahiri. (2000) A Unified Measure of Uncertainty of Estimated
Best Linear Unbiased Predictors in Small Area Estimation Problems.
[_Statistica Sinica_, 10, 613--627](http://www3.stat.sinica.edu.tw/statistica/oldpdf/A10n214.pdf).

Jiang, J., and Lahiri, P. (2001). Empirical Best Prediction for Small Area Inference with Binary Data.
[_Annals of the Institute of Statistical Mathematics_, 53 (2), 217--243](https://link.springer.com/article/10.1023/A:1012410420337),
doi:10.1023/A:1012410420337.

Lahiri, P. (2003). On the Impact of Bootstrap in Survey Sampling and Small-Area Estimation.
[_Statistical Science_, 18 (2), 199--210](https://projecteuclid.org/euclid.ss/1063994975), doi:10.1214/ss/1063994975.

Jiang, J., and Lahiri, P. (2006). Mixed model prediction and small area estimation.
[_Test_, 15 (1)](https://link.springer.com/article/10.1007/BF02595419), doi:10.1007/BF02595419.

Molina, I., and J. N. K. Rao (2010). Small area estimation of poverty indicators.
[The Canadian Journal of Statistics, 38 (3), 369--385](https://onlinelibrary.wiley.com/doi/abs/10.1002/cjs.10051),
doi:10.1002/cjs.10051.

