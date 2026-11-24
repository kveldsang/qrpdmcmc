# qrpdmcmc

**Multi-Chain Adaptive MCMC Estimation and Diagnostics for Quantile Regression for Panel Data with Non-Additive Fixed Effects**

`qrpdmcmc` is a user-written Stata package providing an integrated framework for multi-chain adaptive Markov Chain Monte Carlo (MCMC) estimation and convergence diagnostics for quantile regression with non-additive fixed effects.

The package extends the MCMC estimation procedure implemented in `qregpd` (Powell, 2022), allowing users to run multiple chains with independent seeds, combine retained draws, and assess convergence and sampling efficiency using graphical and numerical diagnostics.

The package is publicly available through the Statistical Software Components (SSC) archive.

## Installation

Install the package directly from SSC:

```stata
ssc install qrpdmcmc
```

The command requires the `moremata` and `amcmc` packages.

For complete documentation and available options, run:

```stata
help qrpdmcmc
```

## Features

- Multi-chain adaptive MCMC estimation with independent random seeds
- Summary statistics for retained parameter draws
- Density, trace, and running-average plots
- Autocorrelation functions (ACF)
- Effective Sample Size (ESS) and Monte Carlo Standard Error (MCSE)
- Gelman–Rubin convergence diagnostics (R-hat)
- Geweke convergence diagnostics
- Parameter cross-correlation matrices
- Postestimation diagnostics without rerunning the estimator
- Saving and reloading MCMC draws for reproducible analysis

## Example

The following example uses Stata's `nlswork` dataset.

```stata
webuse nlswork, clear

* Estimate two MCMC chains and compute diagnostics
qrpdmcmc ln_wage tenure union, ///
    id(idcode) fix(year) ///
    chains(2) seeds(10101 20202) ///
    stats trace ess gr var(tenure union) ///
    saving(mydraws) replace

* Run additional diagnostics without re-estimation
qrpdmcmc, geweke var(tenure union)

* Load previously saved draws
qrpdmcmc, using(mydraws) stats var(tenure)
```

## Authors

**Kamilla Kosheeva** and **Michail Liatos**  
Friedrich-Alexander-Universität Erlangen-Nürnberg (FAU)

## Citation

Kosheeva, K., and M. Liatos (2026). *QRPDMCMC: Stata module to provide Multi-Chain Adaptive Markov Chain Monte Carlo (MCMC) Estimation and Diagnostics for Quantile Regression for Panel Data with Non-Additive Fixed Effects.* Statistical Software Components, Boston College Department of Economics.

[SSC / RePEc publication](https://ideas.repec.org/c/boc/bocode/s459909.html)

## License

Distributed under the MIT License, as indicated in the SSC publication.
