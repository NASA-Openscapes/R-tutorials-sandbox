# R-tutorials-sandbox

[Open in 2i2c](https://openscapes.2i2c.cloud/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2FNASA-Openscapes%2FR-tutorials-sandbox&urlpath=rstudio&branch=main)

Repository for converting existing tutorials to Quarto and adding R code

## The environments

Python: https://github.com/NASA-Openscapes/corn/blob/main/ci/environment.yml

R: rocker/geospatial:4.2

## SET UP specific for the 2i2c Hub

This is important. The Dockerfile for RStudio has a bug such that it does not set the path correctly so that the Python is in the conda notebook environment. **You only do this once!**

Run this code in the R console:
```
usethis::edit_r_environ()
```
When the `.Renviron` file opens paste this into it.
```
PATH = "/usr/bin:/srv/conda/envs/notebook/bin:/srv/conda/condabin:/usr/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin:/bin:/usr/local/texlive/bin/linux:/usr/local/texlive/bin/linux:/usr/lib/rstudio-server/bin/quarto/bin:/usr/lib/rstudio-server/bin/postback/postback:/usr/bin:/usr/bin:/usr/bin:"
```

## Convert ipynb to qmd

You will need to edit the yaml at the top.

```
format:
  html:
    code-fold: true
```

```
input <- "tutorials/Earthdata_Search_Discovery_earthaccess.ipynb"
filename <- "tutorials/Earthdata_Search_Discovery"
rmarkdown::convert_ipynb(input, output = xfun::with_ext(filename, "qmd"))
```