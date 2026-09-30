---
tags:
    - slurm
    - jobs
---

A job array runs the same batch script many times, once for each item in a list,
such as a set of input files or parameter values. You submit it with one
`sbatch` command, and Slurm runs the copies, called tasks, as room becomes
available.

**Before you start:** you should know how to write and submit a batch script.
See [Submit a Batch Job](batch-jobs.md).

## Write an Array Script

This script processes ten input files, named `input_1.txt` through
`input_10.txt`, with one task per file:

```bash title="array.sh"
#!/bin/bash
#SBATCH --job-name=array-example
#SBATCH --array=1-10                 # (1)!
#SBATCH --cpus-per-task=1
#SBATCH --mem=4G
#SBATCH --time=00:30:00              # (2)!
#SBATCH --output=array-%A_%a.out     # (3)!

module load python
python3 process.py input_${SLURM_ARRAY_TASK_ID}.txt   # (4)!
```

1. Runs ten tasks, numbered 1 to 10. You can also give a list, such as
   `--array=1,4,7`, or a step, such as `--array=0-100:10`.
2. The resources on the other lines apply to each task, not to the whole array.
   Each task here gets one CPU, 4 GB of memory and 30 minutes.
3. Gives each task its own output file. `%A` is the array's job ID and `%a` is
   the task number.
4. `SLURM_ARRAY_TASK_ID` holds the task's number, so each task works on a
   different file.

Submit it like any other batch script:

```bash
sbatch array.sh
```

## Use the Task Number

The task number doesn't have to be part of a file name. A common pattern is to
list your inputs in a text file, one per line, and have each task read its own
line:

```bash
input=$(sed -n "${SLURM_ARRAY_TASK_ID}p" inputs.txt)
python3 process.py "$input"
```

With 250 lines in `inputs.txt`, use `--array=1-250`.

## Limit How Many Tasks Run at Once

Add `%` and a number to the range to cap how many tasks run at the same time.
This runs at most 20 at once:

```bash
#SBATCH --array=1-250%20
```

This is useful when tasks all read the same files, or when you want to leave
room for your other jobs.

## Check and Cancel Tasks

`squeue -u $USER` shows the array as one line for the tasks still waiting, and
one line for each running task, with IDs like `300992_4`.

To cancel the whole array, or one task:

```bash
scancel 300992
scancel 300992_4
```

## Things to Know

Each task counts as a job toward the per-person limits. On the `normal` QoS you
can have {{ facts.qos.normal.running_jobs }} jobs running and
{{ facts.qos.normal.submitted_jobs }} submitted at once, so `sbatch` refuses an
array that would take you over the submitted limit. For other QoS limits, see
[Limits](../reference/limits.md).

Arrays work best when each task runs for at least a few minutes. If each piece
of work takes seconds, group several pieces into one task, for example by having
each task process ten lines of `inputs.txt`. Thousands of very short tasks spend
more time being scheduled than running.

## If Something Goes Wrong

See [Jobs](../fix/jobs.md).
