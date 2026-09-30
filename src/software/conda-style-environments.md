---
tags:
    - software
    - python
    - r
---

[Pixi](https://pixi.prefix.dev/latest/) and
[Micromamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html)
create environments from conda-forge packages. Unlike plain Python or R
environments, they can also install the non-Python and non-R libraries that some
packages depend on, such as C libraries. Use them when a package won't install
with `pip`, `uv` or `install.packages()`.

## Micromamba

Micromamba is available as a module:

```bash
module load micromamba
micromamba create -n myenv -c conda-forge python numpy
micromamba activate myenv
```

Micromamba uses the same commands as conda, so most conda instructions work if
you replace `conda` with `micromamba`.

## Pixi

Pixi keeps an environment inside a project folder and records its packages in a
file you can share. To use it, install it in your home directory with the [Pixi
installer](https://pixi.prefix.dev/latest/installation/):

```bash
pixi init myproject
cd myproject
pixi add python numpy
pixi run python analysis.py
```

## Use an Environment in a Batch Job

Activate the environment in the script, the same way you do by hand. For
Micromamba:

```bash
module load micromamba
micromamba activate myenv
python3 analysis.py
```

For Pixi, run commands through `pixi run` from the project folder.

## Things to Know

Environments and their package caches live in your home directory and count
toward your {{ facts.home_quota }} quota. They grow quickly. Remove environments
you're done with, and clear old downloads with `micromamba clean --all` or
`pixi clean cache`.
