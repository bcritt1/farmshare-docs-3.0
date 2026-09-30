---
tags:
    - getting-started
    - slurm
---

On FarmShare, heavy computing runs as a job on a compute node. You describe what
to run in a short script, submit it, and the scheduler, Slurm, runs it when
there's room. This page walks through a first job from start to finish.

**Before you start:** [log in](first-login.md) with SSH, or open a terminal from
**Clusters** > **FarmShare Shell Access** in OnDemand.

## Write a Program to Run

This example uses a Python script that adds up the numbers 1 through 5. Create a
file called `sum.py` with this content, using an editor such as `nano`
(`nano sum.py`, then ++ctrl+o++ to save and ++ctrl+x++ to exit):

```python title="sum.py"
a = (1, 2, 3, 4, 5)
x = sum(a)
print(x)
```

## Write a Batch Script

A batch script tells Slurm what resources your job needs and what commands to
run. Create a file called `example.sh`:

```sh title="example.sh"
#!/bin/bash

#SBATCH --job-name=example
#SBATCH --partition=normal
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --time=00:10:00

module load python
python3 sum.py
```

The `#SBATCH` lines are options for Slurm. They start with `#`, and they need to
keep it. This job asks for one CPU for up to ten minutes. The last two lines
load Python and run the script.

If you leave out `--time`, a job on the `normal` partition gets
{{ facts.default_runtime }}. A job still running when its time is up is stopped,
so ask for a bit more time than you expect to need.

## Submit the Job

```sh
sbatch example.sh
```

Slurm replies with a job number:

```text
Submitted batch job 300992
```

## Check on the Job

To see your jobs that are waiting or running:

```sh
squeue -u $USER
```

When the job no longer appears, it has finished.

## Read the Output

Anything your job prints goes to a file named `slurm-<job number>.out`, in the
directory you submitted from:

```sh
cat slurm-300992.out
```

```text
15
```

## Next Steps

- [Submit a batch job](../use/batch-jobs.md) covers more options, such as memory
  and GPUs.
- [Get an interactive session](../use/interactive-sessions.md) if you want to
  work on a compute node directly.
