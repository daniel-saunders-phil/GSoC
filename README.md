# The Goals

August 23, 2023

The GSoC project aimed to expand support for spatial statistics in PyMC. PyMC is a leading Python package for Bayesian statistics. When I started the project, PyMC had support for some types of popular spatial models, especially with Gaussian processes and the conditional autoregressive (CAR) distribution. But other modern Bayesian packages, such as Stan or r-INLA were more comprehensive in this area. The goal of this project was to add support for the intrinsic conditional autoregressive (ICAR) distribution and the Besag-York-Mollie (BYM) model. 

# The Contributions

I made four major contributions to this end:

- A tutorial-style notebook that explains how to build and interpret a BYM model. It explores a dataset of New York City traffic accidents from roughly 2000 census tracks. The notebook is finished and can be viewed [here](https://www.pymc.io/projects/examples/en/latest/case_studies/nyc_bym.html).

- Added the ICAR distribution. The ICAR distribution is a key building block for the larger goal of constructing the BYM model. I compared several possible implementations for efficiency, accuracy, and usability to settle on the current approach. I also wrote a suite of unit tests. The ICAR distribution was merged from this pull request: https://github.com/pymc-devs/pymc/pull/6831 and work on this part of the project is finished.

- Discovered and fixed a bug in the CAR distribution. Previously, the CAR distribution would accept parameters outside its domain, leading to unstable behavior. I fixed the bug in this merged PR: https://github.com/pymc-devs/pymc/pull/6801.

- Finished tutorial-style notebook on CAR. A previous GSoC project wrote a tutorial on using the CAR distribution for spatial statitics. However, it was never merged. I tidied up some style and formatting issues and had the notebook merged in https://github.com/pymc-devs/pymc-examples/pull/547.

# Future work

There is one area of future work. The BYM model we have in that notebook only works for fully connected spatial areas. Occassionally, people are interested in performing spatial inference on problems where some areas are completely disconnected from other areas. This requires a slightly different scaling factor computation. A discussion of how that problem was fixed in R can be found here https://github.com/ConnorDonegan/Stan-IAR/issues/3 and interested users can use that as template for modifying the existing BYM workflow.
