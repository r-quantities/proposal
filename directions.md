---
output:
  pdf_document: default
---

# Project Milestones

- ~~March 2nd: 1st deliverable.~~
- ~~March 31st: Q1 report.~~
- ~~May 4th: 2nd deliverable.~~
- June 29th: 3rd deliverable.
- June 30th: Q2 report.
- August 31st: 4th report. End of the project.

# Action Lines Proposal

## (NEW) CII Best Practices Badge program

Required by the R Consortium in the last communication about the Q2 report.

- Review the badge program and start the application process of achieving a badge (and inform the R Consortium). For `quantities`, and by extension, for `units` and `errors`.
- Provide feedback using the survey.

## (Follow-up) Parsing Data with Units and Errors

Currently, there are parsers implemented in `quantities`: `parse_quantities`, `parse_errors`, `parse_units`. As a possible follow-up, we could try to integrate these parsers into `readr`. Two possible lines of action:

- Submit those readers as a PR to `readr`. `readr` should depend on `quantities` (which is not on CRAN yet), `errors` and `units`.
- Work on `readr` to open its APIs (R and C++) to external parsers. Pros: adds value to `readr` without changing its dependencies. Cons: a little bit more work.

Either way, it requires approval from `readr`'s maintainer (Jim Hester).

## Compatibility with Existing Workflows

The idea is to write a vignette (or several vignettes) describing how to work with quantities in the most typical workflows: R base, tidyverse, data.table. To that end, we should

- Identify all the most common high level operations: filtering, ordering, transformation, aggregation, grouped operations, (un)pivoting, joining... more? Then identify these operations for each workflow:
    - R base: `[` and `subset`, `order`, `transform`, `aggregate`, `by`...
    - tidivyerse: `filter`, `arrange`, `transmute` and `mutate`, `summarise`, `group_by`...
    - data.table: ... :)
- For each workflow and operation, show usage examples, identify incompatibilities, find workarounds.
- Output:
    - A set of working use cases.
    - A set of incompatibilities and possible future action lines to solve them.

## Printing of units and errors

    - follow, and refer to BIPM conventions/best practices
	- implement in pillar methods:
	- units in column header
	- remove/replace <> with []; follow `units_options` that also sets plot output

## Integration with Linear Models

Fitting linear models and extraction of regression coeficients as quantities.
  
  - To be explored; viability TBD.

## (Addendum) Units Development

- Discuss support for heterogeneous units.
- Understand performance issues reported in `sf` in order to:
    - Define a reference benchmark (separate repo). It should be useful for `errors` too.
    - Further investigate the `xptr_cache` branch (units system enclosed in a C++ class):
        - Enables unit caching.
        - The isolation provided centralises memory management.
        - Enables an easy extension to support multiple units systems (long-term goal).

## (Addendum) Errors Development

- Support samples as input. Store the whole sample instead of a single value and an associated error. Operations work directly on these samples, so that every kind of correlation would be captured.
    - More general alternative to the default Taylor-based mechanism.
    - Representation? (matrix vs. list of vectors).
    - Length of samples, resampling.

## Hex stickers

- use logo
