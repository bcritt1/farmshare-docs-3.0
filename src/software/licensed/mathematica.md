---
tags:
    - software
---

Mathematica is licensed on FarmShare and comes from the `mathematica` module.
Use notebooks in a FarmShare Desktop, or run Wolfram Language scripts as batch
jobs.

## Use Notebooks

**Before you start:** start a FarmShare Desktop in
[OnDemand]({{ facts.ondemand_url }}). See [Run GUI
Programs](../../use/gui-programs.md).

Open a terminal in the desktop and run:

```bash
module load mathematica
mathematica &
```

## Run a Script in a Batch Job

Save your code as a `.wls` script and run it with `wolframscript`:

```bash title="mathematica-job.sh"
#!/bin/bash
#SBATCH --job-name=mathematica    # (1)!
#SBATCH --cpus-per-task=1         # (2)!
#SBATCH --mem=8G                  # (3)!
#SBATCH --time=02:00:00           # (4)!

module load mathematica           # (5)!
wolframscript -file analysis.wls  # (6)!
```

1. A name for the job, shown in `squeue`.
2. How many CPU cores the job gets.
3. How much memory the job gets.
4. How long the job can run, as hours:minutes:seconds.
5. Loads the default Mathematica version. Run `module spider mathematica` to see
   the others.
6. Runs the script without a notebook.

Submit it with `sbatch mathematica-job.sh`. See [Submit a Batch
Job](../../use/batch-jobs.md).

## If Something Goes Wrong

If Mathematica says it isn't activated or can't find a license, the license
server may be having trouble. It isn't something you can fix by activating your
own copy. Email {{ facts.support_email }} with "FarmShare" in the subject and
include the message.
