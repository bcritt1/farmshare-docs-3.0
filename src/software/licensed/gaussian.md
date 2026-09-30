---
tags:
    - software
---

Gaussian and its graphical interface, GaussView, are licensed on FarmShare and
are used in chemistry courses. Both come from the `gaussian` module. Use
GaussView in a FarmShare Desktop to build molecules and look at results, and
run longer calculations as batch jobs.

## Use GaussView

**Before you start:** start a FarmShare Desktop in
[OnDemand]({{ facts.ondemand_url }}). See [Run GUI
Programs](../../use/gui-programs.md).

Open a terminal in the desktop and run:

```bash
module load gaussian
gv
```

GaussView also works over SSH with display forwarding (`ssh -X`), but a desktop
is faster and more reliable.

Calculations you start from GaussView run inside the desktop session, and they
stop when the session ends. That's fine for short calculations. For anything
that might outlast the session, save the input file and submit it as a batch
job.

## Run Gaussian in a Batch Job

```bash title="gaussian-job.sh"
#!/bin/bash
#SBATCH --job-name=gaussian    # (1)!
#SBATCH --cpus-per-task=8      # (2)!
#SBATCH --mem=16G              # (3)!
#SBATCH --time=12:00:00        # (4)!

module load gaussian           # (5)!
g16 molecule.gjf               # (6)!
```

1. A name for the job, shown in `squeue`.
2. How many CPU cores the job gets. Set `%NProcShared` in your input file to the
   same number.
3. How much memory the job gets. Set `%Mem` in your input file a little lower,
   so Gaussian stays inside the job's limit.
4. How long the job can run. Jobs can run for up to {{ facts.max_runtime }}.
5. Loads the default Gaussian version. Run `module spider gaussian` to see the
   others.
6. Runs Gaussian 16 on the input file. The output goes to `molecule.log`.

Submit it with `sbatch gaussian-job.sh`. See [Submit a Batch
Job](../../use/batch-jobs.md).

## Things to Know

If a whole class opens desktops for Gaussian at once, choose the smallest
desktop size and shortest time that fit the work. Desktops share the same nodes,
and smaller requests start sooner for everyone. Close the desktop when you're
done rather than leaving it to run out.

Instructors planning to use Gaussian in a course should say so in their course
setup request. See [Request Course Software or Reserved
Nodes](../../teaching/course-software-and-reservations.md).
