# Pulsar Timing notes

## GOALS
* array telescopes
* how pulsar-timing data is recorded

* Signal and noise in pulsar timing observations
* Pulsar Timing
* Millisecond pulsars
    * most stable rotations
    * highest precision timings
* Other pulsars
  * BH pulsar
* Time of arrival (TOA)
___
## Introduction (Ryan)

### Traditional time taking measurements
* avg time + freq to produce a single profile of minutes-hours of observations


### Common assumptions
* radio emission "anchored" to NS -- measures rotational state of pulsars
* radio emission is stable: emission will converge to same profile at each epoch


### Contributions to pulsar arrival times
* light travels 30cm in minutes
* arrival time can be affected by
  * spin-down rate of pulsars
  * the orbit around of the pulsar around something else
  * stochastic background of gravitational waves can affect the pulsar signal's arrival time

### Power spectral estimation
* FFT time data, get powers of different frequencies

### Deterministic VS stochastic process
* White noise
  * noise that is uncorrelated in the TOA
  * has flat power spectrum
  * we see a "jitter" in the data
  * JOY DIVISION album cover
  * radiometer noise + pulse jitter + instrumental effects
* Red noise
  * correlated, random walks
  * Brownian noise
  * The graphic representation of the sound signal mimics a Brownian pattern
  * Its spectral density is inversely proportional to f^2, meaning it has more energy at lower frequencies (can be modeled by P(f)=A f^b)
  * Red noise has time variability similar to that expected from gravitational waves (maps onto gravitational wave background)
  * GW noise + spin noise + ISM Noise
* Band noise
* Systematic Noise (lab frame noise)


### Physical models for timing effects
* spin rate
* magnetosphere
* gravitational lensing
* more...

### Interpreting results of a timing model
* Visual inspection -- do residuals look strange
* how good does the model fit the data
* are parameters significant and values make sense
* do parameters improve the fit/increase the evidence

### The implementation
#### Use `tempo2` graphical plugin to inspect residuals
* "Bailes method" -> remove low SNR TOAs and see thats left "delete the crap"
  * Paul Lasky: presumably if you had a robust enough model, then the model should take the low SNR and deal with it...
  * Bailes: uncertainty increases way too much -- might be Systematic error and this might make us loose
  * If the Low SNR are due to systematic errors, can a model be built to model them

### Be careful of
* Power spectrum leakage

___

## Bayesian inference (Paul)

### Breast cancer example

* 1% woman at age 40 have breast cancer
* 80% of women with breast cancer have positive mammogram
* 9.6% of women without breast cancer also have mammogram (false positive!)
* a women in this age group had a positive mammogram in a routine screening. What is the prb that she has breast cancer?
![alt text](https://drive.google.com/open?id=1UiEIqREN5d8ENbC4TheBy2SJicnB2GD5 “Bayesian Inference”)



* p(A|B) = p(B|A) * p(A) / P(B)

### Bayesian Stats + Pulsar Astronomy
![alt text](https://drive.google.com/open?id=1vmmky1hXixshSwLyLz6g-OylR-0HWB8V “Pulsar Data”)


* Components of Posterior probability in terms of astrophysics
* Likelihood: prob of data given the model
* Prior: apriori info of the parameters of the model
* Evidence: only depends on data, for parameter estimation is just a normalisation constant
* Samplers:
	* too many parameters to calculate the likelihood at different points
	* need to sample the parameter space and move towards the parameters with higher likelihoods

### Bayesian stats to extract glitch
* Make model for glitch
* Use this model in our posterior probability equation
* calculate the evidence using the glitch model, then the evidence of the signal
* compare the models with the odds ratio or bayes factor
* todays posteriors are tomorrow's priors

Question for Paul: the overshoot and decay is potentially explained by the fluid in the container model, but could that be explained by a superfluid core? Wouldn’t you need some friction from the fluid to spin up the pulsar? Would vortex unpinning explain that?
A: He said ya

___


## Inference in Pulsar timing (Boris)

#### The LnL function for Pulsar
* multimodal gaussian  
* Covariance matrix: Intuitively, the covariance matrix generalizes the notion of variance to multiple dimensions. As an example, the variation in a collection of random points in two-dimensional space cannot be characterized fully by a single number, nor would the variances in the x and y directions contain all of the necessary information; a 2x2 matrix would be necessary to fully characterize the two-dimensional variation. (wikipedia)

Question for Boris: why do DM variations produce red noise? Wouldn’t we expect it to be uncorrelated between measurements?

Q: Solar System Ephemeris is best measured from PTAs, so how do you then remove the Ephemeris noise from PTAs without risking removing data?

___

## Pulsar Inference Tools (Marcus Lower + Aditya Parthasarathy)

* Temo + Temp2
	* pulsar timing tool




Q for Marcus: Does TempoNest (the Bayesian PT add-on) incorporate the method Paul was talking about of running Bayesian analysis on each pulse?
