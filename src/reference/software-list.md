---
tags:
    - reference
    - software
---

This table lists commonly used software on FarmShare and how to get it. It isn't
the full list. For every module, run `module avail`, and to look for something
by name, run `module spider <name>`. Versions change, so check there rather than
relying on a version you've seen before.

| Software | How to get it | More |
|---|---|---|
| Python | Built in as `python3`, or `module load python` for a newer version | [Python](../software/python.md) |
| uv | `uv` command, or install it yourself | [Python](../software/python.md) |
| R | `module load r` | [R](../software/r.md) |
| RStudio | OnDemand app | [Use RStudio](../use/rstudio.md) |
| JupyterLab | OnDemand app | [Use JupyterLab](../use/jupyterlab.md) |
| VS Code | OnDemand app | [Use VS Code](../use/vs-code.md) |
| Linux desktop | OnDemand apps: FarmShare Desktop, Caddyshack Desktop | [Start a Desktop](../use/start-a-desktop.md) |
| Micromamba | `module load micromamba` | [Conda-Style Environments](../software/conda-style-environments.md) |
| Pixi | Install it yourself | [Conda-Style Environments](../software/conda-style-environments.md) |
| Spack | Install it yourself | [Install Software Yourself](../software/install-yourself.md) |
| Apptainer | `module load apptainer` | [Containers](../software/containers.md) |
| Podman | Built in as `podman` | [Containers](../software/containers.md) |
| CUDA | `module load {{ facts.cuda_module }}` | [Use GPUs](../use/gpus.md) |
| Compilers and MPI | Modules; run `module spider gcc` or `module spider openmpi` | [Run Parallel and MPI Jobs](../use/mpi.md) |
| MATLAB | `module load matlab`, or the OnDemand MATLAB app | [MATLAB](../software/licensed/matlab.md) |
| Gaussian and GaussView | `module load gaussian` | [Gaussian and GaussView](../software/licensed/gaussian.md) |
| Stata | `module load stata` | [Stata](../software/licensed/stata.md) |
| Ansys and HFSS | `module load ansys` | [Ansys and HFSS](../software/licensed/ansys.md) |
| SAS | `module load sas` | [SAS](../software/licensed/sas.md) |
| Mathematica | `module load mathematica` | [Mathematica](../software/licensed/mathematica.md) |
| Gurobi | `module load gurobi` | [Gurobi](../software/licensed/gurobi.md) |
| Schrödinger | `module load schrodinger` | [Schrödinger](../software/licensed/schrodinger.md) |
| Sentaurus | Provided by EE in the Caddyshack Desktop | [Sentaurus](../software/licensed/sentaurus.md) |
| EE course software | Caddyshack Desktop | [Use Caddyshack for EE Courses](../use/caddyshack.md) |

"Built in" means the program comes with the operating system, {{ facts.os }},
and runs without loading a module.

If something you need isn't here or in `module avail`, see [Request
Software](../software/request.md) or [Install Software
Yourself](../software/install-yourself.md).
