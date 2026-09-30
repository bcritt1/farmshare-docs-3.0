---
tags:
    - software
    - python
---

FarmShare has two versions of Python. The operating system's `python3` is
version {{ facts.python_system_version }}, and `module load python` gives you
{{ facts.python_module_version }}. For your own packages, use a virtual
environment. We recommend creating and managing them with
[uv](https://docs.astral.sh/uv/).

## Create a Virtual Environment with uv

A virtual environment is a folder holding its own Python packages, separate from
everyone else's and from your other projects. uv creates them quickly and stores
packages efficiently, which helps with the {{ facts.home_quota }} home quota.

```bash
uv venv ~/myproject
source ~/myproject/bin/activate
uv pip install numpy
```

This creates the environment in your home directory, at `~/myproject`.
`source ~/myproject/bin/activate` switches your shell to that environment, and
your prompt starts with `(myproject)`. Run `deactivate` to leave it.

uv can also create environments with a specific Python version, for example
`uv venv --python 3.12 ~/myproject`.

If the `uv` command isn't found, install it in your home directory with the
[standalone installer](https://docs.astral.sh/uv/getting-started/installation/).
It doesn't need administrator rights.

## Use the Standard Tools Instead

Python's own `venv` and `pip` also work:

```bash
module load python
python3 -m venv ~/myproject
source ~/myproject/bin/activate
pip install numpy
```

## Use an Environment in a Batch Job

Activate the environment in the script before running Python:

```bash title="python-job.sh"
#!/bin/bash
#SBATCH --job-name=python-example
#SBATCH --time=01:00:00

source ~/myproject/bin/activate
python3 analysis.py
```

If you created the environment with `module load python` loaded, as in the
standard-tools example above, add `module load python` to the script too, before
the `source` line.

## Use an Environment in JupyterLab

To use an environment's packages in the JupyterLab app in
[OnDemand]({{ facts.ondemand_url }}), install it as a Jupyter kernel:

```bash
source ~/myproject/bin/activate
uv pip install ipykernel
python3 -m ipykernel install --user --name myproject
```

The next time you open JupyterLab, `myproject` appears in the list of kernels.

## Things to Know

Environments and package caches live in your home directory and count toward
your {{ facts.home_quota }} quota. Machine learning packages are large, so a few
environments can fill it. Delete environments you no longer use, and clear old
downloads with `uv cache clean` or `pip cache purge`.

For packages that need non-Python libraries, see [Conda-Style
Environments](conda-style-environments.md).
