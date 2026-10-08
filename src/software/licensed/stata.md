---
tags:
    - software
---

Stata is licensed on FarmShare and comes from the `stata` module. Run it in an
interactive session for exploratory work, or run do-files as batch jobs.

## Run Stata Interactively

Start an interactive session on a compute node, then load the module and start
Stata:

```bash
srun --partition=interactive --qos=interactive --cpus-per-task=4 --pty bash
module load stata
stata
```

You can also run these commands on a login node for small jobs, or in a terminal
in a FarmShare Desktop. See [Get an Interactive
Session](../../use/interactive-sessions.md).

## Run a Do-File in a Batch Job

```bash title="stata-job.sh"
#!/bin/bash
#SBATCH --job-name=stata       # (1)
#SBATCH --cpus-per-task=1      # (2)
#SBATCH --mem=8G               # (3)
#SBATCH --time=02:00:00        # (4)

module load stata              # (5)
stata -b do analysis.do        # (6)
```

1. A name for the job, shown in `squeue`.
2. How many CPU cores the job gets.
3. How much memory the job gets. Stata keeps your whole dataset in memory, so
   allow more than the size of the data.
4. How long the job can run, as hours:minutes:seconds.
5. Loads the default Stata version. Run `module spider stata` to see the others.
6. Runs `analysis.do` without the interactive prompt. The output goes to
   `analysis.log`.

Submit it with `sbatch stata-job.sh`. See [Submit a Batch
Job](../../use/batch-jobs.md).

## Things to Know

The FarmShare Stata license is shared, and only a few people can run Stata at
the same time. If Stata says no license is available, try again later. Close
Stata when you're done so the license is free for someone else.

To move your data files onto FarmShare, see [Move Files to and from
FarmShare](../../use/transfer.md).
