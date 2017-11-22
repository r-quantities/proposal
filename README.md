---
output:
  pdf_document: default
---
# Quantities for R

**[Iñaki Ucar](https://github.com/Enchufa2), Arturo Azcorra**. Dept. of Telematic Engineering, Universidad Carlos III de Madrid, Spain.

Supporting authors:

- **[Edzer Pebesma](https://github.com/edzer)**. Institute for Geoinformatics, University of Muenster, Germany.

## Summary

A quantity is a "property of a phenomenon, body, or substance, where the property has a magnitude that can be expressed as a number and a reference" [1,2]. Science and engineering have to deal with all kinds of quantities: length, mass, time, energy, electric charge... Such quantities can be either a result of a measurement (direct measurement) or a combination of measurements (indirect measurement), and are composed of (1) a value (a number representing the measurand), (2) a measurement unit (or magnitude), and (3) a measurement error (or uncertainty).

Originally, computational systems have treated these three components separately. Data consisted of bare numbers, and data transformations and mathematical operations applied to them solely. Units were just metadata, and error propagation was an unpleasant task requiring additional effort and complex operations. Nowadays, many software libraries implement *quantity calculus* as a method of working with numbers and units in an integrated way, so that operations preserve dimensional correctness. Similarly, some software assist the task of the propagation of uncertainty. Unfortunately, quantity calculus and error propagation are seldom integrated in a complete solution [3].

## The Problem

Several R packages provide unit conversions, such as [`measurements`](https://cran.r-project.org/package=measurements) or [`NISTunits`](https://cran.r-project.org/package=NISTunits). Beyond this basic use case, the [`units`](https://cran.r-project.org/package=units) package [4], by Edzer Pebesma *et al.*, systematises the management of quantity values. It assigns units to numeric vectors as attributes of S3 objects, and implements S3 methods and operations for unit propagation, automatic conversion, derivation, simplification of units, error checking and printing. Using the `units` package may eliminate a whole class of potential scientific programming mistakes. The `units` package has become the reference for quantity calculus in R, with a wide and welcoming response from the R community in the form of pull requests and issues on GitHub.

On the other hand, packages such as [`propagate`](https://cran.r-project.org/package=propagate), [`car`](https://cran.r-project.org/package=car), [`msm`](https://cran.r-project.org/package=msm), [`spup`](https://cran.r-project.org/package=spup), [`distr`](https://cran.r-project.org/package=distr) or [`metRology`](https://cran.r-project.org/package=metRology) are entirely or partially devoted to assist the propagation of uncertainty using the Monte Carlo method (MCM), the Taylor series method (TSM) or both. Along the same lines as `units`, the recent [`errors`](https://cran.r-project.org/package=errors) package, by Iñaki Ucar, takes this approach one step further by integrating and automatising error propagation (using the TSM) and printing for R vectors.

A significant fraction of R users, both practitioners and researchers, use R to analyse measurements, and will benefit from a joint processing of quantity values with errors. Unfortunately, using `units` in R currently excludes `errors` and vice versa. Therefore, we propose the creation of a new package, `quantities`, which will not only orchestrate `units` and `errors` in a new data type, but will also extend the existing frameworks (compatibility with base R as well as other frameworks such as the *tidyverse*) and standardise how to import/export data with units and errors. 

Both the `units` and `errors` packages, as well as the [`constants`](https://cran.r-project.org/package=constants) package, have been already joined into the [*r-quantities*](https://github.com/r-quantities) organisation on GitHub, which aims at building the new `quantities` framework. Moreover, to the best of the authors' knowledge, there exists no such an integrated and automated framework outside the R language.

## The Plan

The development of the *r-quantities* framework for R requires the following action points:

- Design and implementation of a new R package called `quantities` for the joint orchestration of units and errors in numeric vectors.
- Implement the necessary changes in the existing codebase to resolve compatibility issues.
- Implement methods to import/export data with units and/or errors.
- Implement methods to better integrate them with *tidyverse*, and when possible *data.table*.
- Implement wrapper functions to map units/errors to the output of functions of interest, such as regression coefficients from linear models.
- Develop outlooks on the ability to extend the framework (e.g., new units, new error propagation methods).

These action points will be addressed based on the following timeline, with a total planned duration of 12 months:

- Month 1-2: work out the design, identify compatibility issues in the existing codebase.
- Month 3-6: program the R package, develop test cases.
- Month 7-8: program import/export methods and wrapper functions, develop test cases.
- Month 9-12: write tutorials, develop teaching material and reproducible examples.
- Month 9-12: develop outlooks on the ability to extend the framework.
- Month 9-12: develop outlooks on the ability and limitations of these data types.

Finally, we foresee the following failure modes and recovery plans:

- In case S3 objects are too simple for a wider compatibility with base R and tidyverse packages, we will evaluate alternatives, e.g., an S4-based design.
- In case integration with *data.table* causes problems, we will involve its user community.

## The Team

- **Iñaki Ucar** is PhD Candidate in Telematic Engineering at Universidad Carlos III de Madrid, Spain. He is an active R package author and contributor, and maintains a number of R packages published on CRAN: [`constants`](https://cran.r-project.org/package=constants) , [`errors`](https://cran.r-project.org/package=errors) (both part of [*r-quantities*](https://github.com/r-quantities)), [`RcppXPtrUtils`](https://cran.r-project.org/package=RcppXPtrUtils), [`simmer`](https://cran.r-project.org/package=simmer) and [`simmer.plot`](https://cran.r-project.org/package=simmer.plot).

- **Edzer Pebesma** is PhD in Geosciences and Professor of Geoinformatics at University of Muenster, Germany. He is an active R package author and contributor, and maintains a number of R packages published on CRAN including
[`units`](https://cran.r-project.org/package=units) (part of [r-quantities](https://github.com/r-quantities)),
[`sf`](https://cran.r-project.org/package=sf) (funded by the R Consortium), 
[`sp`](https://cran.r-project.org/package=sp), 
[`spacetime`](https://cran.r-project.org/package=spacetime), 
[`trajectories`](https://cran.r-project.org/package=trajectories), 
[`gstat`](https://cran.r-project.org/package=gstat), 
[`hexbin`](https://cran.r-project.org/package=hexbin), 
and
[`intervals`](https://cran.r-project.org/package=intervals).

## How Can The ISC Help

The total costs of this project will be USD 10,000, split into the following items:

- Travel costs for an intermediate meeting (flights, accomodation) in Madrid, Muenster or another venue where we can meet (USD 2000).
- Programming, project disemmination (USD 8000).

## Dissemination

The project will use a permissive open-source license such as MIT. The development process will take place in the [*r-quantities*](https://github.com/r-quantities) organisation on GitHub, and the new package will be submitted to CRAN when it is ready. Discussion and contributions will be encouraged through GitHub issues and the R mailing lists.

We will regularly post articles in the author's blog, which is automatically fed into the R news and tutorials site [R-bloggers](https://www.r-bloggers.com/) and Twitter under the well-known *#rstats* hashtag. Also, we will provide articles for the R Consortium blog at the start and end of the project. A publication in the R Journal or a similar scientific journal is foreseen.

## References

[1] Joint Committee for Guides in Metrology. *International Vocabulary of Metrology (VIM) – Basic and General Concepts and Associated Terms*. International Bureau of Weights and Measures, 3rd edition, 2012.

[2] Joint Committee for Guides in Metrology. *Guide to the Expression of Uncertainty in Measurement (GUM)*. International Bureau of Weights and Measures, 1st edition, 2008.

[3] Flater, D. *Architecture for Software-Assisted Quantity Calculus*. NIST Technical Note 1943. December 2016. doi: [10.6028/NIST.TN.1943](https://doi.org/10.6028/NIST.TN.1943). (see also https://www.sciencedirect.com/science/article/pii/S0920548917303069)

[4] Pebesma, E., Mailund, T., Hiebert, J. *Measurement Units in R*. The R Journal, 8 (2), [486--494](https://journal.r-project.org/archive/2016/RJ-2016-061/index.html), December 2016. 
