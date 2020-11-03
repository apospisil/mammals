
<!-- README.md is generated from README.Rmd. Please edit that file -->

mammals
=======

<!-- badges: start -->
name: R

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: macOS-latest
    strategy:
      matrix:
        r-version: [3.5, 3.6]

    steps:
      - uses: actions/checkout@v2
      - name: Set up R ${{ matrix.r-version }}
        uses: r-lib/actions/setup-r@ffe45a39586f073cc2e9af79c4ba563b657dc6e3
        with:
          r-version: ${{ matrix.r-version }}
      - name: Install dependencies
        run: |
          install.packages(c("remotes", "rcmdcheck"))
          remotes::install_deps(dependencies = TRUE)
        shell: Rscript {0}
      - name: Check
        run: rcmdcheck::rcmdcheck(args = "--no-manual", error_on = "error")
        shell: Rscript {0}
<!-- badges: end -->

The goal of mammals is to track mammal data for various species

Installation
------------

You can install the released version of mammals with:

    install.packages("devtools")
    remotes::install_github("mawiramawira/mammals")
