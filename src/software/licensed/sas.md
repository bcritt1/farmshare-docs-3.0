---
tags:
    - software
---

SAS is licensed on FarmShare and comes from the `sas` module. Run SAS programs
as batch jobs, or from an interactive session.

## Run a SAS Program

```bash title="sas-job.sh"
#!/bin/bash
#SBATCH --job-name=sas         # (1)
#SBATCH --cpus-per-task=1      # (2)
#SBATCH --mem=8G               # (3)
#SBATCH --time=02:00:00        # (4)

module load sas                # (5)
sas analysis.sas               # (6)
```

1. A name for the job, shown in `squeue`.
2. How many CPU cores the job gets.
3. How much memory the job gets.
4. How long the job can run, as hours:minutes:seconds.
5. Loads SAS. Run `module spider sas` to see the installed versions.
6. Runs `analysis.sas`. SAS writes its log to `analysis.log` and its output to
   `analysis.lst`.

Submit it with `sbatch sas-job.sh`. See [Submit a Batch
Job](../../use/batch-jobs.md).

To run the same commands interactively, start an [interactive
session](../../use/interactive-sessions.md) first.

## If Something Goes Wrong

If the module won't load or SAS reports a license problem, email
{{ facts.support_email }} with "FarmShare" in the subject and include the full
error.
