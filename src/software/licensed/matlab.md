---
tags:
    - software
    - ondemand
---

MATLAB is licensed on FarmShare for everyone with an account. The easiest way to
use it is the MATLAB app in OnDemand, which opens the full MATLAB desktop in
your browser. For longer work, run MATLAB scripts as batch jobs.

## Use the MATLAB App

1. Go to [OnDemand]({{ facts.ondemand_url }}).
2. Select **Interactive Apps** > **MATLAB**.
3. Choose how long you need and select **Launch**.
4. When the session is ready, select the button to connect.

The session ends at the time you chose, and MATLAB closes with it. Save your
work to your home or scratch directory as you go.

## Run MATLAB in a Batch Job

Write your code as a script or function file, then call it with `matlab -batch`.
This example runs `analysis.m` from the directory you submit the job from:

```bash title="matlab-job.sh"
#!/bin/bash
#SBATCH --job-name=matlab-example    # (1)
#SBATCH --cpus-per-task=4            # (2)
#SBATCH --mem=16G                    # (3)
#SBATCH --time=02:00:00              # (4)

module load matlab                   # (5)
matlab -batch "analysis"             # (6)
```

1. A name for the job, shown in `squeue`.
2. How many CPU cores the job gets. Parallel code such as `parfor` can use up to
   this many workers.
3. How much memory the job gets. MATLAB uses a good deal of memory to start, so
   allow more than your data alone needs.
4. How long the job can run, as hours:minutes:seconds.
5. Loads the default MATLAB version. Run `module spider matlab` to see the
   others.
6. Runs `analysis.m` without the graphical interface, then exits. Use the
   script's name without `.m`.

Submit it with `sbatch matlab-job.sh`. See [Submit a Batch
Job](../../use/batch-jobs.md) for more about batch jobs.

## Run MATLAB from a Terminal

For the MATLAB desktop, use the MATLAB app. In an SSH session or an [interactive
session](../../use/interactive-sessions.md), you can start MATLAB without the
graphical interface:

```bash
module load matlab
matlab -nodisplay
```

## Things to Know

When MATLAB starts from a terminal, it may print
`MATLAB is selecting SOFTWARE OPENGL rendering.` That message on its own isn't
an error. If MATLAB doesn't open after it, use the MATLAB app instead.

Add-on toolboxes are whatever the license includes. To see them, run `ver` at
the MATLAB prompt.

## If Something Goes Wrong

See [OnDemand and Desktops](../../fix/ondemand.md) for problems starting the
app, and [Software and Modules](../../fix/software.md) for problems with the
module.
