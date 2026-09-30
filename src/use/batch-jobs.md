---
tags:
    - slurm
    - jobs
---

A batch job runs a script on a compute node without you watching it. You write
the script, submit it, and read the output when it finishes. Batch jobs keep
running after you log out or close your browser, so they're the right choice for
anything that takes more than a few minutes.

FarmShare uses the [Slurm](https://slurm.schedmd.com/) scheduler. If you haven't
submitted a job before, [Run Your First Job](../get-started/first-job.md) walks
through it step by step.

## Write a Batch Script

A batch script is a shell script with `#SBATCH` lines at the top. Those lines
tell Slurm what the job needs. This example runs a small Python script,
`sum.py`, that adds the numbers 1 through 5:

```python title="sum.py"
a = (1, 2, 3, 4, 5)
x = sum(a)
print(x)
```

```bash title="example.sh"
#!/bin/bash
#SBATCH --job-name=example    # (1)!
#SBATCH --partition=normal    # (2)!
#SBATCH --cpus-per-task=1     # (3)!
#SBATCH --mem=4G              # (4)!
#SBATCH --time=00:10:00       # (5)!

module load python            # (6)!
python3 sum.py
```

1. A name for the job, shown in `squeue` and in the output file.
2. Where the job runs. `normal` is the default and fits most jobs.
3. How many CPU cores the job gets.
4. How much memory the job gets. Jobs that use more than this are stopped.
5. How long the job can run, as hours:minutes:seconds. Jobs still running at the
   end of this time are stopped.
6. Loads the software the job needs. See [Find Installed
   Software](../software/modules.md).

Slurm reads `#SBATCH` lines only at the top of the script. Any `#SBATCH` line
that comes after the first command is ignored.

## Submit the Job

```bash
sbatch example.sh
```

Slurm replies with a job ID:

```text
Submitted batch job 300992
```

## Check on the Job

`squeue` lists your jobs that are waiting or running:

```bash
squeue -u $USER
```

To cancel a job, use its ID:

```bash
scancel 300992
```

## Find the Output

Anything the script prints goes to a file named `slurm-<jobid>.out` in the
directory you submitted from:

```bash
cat slurm-300992.out
```

```text
15
```

## Things to Know

If you don't set a time limit, a job on `normal` gets
{{ facts.default_runtime }}. You can ask for up to {{ facts.max_runtime }}, or
{{ facts.long_max_runtime }} with the `long` QoS. See [Run Long or Big-Memory
Jobs](long-and-bigmem-jobs.md).

Ask for what the job needs and not much more. Larger requests wait longer to
start, because the scheduler has to find room for them. Jobs that go over their
memory or time are stopped, so leave a little headroom.

On some nodes, a job that asks for one CPU gets two, because each physical core
runs two hardware threads.

[Job Options Reference](job-options.md) lists the common `#SBATCH` options. For
limits on CPUs, memory and jobs per person, see
[Limits](../reference/limits.md).

## If Something Goes Wrong

See [Jobs](../fix/jobs.md) for jobs that won't start or that stop early.
