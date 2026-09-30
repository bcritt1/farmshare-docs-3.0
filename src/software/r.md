---
tags:
    - software
    - r
---

R is available as a module, and in the RStudio app in
[OnDemand]({{ facts.ondemand_url }}). Packages you install go into a personal
library in your home directory.

## Start R

```bash
ml r
R
```

## Install Packages

```r
install.packages("dplyr")
```

The shared R library isn't writable, so R installs packages into a personal
library in your home directory instead. The first time you install a package, R
asks whether to create one. Answer yes.

Packages you install from a terminal are also available in RStudio, and the
other way around.

Some packages fail to install from inside RStudio but install fine from R in a
terminal. If an install fails in RStudio, try it from a terminal first.

## Keep Project Environments with renv

`renv` records the exact packages a project uses, so you can recreate its
environment later or share it:

```r
install.packages("renv")
renv::init()
```

See the [renv documentation](https://rstudio.github.io/renv/) for more.

## Packages That Need System Libraries

Some R packages depend on libraries written in other languages, such as C. If an
install fails because a library is missing, you can use [Pixi or
Micromamba](conda-style-environments.md), which install those libraries
alongside R. Or [ask us](request.md) to add the library, and include the package
name and the full error.

## Things to Know

Your personal library counts toward your {{ facts.home_quota }} home quota.
