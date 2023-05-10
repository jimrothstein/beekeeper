
<!-- README.md is generated from README.Rmd. Please edit that file -->

# beekeeper <a href="https://jonthegeek.github.io/beekeeper/"><img src="man/figures/logo.svg" align="right" height="424" /></a>

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)
[![CRAN
status](https://www.r-pkg.org/badges/version/beekeeper)](https://CRAN.R-project.org/package=beekeeper)
[![Codecov test
coverage](https://codecov.io/gh/jonthegeek/beekeeper/branch/main/graph/badge.svg)](https://app.codecov.io/gh/jonthegeek/beekeeper?branch=main)
[![R-CMD-check](https://github.com/jonthegeek/beekeeper/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/jonthegeek/beekeeper/actions/workflows/R-CMD-check.yaml)
<!-- badges: end -->

This package will allow users to automatically generate R package
skeletons from APIs that follow the [OpenAPI Specification
(OAS)](https://spec.openapis.org/oas/v3.1.0) (and probably other
specifications, such as swagger, the predecessor to OpenAPI). The
skeletons will implement best practices to streamline package
development.

## The Plan

This project has been accepted by the [R Consortium 2023 ISC Grant
Program](https://www.r-consortium.org/all-projects/call-for-proposals)!

In general, this is how I anticipate things working:

- Create a class, `tbl_swarm`, which is a list of tbls with an
  opinionated relationship. The exact opinion associated with a given
  `tbl_swarm` leads to subclasses, such as.
- Create a `tbl_swarm` subclass, `api_tbl_swarm`. Such objects will
  contain the result of parsing an API spec into a format that can be
  \~easily built into a package.
- Create a function that takes an `api_tbl_swarm` and creates a package.
  Build backward from here; determine which parts of the spec are
  useful, and how they need to be parsed to be easy to work with.

That general framework will make it cleaner to add different types of
spec or different implementations of the OpenAPI spec (not all specs are
perfect). That way the process is divided more cleanly into “use the
spec to generate the expected `api_tbl_swarm`” and then “use the
`api_tbl_swarm` to generate a package.” That also means I can guide
users through steps to manually make changes to their not-quite-perfect
`tbl_swarm` (`imperfect_tbl_swarm`? `pending_api_tbl_swarm`?) in order
to generate a valid `api_tbl_swarm`.

This is a rough outline of the planned development milestones of this
package, working toward a stable version 1.0.0:

- 0.1.0: Basic authentication and endpoint calls.
  - Export a function to generate `R/*.R` and `tests/testthat/*.R` files
    to authenticate the user and make a call to the API, given the URL
    of an OpenAPI spec in YAML format. The generated files will follow
    and encourage best practices, and will serve as the core around
    which the rest of a package would be built.
  - Produce a vignette about configuring authentication.
  - **Potential challenges:** Authentication is a complex and delicate
    subject. Some APIs require registration of special apps to “catch”
    authentication requests, while others simply provide an API key. I
    will need to carefully navigate these complexities in the vignette.
- 0.2.0: OAS definition discovery.
  - Add support for APIs using the OAS json format.
  - Streamline discovery of API definitions (with associated error
    handling).
  - **Potential challenges:** There does not appear to be a set standard
    of where API definitions are posted on a given site. It might be
    difficult to help users find the right place. Interestingly,
    <https://APIs.guru> itself has a (simple) API to aid in API
    discovery, which might provide an opportunity to use beekeeper to
    generate parts of itself.
- 0.3.0: Batching and rate limiting.
  - Add documentation for implementing batching and rate-limiting.
  - If possible, export functionality to help implement these processes,
    but standards seem to vary widely.
  - **Potential challenges:** This step will involve more reading and
    documenting than code, to gather examples of how different APIs
    implement limits and batching. It’s possible systems will be so
    different that it will be difficult to summarize them. For example,
    Slack has two separate batching systems in its API, with some
    functions moved to the newer system, and others not.
- 0.4.0: Endpoint function scaffolding.
  - Generate R/*.R and tests/testthat/*.R files for all endpoints
    (“paths”) described in the given API specification.
  - The generated functions will work, but error checking,
    documentation, and tests will be minimal.
  - **Potential challenges:** I’ll need to strike a balance here between
    getting a basic working system and producing something that can be
    easily expanded later.
- 0.5.0: More robust scaffolding.
  - Add parameter documentation.
  - Also add parameter type checking.
  - **Potential challenges:** By this point I’ll need an OAS definition
    document to use for testing that includes all of the possible
    parameter types. I’ll likely need to generate a fake API
    specification that goes beyond a typical individual example.
- 0.6.0: Expected results.
  - Add response (return value) documentation.
  - Use expected responses to generate better test scaffolds.
  - **Potential challenges:** Testing the generation of tests might
    present unique challenges. I’ll need to look into how testthat tests
    itself.
- 0.7.0: Error messaging.
  - Add more robust error messaging for non-standard responses.
  - **Potential challenges:** Mocking cases where things fail can be
    tricky. Ideally this step will involve pushing the package to a
    stable 1.0.0, but that will require enough usage to feel confident
    that the core function definitions are stable.

## Installation

You can install the development version of beekeeper from
[GitHub](https://github.com/) with:

``` r
# install.packages("remotes")
remotes::install_github("jonthegeek/beekeeper")
```

## Usage

This package does not yet work.

See
[usethis::create_package()](https://usethis.r-lib.org/reference/create_package.html)
and
[golem::create_golem()](https://thinkr-open.github.io/golem/reference/create_golem.html)
for motivating examples.

## Code of Conduct

Please note that the beekeeper project is released with a [Contributor
Code of
Conduct](https://jonthegeek.github.io/beekeeper/CODE_OF_CONDUCT.html).
By contributing to this project, you agree to abide by its terms.