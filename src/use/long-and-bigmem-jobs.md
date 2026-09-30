---
tags:
    - slurm
    - jobs
---

Most jobs fit within the default limits. This page covers the two ways to go
past them: the `long` QoS for jobs that run more than {{ facts.max_runtime }},
and the `bigmem` partition for jobs that need a lot of memory.

## Jobs That Run Longer than {{ facts.max_runtime }}

Add `--qos=long` and set a time limit of up to {{ facts.long_max_runtime }}:

```bash
#SBATCH --partition=normal
#SBATCH --qos=long
#SBATCH --time=5-00:00:00
```

Each person can have {{ facts.qos.long.running_jobs }} `long` jobs running at
once, using up to {{ facts.qos.long.cpus }} CPUs between them. Long jobs hold
their resources for days, so we keep the number small to leave room for everyone
else.

If a job needs more than {{ facts.long_max_runtime }}, split it into pieces that
save their progress and pick up where the last one stopped. We generally don't
extend running jobs.

## Jobs That Need a Lot of Memory

Submit to the `bigmem` partition and ask for the memory you need:

```bash
#SBATCH --partition=bigmem
#SBATCH --mem=500G
```

Each person can use up to {{ facts.qos.bigmem.mem }} of memory on `bigmem`,
across up to {{ facts.qos.bigmem.running_jobs }} running jobs. There are only
two big-memory nodes, so use `bigmem` only when the job doesn't fit on `normal`.

## When FarmShare Isn't Big Enough

We don't raise limits for individual people. If your work regularly needs more
time, memory or GPUs than FarmShare offers, or if it's funded research, it
belongs on [Sherlock](../resources/sherlock.md).

For the full set of limits, see [Limits](../reference/limits.md).
