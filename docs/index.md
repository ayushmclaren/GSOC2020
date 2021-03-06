---
title: "Google Summer of Code 2020, Ayush Agarwal" 
author: "QBLD - Quantile Regression for Binary Longitudinal Data"
knit: (function(input_file, encoding) {
  out_dir <- 'docs';
  rmarkdown::render(input_file,
 encoding=encoding,
 output_file=file.path(dirname(input_file), out_dir, 'index.html'))})
output:
  prettydoc::html_pretty:
    keep_md: True
    theme: hpstr
    highlight: github
---


## Project Details
***
### Project Title       : QBLD: Quantile Regression for Binary Longitudinal Data
### Project short title : QBLD
### Project url         : https://github.com/rstats-gsoc/gsoc2020/wiki/QBLD---Quantile-Regression-for-Binary-Longitudinal-Data

## About Me
***
I am a junior undergraduate in the Department of Mathematics and Statistics at IIT Kanpur and have experience in the field of Markov Chain Monte Carlo (MCMC) through both courses and projects. I am crediting post-graduate courses on MCMC and Bayesian Econometrics, where I am learning the theoretical as well as implementation details of the field.  
I am proficient in R and have gained considerable implementation experience in the language through projects and implementation assignment in courses. I have implemented a variety of mcmc and time series models in research projects on *Gaussian Mixture Models* and *Bayesian Logisitic Regression* under Prof. Dootika Vats and [*Time Series Analysis and Forecasting*](https://github.com/ayushmclaren/Time-Series-and-Forecasting) under Prof. Amit Mitra of IIT Kanpur. I hold the position of coordinator of Stamatics, the mathematics and statistics society of IIT Kanpur. Additionally, I am mentoring sophomores and freshers on Probabilistic Machine Learning and Bayesian MCMC models as part of a project under statistics and the computer science association of IIT Kanpur.  

**Relevant Experience**  

### Gaussian Mixture Models -
Mentor :- Prof. Dootika Vats

* Implemented clustering mechanism in R using the Expectation-Maximization Algorithm.
* Using the AIC Loss function and Cross-Validation techniques, outputting and plotting final clustering.

GitHub link - https://github.com/ayushmclaren/Gaussian-Mixture-Models

### Bayesian Logistic Regression -
Mentor :- Prof. Dootika Vats

* Implemented a Bayesian Logistic Regression model in R for a Bernoulli likelihood.
* Analysed the obtained fits using Trace, Time, and Auto-Correlation plots to further help in tuning.

GitHub link - https://github.com/ayushmclaren/Bayesian-Logisitic-Regression


### Time Series Analysis and Forecasting -
Mentor :- Prof. Amit Mitra

 * Implemented a SARIMA time series model in python for Monthly Rainfall Data of the last 114 years in India.
 * Using the PACF Interpolation techniques, missing values were internally interpolated to maintain the full data.
 * Using the Dickey-Fuller Test, data was stationarized at first to implement the SARIMA model.
 * Using the Box-Jenkins Algorithm, predictive forecasting for the next month was achieved.
 
 GitHub link - https://github.com/ayushmclaren/Time-Series-and-Forecasting

### Relevant Coursework :
**Markov Chain Monte Carlo**                        |  **Time Series Analysis**  
**Bayesian Econometrics**                           |  **Quantitative Methods**  
**Statistical Simulation and Data Analysis**        |  **Probability and Statistics**


## Contact Information :
***
**Email**          : ayush.agarwal50@gmail.com, \ ayuag@iitk.ac.in  
**GitHub handle**  : [ayushmclaren](http://github.com/ayushmclaren)  
**Postal Address** : A 302 Hall 5, IIT Kanpur, Uttar Pradesh, 208016  
**Telephone**      : +91 9815139259
**Skype Id**       : Ayush Agarwal


## Student Affiliation
***
**Institution ** : Indian Institute of Technology, Kanpur  
**Program** : Bachelor of Science, Mathematics and Statistics  
**Stage of Completion** : Currently in my $3^{rd}$ (penultimate) year  
**Contact to verify** : Prof. Mohammad Arshad Rahman (marshad@iitk.ac.in) / [Dean, Students Affairs, IIT Kanpur](https://www.iitk.ac.in/dosa/)  

## Mentors
***
**Evaluating mentor** : Prof. Dootika Vats(dootika@iitk.ac.in) - MCMC Expert

**Co-mentor** : Dr. Adam Maidman (abmaidman@gmail.com) - Quantile Regression Expert


## Background
Panel data have been attractive for understanding behavior and dynamics, the modeling complexities involved have moved attention away from the data’s unique capacities. Modeling features such as a binary outcome variable or a quantile analysis, which are relatively straightforward to implement with cross-sectional data, are challenging and computationally burdensome for panel data. However, these features are important as they allow for the modeling of probabilities and lead to a richer view of how the covariates influence the outcome variable. For limited dependent variables, the concern is modeling the latent utility differential in the quantile framework, since the response variable takes limited values and does not yield continuous quantiles. 

This project follows Rahman and Vossmeyer (2019) as its motivating literature(hereon referred to as master literature), and contributes to the three literatures by extending the various methodologies to a hierarchical Bayesian quantile regression model for binary longitudinal data (QBLD) and proposing a Markov chain Monte Carlo (MCMC) algorithm to estimate the model. The model handles both common (fixed) and individual-specific (random) parameters (commonly referred to as mixed effects in statistics). The algorithm implements a blocking procedure that is computationally efficient and the distributions involved allow for straightforward calculations of covariate effects.


**The Model**

The QBLD model can be conveniently expressed in the latent variable formulation (Albert & Chib, 1993) as follows:

$$ z_{it} = x_{it}^{'}\beta + s_{it}^{'}\alpha_{i} + \epsilon_{it}   \hspace{35 pt} \forall i = 1,...,n; \hspace{5 pt} t = 1,...,T_{i} $$
$$ 
y_{it} = 
     \begin{cases}
       \text{1}  &\quad {if \hspace{5 pt} z_{it}\gt 0} \\
       \text{0} &\quad\text{otherwise,} \\
     \end{cases}
$$

where the latent variable $z_{it}$ denotes the value of $z$ at the $t^{th}$ time period for the $i^{th}$ individual, $x_{it}^{'}$ is a $1 × k$ vector of explanatory variables, $\beta$ is $k × 1$ vector of common parameters, $s_{it}^{'}$ is a $1 × l$ vector of covariates that have individual-specific effects, $\alpha_{i}$ is an $l × 1$ vector of individual-specific parameters, and $\epsilon_{it}$ is the error term assumed to be independently and identically distributed (i.i.d.) as $AL(0, 1, p)$ with $Q_{\epsilon_{it}}(p| x_{it}, \alpha_{i}) = 0$.

While working directly with the AL density is an option, the resulting posterior will not yield the full set of tractable conditional distributions necessary for a Gibbs sampler. Thus, we utilize the normal-exponential mixture representation of the AL distribution, presented in Kozumi and Kobayashi (2011).

The appropriate priors are chosen and a blocked Gibbs sampler is implemented as described in Rahman and Vossmeyer (2019).


## Related Work

Quantile regression has been implemented in binary data models (Benoit & Poel, 2012; Kordas, 2006), ordered data models (Alhamzawi & Ali, 2018; Rahman, 2016), count data models (Machado & Silva, 2005), and censored data models (Harding & Lamarche, 2012; Portnoy, 2003). The latter of these papers discusses the issues associated with solely focusing on fixed effects estimators and highlights the usefulness of allowing for a flexible specification of individual heterogeneity associated with covariates, also of interest in this framework.

To the best of my knowledge, several quantile regression packages already exist namely, `quantreg`, `BayesQR`, `MCMCpack`, `bqror`, `rqPen`. However, these packages are either based on frequentist frameworks or incapable of handling mixed effects BLD. `BayesQR` can handle a BLD framework, albeit using a Metropolis-within-Gibbs sampler and can only account for random effects. The proposed package aims to complement the existing packages and widen the scope of quantile regression framework to heterogenous binary longitudinal data. Similarly `brq` package implements the idea of Bayesian adaptive Lasso quantile regression.

In a recent Bayesian paper, Luo, Lian, and Tian (2012) develop a hierarchical model to estimate the parameters of conditional quantile functions with random effects. The authors do so by adopting an asymmetric Laplace (AL) distribution for the residual errors and suitable prior distributions for the parameters. Sampler for AL distribution is implemented in the `ald` package.

However, directly using the AL distribution does not yield tractable conditional densities for all of the parameters and hence a combination of Metropolis-Hastings (MH) and Gibbs sampling is required for model estimation. The use of the MH algorithm may require tuning at each quantile. To overcome this limitation, I will implement a full Gibbs sampling algorithm that utilizes the normal-exponential mixture representation of the AL distribution. The other significant point of difference is that the model handles both common (fixed) and individual-specific (random) parameters.

## Expected Impact and Usage

The paper on, "Estimation and Applications of Quantile Regression for Binary Longitudinal Data" by Rahman, and Vossmeyer (2019) develops a framework for quantile regression in binary longitudinal data settings. A novel Markov chain Monte Carlo (MCMC) method is designed to fit the model and its computational efficiency is demonstrated. Panel data have been attractive to reserachers for understanding behavior and dynamics. The paper already has 6 citations in less than 6 months, demonstrating an interest in the field. An open source code in R is not available yet, however, a rudimentary implementation in MATLAB has been achieved. Availability of an open source tool will further help researchers take advantage of the theoretical development.

Researchers, and students in fields related to Quantile Regression, Econometrics, and Policy making that use R will be benefited by the new tools generated with this project. The set of tools to be created will facilitate deeper insights into panel data in a binary response variable environment, that otherwise will require extensive analyses in distinct software platforms. These tools will help in accounting for hetergoenity. Heterogeneity implies that response may differ in terms of certain unmeasured variables that affect the probability of the outcome. Users will find in this package an important set of tools that will help them to make informed decisions.

**Usage (Till date)**

The methodology has been applied to study female labor force participation and home ownership in the United States. The results offer new insights at the various quantiles, which are of interest to policymakers and researchers alike. The datasets for both the examples will be a part of the package and will help in demonstartion of the tools through a R vignette.

**CRAN release**

The `qbld` package will be submitted to the authors for a peer review. After its hopefully smooth acceptance, I will submit it to CRAN under GPL(>2). A developmental version of the package will be hosted on GitHub and tested for future releases. 


## Coding Plan and Methods
***
### Asymmetric Laplace distribution  

The current implementation of the random number generator function `rALD` in the `ald` package uses the three parameter Asymmetric Laplace Distribution defined in Koenker and Machado (1999). I will implement a more efficient method by utilizing the normal-exponential mixture representation of the AL distribution, presented in Kozumi and Kobayashi (2011). This method only requires the skewness paramter *p* as the input and will make use of `rnorm` and `rexp` functions.

$$ \epsilon_{it} = w_{it}* \theta + \tau * \sqrt{w_{it}}*u_{it} \hspace{20 pt} \forall i = 1,...,n; \hspace{5 pt} t = 1,...,T_{i} $$
where $u_{it} \sim N(0,1)$ is mutually independent of $w_{it} ∼ \epsilon(1)$ with $\epsilon$ representing an exponential distribution and the constants $\theta = \frac{1-2p}{p(1-p)}$ and $\tau = \sqrt{\frac{2}{p(1-p)}}$.
Supporting functions analogous to `dALD`, `qALD` for density and quantile calculations respectively will also be similarly implemented.


```r
rALD <- function(n,p) #random number generator
{
  # skewness parameter and number of samples as the input.
  # the output follows a AL(0,1,p) distribution. (normalized for interpretation)
}

qALD <- function(prob,p,tail) #quantile function
{
  #tail is logical variable to decide P(X<=prob) or P(X>prob) 
}

dALD <- function(y,p) #gives the density
{
  #evaluates density of AL(0,1,p) at y
}
```



### The Gibbs Sampler

Following the master literature, I will implement a blocked Gibbs sampler for the QBLD framework which can handle heterogenity in both common (fixed) and individual-specific(random) parameters. The Blocking procedure is essential for efficiency and reducing computational load. This blocked approach also significantly improves the mixing properties of the Markov chain. The success of these blocking techniques can be found in J.S. Liu (1994), Chib and Carlin (1999), and Chib and Jeliazkov (2006). The functions to sample from the conditional distributions will be set up generically for a wide scope usage outside the model.

To improve the speed of the routine, the Markov Chain Monte Carlo (MCMC) part of the algorithm will be programmed in Rcpp and be called from within the function in R.

I have also identified and plan to solve the following additional roadblocks - 

**Stacking of individual data** -

Since this is a panel data setting, Longitudinal data models often involve a moderately large amount of data, so it is important to take advantage of any opportunity to reduce the computational burden. One such trick is to stack the model for each individual *i* for all its time points and account for the covariates as one matrix rather than covariate vectors. (Hendricks, Koenker, & Poirier, 1979).

**Transposing and Inverting high-dimensional matrices** -

Since the sampler involves calculation and storage of transpose and inverse of large size matrices at repeated intermediate steps, I will offload these functions to Rcpp for faster implementation. Cpp is also known to be better at handling the machine tolerance issues than R.
Methods to avoid this issue also includes alternative algorithms for sampling from a Multivariate Normal and Using a Non-blocked sampler decribed later.

**Penalization and priors on $\beta$ ** -

The form of the prior distribution on $\beta$ holds a penalty interpretation on the quantile loss function. A normal prior on $\beta$ implies a $l_2$ penalty and has been used in Luo et al. (2012). One may also employ a Laplace prior distribution on laplace that imposes $l_1$ penalization, as used in Alhamzawi and Ali (2018). I will try to efficiently implement the sampler for latter case giving the user a choice in terms of the priors. In case it is not specified, the deafult will be the normal prior.

**Pre-processing of the data** -

The input data by the user will have to be cleaned, by reshaping, deleting or adding rows and columns, removing or intrapolating the missing data cells. I will implement a generic function that will clean the data and mould it into a QBLD format that can be used by the algorithm. The function can be implemented generically for a much larger use case. In case the data cannot be processed, the user will be given appropriate warnings to ensure that the data can be manually processed by the user and fed in the correct format to the sampler.


```r
# Returns an object of specified classes that represents a quantile regression fit
qbld.gibbs <- function(formula,tau,data,subset=data,method,summary=TRUE,blocking = TRUE, clean = TRUE) 
{
  #formula specifies y~x.
  #tau specifies the quantiles to be estimated
  #data is the data.frame to work upon, subset can be specified if the whole data is not to be used.
  #method is default at l2 with normal prior on beta, may be used to switvh to l1 and laplace
  #summary will specify the object type returned, when true user may be able to call the summary function afterwards
  #blocking may be specified, clean will pre-process the data (maybe implemented outside the function)
}
```



### Handling Categorical Variables

It is imperative that categorical variables be handled correctly, because if the algorithm does not employ any checks and treats the categorical variables as normal integers the sampler will inadvertently lead to wrong solutions. Since, this sampler works for the QBLD setting, categorical variables are highly common in these datasets. The design matrix for the model will be needed to be transformed and augmented properly depending on the number of factor variables. This should be done under the hood as the user must be able to specify the formula generically as in for instance, `lm(y~x)` can handle both continous and factor regressors without user interference. I plan to take this into account and employ a factor variable checker, one of which could be made using `as.factor` function so that the algorithm gets to the right design matrix. This function can be implemented generically for independent usage in multiple data settings including QBLD.


### Blocked vs Non-Blocked Sampling

Blocking technique is preferred over the Non-blocking counterpart because is provides with a better autocorelation structure and relatively faster mixing. However, the blocking procedure employs inverting large matrices which may be too computationally burdensome. I plan to also give the blocking vs non-blocking samplers as an additional choice for the user. 

However, Since the non-blocked version involves inverting only diagonal matrices which is computationally a lot easier, I plan to implement a method for the algorithm to decide when is it computationally feasible to switch to a non-blocked sampler despite giving slightly more autocorrelated samples without the user having to decide or wait longer for the results. One generic way to bypass this problem is to switch beyond a specified dimension of the covariate vector.

A second method involves the use of alternative algorithms to *sample from the mutivariate normal* which do not require such inverse calculations.
I plan to try and implement one of the following two algorithms, (with the effort to find more efficient methods)

* Fast sampling, Anirban Bhattacharya (2016) 
* Perturbation-Optimization, François Orieu (2013)

These algorithms are specific to a class of normals having desired structure, and avoid the inversion of matrices and can significantly improve efficiency of the sampler. Since, sampling from a multivariate normal is an essential central step in this Gibbs sampler, this will speed up the algorithm significantly. I will also try to implement the samplers genrically for usage outside the present setting.


```r
fast_rmvn <- function(n,phi,dmat,method) #fast sample from MVN
{
  #phi is a decomposition term as specified in the algorithm
  #dmat is a decomposition term as specified in the algorithm
  #method will employ different methods to solve system of linear equations, SOR,Gauss-Seidel are examples.
}
```

  
  
### Sampling from Univariate/Multivariate Truncated Normal

The Gibbs sampler requires to sample from a Truncated Multivariate Normal distribution multiple times across runs and thus it is essential to look at its implementation. In the master literature, algorithm samples $z_{i} \sim TMVN_{B_{i}}(X_{i}\beta + w_{i}\theta,\Omega_{i})$ using a series of conditional posteriors which are univariate truncated normal distributions, where the symbols hold their appropriate meaning. This algorithm was proposed in Geweke(1991).

Geweke's method is computationally heavy and suffers from slow mixing issues, therefore I will implement other, more efficient methods to sample from a Truncated Multivariate Normal. A few of the algorithms are mentioned :-

* Exact Hamiltonian Monte Carlo, Pakman (2013), this has been implemented in the `tmg` package
* Minimax Tilting, Botev (2016), this has been implemented in the `TruncatedNormal` package
* Fast Simulation of Hyperplane-Truncated, Cong (2017), no known implementation exists, I will try to implement this efficiently and for generic use.

**The Generalized Inverse Gamma sampler**

I will also try to improve efficiency of the GIG sampler, using the method described in Leydold (2013). An author implementation is already present in `GIGrvg` package.

### Covariate Effects and Model Comparison

Covariate effects are a key consideration in model evaluation, forecasting, and policy analysis, yet their dependence on estimation uncertainty has been largely overlooked in previous work. Jeliazkov and Vossmeyer (2018) explores the evidence that reveals that failing to consider estimation variability and relying solely on parameter point estimates may lead to nontrivial biases in covariate effects that can be exacerbated in certain settings, underscoring the pivotal role that estimation uncertainty can play in this context.

I will implement the method described in the said paper genrically for use outside the QBLD framework, this will be used in the final `summary` table output for the Gibbs output. The probabilities are computed from the AL cdf, allowing for straightforward interpretations of the covariate effects. Implemented in the `dALD` function I mentioned about earlier. 

In the past, marginal effects have often been computed at the average value of the covariates $\bar{x}$ and the parameter point estimate $\hat{\beta}$. $\bar{x}$ can be meaningless if the set of covariates involves categorical, indicator, or any other kind of discrete variables. The effect can be unrepresentative even
with continuous covariates if $\bar{x}$ falls in a low density region (e.g., if that distribution is multimodal), in which case policy recommendations based on $\bar{x}$ may not reflect the effects in the population. To avoid some of the aforementioned issues, covariate effects can be evaluated by the several methods mentioned in the paper.


```r
cov_effect - function(model) #calculates cov effect 
{
  #will take the model class object as input and print out the cov_effects 
  #can be extended to work generically for other models, also part of summary function
}
```


For model comparison, I will follow standard techniques for longitudinal data models. Specifically, in the `summary` table output, I will provide the conditional Akaike Information Criterion (AIC), and conditional Bayesian Information Criterion (BIC). The calculations for the conditional AIC and conditional BIC can be found in Greven and Kneib (2010) and Delattre, Lavielle, and Poursat (2014), respectively.

The same will be implemented as genric functions for broader use case.

### Inefficiency Factor 

Final `summary` table will also include calculations for inefficiency factor (IF) by implementing the Batch Means method employed in Greenberg (2012).
I will also try to implement and estimate the probit model for binary longitudinal data (PBLD) using the algorithm presented in Koop, Poirier, and Tobias (2007) and Greenberg (2012) and identical priors for relevant parameters. The results for the QBLD and PBLD models will help us check the conformity with the alreasdy existing models while also highlight the extra information we get with the lower and higher quantiles.


## Convergence and Standard Errors

I will also make the output object for Gibbs sampler compatible with `mcmcse` package. Using the `mcse.q` function Standard Error will be caluclated and presented to the user in summary format.

The `mcmcse` package will also further help in testing for convergence in the implemented sampler and will be essential especially while using Non-Blocking technique. The package will also provide confidence regions and Effective Sample Size for further analysis using the inbuilt functions.


### Benchmarking and Profiling  

I will use the package `profvis` for visualizing code profiling data from R. To run code with profiling, wrap the expression in `profvis()`. By default, this will result in the interactive profile visualizer opening in a web browser.  
Examplle implementation - 

```r
profvis({
  g <- ggplot(diamonds, aes(carat, price)) + geom_point(size = 1, alpha = 0.2)
  print(g)
})
```
**Profiling for cpp** -  
I will use the profiling tools in visual studio for cpp functions as `profviz` doesn't support profling of individual functions in Rcpp.  

**Profiling memory** -  
Applying functions to a list of Markov chains is memory intensive in R as separate memory is allocated to the output of functions on each call. I will perform profiling for the memory usage to solve this issue. A possible workaround can be to perform all operations on lists in cpp and to clear the working memory of the R session if working in R is unavoidable.  

I will create a *.Rmd* file while optimizing code to store all the approaches for performance optimization, which can be used as a reference for similar problems in the future. I will use the `microbenchmark` package (which provides an infrastructure to measure and compare the execution time of R expressions accurately) to compare the performance of different approaches.  

**Possible approaches to improving the performance of bottlenecks** -  

* If the bottleneck is a function in a package, it’s worth looking at other packages that do the same thing. Two good places to start are:  
1. [CRAN task views](https://cran.rstudio.com/web/views/). If there’s a CRAN task view related to the problem domain, it’s worth looking at the packages listed there.  
2. Reverse dependencies of Rcpp, as listed on its CRAN page. Since these packages use C++, it’s possible to find a solution to the bottleneck written in a higher performance language.  
3. For Google, trying *rseek* and for StackOverflow, restricting the search by including the R tag, [R], in the search.  

* Knowing the exact format of the input so that appropriate, more efficient functions can be used instead of general functions.  For example, `as.data.frame()` is quite slow because it coerces each element into a data frame and then `rbind()`s them together. If you have a named list with vectors of equal length, you can directly transform it into a data frame. In this case, if you’re able to make strong assumptions about your input, you can write a method that’s about 20x faster than the default.  

* Vectorizing the code wherever possible (as loops in a vectorized function are written in C instead of R). Loops in C are much faster because they have much less overhead.  

* On further discussion with the mentors, I will look to parallelize the code in R.  

I will perform benchmarking using the package `rbenchmark`. Given a specification of the benchmarking process (counts of replications, evaluation environment) and an arbitrary number of expressions, `benchmark` function in `rbenchmark` evaluates each of the expressions in the specified environment, replicating the evaluation as many times as specified.  

### Numerical Instability

The Markov Chain sampler used in the algorithm is consistent and eventually converge to the correct target. But since we are performing inverse operations on matrices, the expressions for the inverse might give mathematically inconsistent results. A classic example of this is when repeated checks of positive semi-definiteness of covariance matrices give rise to incositenties in the long run. The user needs to be alerted in such a case and consistency eventually needs to kicks in. Some of the approaches to tackle this issue are  
1. Bypassing calculation of inverse by methods described above.  
2. Adding an $\epsilon$ term to the values to account fro machine tolerance.  
The optimal method to tackle such inconsistencies can be decided after consultation with the mentors.  


### Documentation

I will use the package `roxygen2` to maintain and update the documentation. `roxygen2` generates *.md* files and creates `NAMESPACE` with R and Rcpp. The package requires adding roxygen comments to the source code. I will add the necessary roxygen comments to all the functions while in progress to maintain and bring uniformity in all documentation.

I will also add two data sets as part of the package, and publish a vignette which will extensively detail the scope and proper use of the package functions by using the model on the said data sets.


### Visualizations

Visualizations of both table(text) forms and plot forms are also included in the project description and will be a worthy addition for the package, in my opinion. 

`summary.QR` will be a package function that summarizes the output of the `bayesQR` function in an object of class bayesQR.summary. For every estimated beta and sigma, this object will contain the Bayes estimate and the posterior credible interval. The object will also contains other relevant
information about the estimation procedure, such as the quantile, the variable names, etc.

`plot.QR` will be a package function that produces quantile plots, traceplots or posterior histograms based on the estimates obtained by the `bayesQR` function. For quantile plots, note that the more quantiles are estimated with bayesQR, the more detailed the quantile plot will be.

I plan to make the visualizations in the package compatible with `ggplot` to allow for elegant and sophisticated *acf* and time series plots for the Markov chains. I also plan on making the function output objects compatible with base package tools such as `plot` and `summary` to reduce package dependencies and provide a more useful user experience.


## Timeline 
***



<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> PERIOD </th>
   <th style="text-align:left;"> TASK </th>
   <th style="text-align:right;"> MEETINGS </th>
  </tr>
 </thead>
<tbody>
  <tr grouplength="1"><td colspan="3" style="background-color: #666; color: #fff;"><strong>Community Bonding</strong></td></tr>
<tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> May 4 - June 1 (Pre GSoC period) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Research more on quantile regression related literature and development of second penalised framework. Get familiar with writing R packages with the C++ code and using other tools mentioned. Discussion of some of the roadblocks and plans mentioned in the proposal with mentors. </td>
   <td style="text-align:right;"> 1 </td>
  </tr>
  <tr grouplength="5"><td colspan="3" style="background-color: #666; color: #fff;"><strong>Phase I: Implementing the sampler</strong></td></tr>
<tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> June 1 - June 8 (Week 1) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementation of Asymmetric Laplace related functions and GIG functions </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> June 8 - June 15 (Week 2) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing the blocked Gibbs sampler code in R followed by cpp implementation. Writing testthat for the implementation, checking for numerical instability and profiling. </td>
   <td style="text-align:right;"> 3 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> June 15 - June 22 (Week 3) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing the Non-blocked Gibbs Sampler code in R followed by cpp implementation. Writing testthat for the implementation, checking for numerical instability and profiling. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> June 22 - June 29  (Week 4) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Handling issues related to categorical variables, checking for numerical instability and test runs of the sampler with new data setting </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> June 29 - July 3 (Phase 1 eval) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Phase one eval prep and cleanup - tying any loose ends up to this point  (bug fixes, documentation, incomplete implementation) to submit work for evaluation. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr grouplength="5"><td colspan="3" style="background-color: #666; color: #fff;"><strong>Phase II: Efficiency Improvements</strong></td></tr>
<tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> July 3 - July 10 (Week 5) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing the blocking vs non-blocking algorithm and testing for efficiency vs accuracy tradeoffs </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> July 10 - July 17 (Week 6) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing Sampling from Univariate/Multivariate Truncated Normal algorithms, Writing testthat for the implementation, checking for numerical instability and profiling. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> July 17 - July 24 (Week 7) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing the alternative penalization model, test runs and improvements, Implementation of PBLD model functions for comparison </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> July 24 - July 27 (Week 8) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Writing testthat, checking for numerical instability and profiling and writing roxygen comments for documentation for the previous weeks. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> July 27 - July 31 (Phase 2 eval) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Phase two eval prep and cleanup - tying any loose ends up to this point  (bug fixes, documentation, incomplete implementation) to submit work for evaluation. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr grouplength="5"><td colspan="3" style="background-color: #666; color: #fff;"><strong>Phase III: User experience and Integration</strong></td></tr>
<tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> July 31 - August 7 (Week 9) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing the Covariate Effects and Model Comparison. Writing testthat for the implementation, checking for numerical instability and profiling. </td>
   <td style="text-align:right;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> Ausgust 7 - August 14 (Week 10) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Implementing the functions for pre-processing the data, and mcmcse support is added, checking for numerical instability and profiling. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> August 14 - August 21 (Week 11) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Making visualizations in the package compatible with ggplot, base plot and summary functions and write in-package summarizing functions. </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> August 21 - August 24 (Week 12) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Writing roxygen comments for the existing untouched functions in the package. Checking for numerical instability in the remaining functions. </td>
   <td style="text-align:right;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;border-right:1px solid; padding-left: 2em;" indentlevel="1"> August 24 - August 31 (Final eval) </td>
   <td style="text-align:left;width: 30em; border-right:1px solid;"> Final eval prep and cleanup - tying any loose ends up to this point  (bug fixes, documentation, incomplete implementation) to submit work for evaluation. </td>
   <td style="text-align:right;"> 3 </td>
  </tr>
</tbody>
</table>

## Management of Coding Project
***
As proposed in my coding plan, I will use `testthat` for user and code testing. Using `testthat` will also ensure code submission. I have specifically allocated time slots in my timeline for testing.  
I will make multiple minor commits adhering to each new functionality that I add. The minor commits will be followed by a major commit every week, which concludes the successful completion of the task allocated to that week. The minor commits will be helpful for the mentors to track my progress over a week and will dictate the schedule of meetings. My major commits will track my workflow over the entire GSoC period. Missing out on major commits for two continuous week would indicate a problem.  

## References

* Rahman, Mohammad & Vossmeyer, Angela. (2019). Estimation and Applications of Quantile Regression for Binary Longitudinal Data. Advances in Econometrics. 40. 
* Albert, J., & Chib, S. (1993). Bayesian analysis of binary and polychotomous response data. Journal of the American Statistical Association, 88(422), 669-679.
* Benoit, D. F., & Poel, D. V. D. (2012). Binary quantile regression: A Bayesian approach based on the asymmetric Laplace distribution. Journal of Applied Econometrics, 27(7), 1174-1188.

* Kordas, G. (2006). Smoothed binary regression quantiles. Journal of Applied Econometrics, 21(3), 387-407.

* Alhamzawi, R., & Ali, H. T. M. (2018). Bayesian quantile regression for ordinal longitudinal data. Journal of Applied Statistics, 45(5), 815-828.

* Rahman, M. A. (2016). Bayesian quantile regression for ordinal models. Bayesian Analysis, 11(1),
1-24.

* Machado, J., & Silva, J. S. (2005). Quantiles for counts. Journal of the American Statistical
Association, 100(472), 1226-1237.

* Luo, Y., Lian, H., & Tian, M. (2012). Bayesian quantile regression for longitudinal data models.
Journal of Statistical Computation and Simulation, 82(11), 1635-1649.

* Koenker, R., & Machado, J. A. F. (1999). Goodness of fit and related inference processes for quantile regression. Journal of the American Statistical Association, 94(448), 1296-1310.

* Liu, J. S. (1994). The collapsed Gibbs sampler in Bayesian computations with applications to a gene regulation problem. Journal of the American Statistical Association, 89(427), 958-966.

* Chib, S., & Carlin, B. P. (1999). On MCMC sampling in hierarchical longitudinal models. Statistics
and Computing, 9(1), 17-26.

* Chib, S., & Jeliazkov, I. (2006). Inference in semiparametric dynamic models for binary longitudinal
data. Journal of the American Statistical Association, 101(474), 685-700.

* Bhattacharya A, Chakraborty A, Mallick BK. Fast sampling with Gaussian scale-mixture priors in high-dimensional regression. Biometrika. 2016;103(4):985–991.

* François Orieux, Olivier Féron, Jean-François Giovannelli. Sampling high-dimensional Gaussian distributions for general linear inverse problems. IEEE Signal Processing Letters, Institute of Electrical
and Electronics Engineers, 2012, 19 (5), pp.251.

* Pakman, Ari & Paninski, Liam. (2012). Exact Hamiltonian Monte Carlo for Truncated Multivariate Gaussians. Journal of Computational and Graphical Statistics.

* Botev, Z.I. (2017). The normal law under linear restrictions: simulation and estimation via minimax tilting.

* Cong, Yulai; Chen, Bo; Zhou, Mingyuan. Fast Simulation of Hyperplane-Truncated Multivariate Normal Distributions. Bayesian Anal. 12 (2017), no. 4, 1017--1037.

* Wolfgang Hörmann and Josef Leydold (2013). Generating generalized inverse Gaussian random
variates, Statistics and Computing.

* Jeliazkov, I., & Vossmeyer, A. (2018). The impact of estimation uncertainty on covariate effects in
nonlinear models. Statistical Papers, 59(3), 1031-1042.

* Greven, S., & Kneib, T. (2010). On the behaviour of marginal and conditional AIC in linear mixed models. Biometrika, 97(4), 773-789.

* Delattre, M., Lavielle, M., & Poursat, M.-A. (2014). A note on BIC in mixed-effects models.
Electronic Journal of Statistics, 8(1), 456-475.

* Greenberg, E. (2012). Introduction to Bayesian econometrics. New York, NY: Cambridge University Press.

* Koop, G., Poirier, D., & Tobias, J. (2007). Bayesian econometric methods. New York, NY: Cambridge University Press



