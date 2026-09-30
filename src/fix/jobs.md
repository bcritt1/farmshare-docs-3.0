---
tags:
    - troubleshooting
    - slurm
    - jobs
---

These are the most common problems with batch jobs and interactive sessions:
jobs that won't start, jobs that fail right away, and jobs that stop early. For
GPU jobs, see also [GPUs](gpus.md).

!!! note "Outages"
    If jobs are failing for everyone, FarmShare may be down. Outages and
    maintenance are announced in
    [`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack.

## `Invalid account or account/partition combination`

Your FarmShare account hasn't been fully set up yet. The part of your account
that lets you run jobs is created the first time you log in to a login node.

Log in once with `ssh SUNetID@{{ facts.login_host }}`, or in
[OnDemand]({{ facts.ondemand_url }}) select **Clusters** >
**FarmShare Shell Access**. Then submit the job again.

## My Job Fails Right Away With Exit Code `0:53`

`sacct` shows the job as `FAILED` or `CANCELLED` with exit code `0:53` after a
few seconds, and there's no `slurm-<jobid>.out` file. This usually means your
home directory is full, so the job can't write its output file.

Check how much space you're using:

```sh
du -sh ~
```

We give everyone {{ facts.home_quota }} of home space, which `du` shows as
`{{ facts.home_quota_du }}`. If you're at or near that, clear some space. Caches
from pip, conda and similar tools often take the most, and they're safe to
delete:

```sh
rm -rf ~/.cache/*
```

Move large data you still need to your scratch directory,
`{{ facts.scratch_path }}`. [Check and Free Up Space](../use/free-up-space.md)
shows how to find what's taking up room.

If your home directory isn't full and every job fails this way, the problem may
be on our side. Check `{{ facts.announce_channel }}`, then email
{{ facts.support_email }} with a job ID.

## My Job Is Waiting in the Queue

Run `squeue -u $USER`. The last column gives the reason the job hasn't started:

| Reason | What it means | What to do |
|---|---|---|
| `Priority` | Other jobs are ahead of yours. | Wait. See [How Jobs Get Scheduled](../use/scheduling.md). |
| `Resources` | The job is next, but there isn't room for it yet. | Wait, or ask for fewer CPUs, less memory or less time. |
| `QOSMax…PerUserLimit`, `AssocGrp…Limit` | You've reached a per-person limit, such as CPUs or jobs running at once. | Wait for your other jobs to finish. See [Limits](../reference/limits.md). |
| `ReqNodeNotAvail`, `Reserved for maintenance` | Nodes are held for maintenance or a reservation. | Wait until the maintenance ends, or shorten `--time` so the job finishes before it starts. |

To see when the scheduler expects your jobs to start:

```bash
squeue -u $USER --start
```

The queue is busiest in the weeks before exams. Smaller, shorter jobs start
sooner, because they fit into gaps the scheduler leaves around larger jobs.

## `AssocGrpCPURunMinutesLimit`

Your running jobs, counted as CPUs times their remaining time limit, have
reached the most you can hold at once. The waiting job starts when some of your
running jobs finish. Asking for less `--time` or fewer CPUs also helps.

We don't raise limits for individual people, because the same limits for
everyone are what keep FarmShare fair to share. If your work regularly needs
more than FarmShare allows, or it's sponsored research, it belongs on
[Sherlock](../resources/sherlock.md).

## My Interactive Session Takes a Long Time to Start

Check that you included both `--partition=interactive` and `--qos=interactive`:

```bash
salloc --partition=interactive --qos=interactive
```

Without them, the request goes to the `normal` partition and waits in line with
batch jobs. If you asked for a GPU, the wait can also be long, because batch
jobs that ask for GPUs are scheduled first. See [Get an Interactive
Session](../use/interactive-sessions.md).

## `DUE TO TIME LIMIT`

The job ran out of the time it asked for, and Slurm stopped it. The output file
ends with a line like `CANCELLED AT ... DUE TO TIME LIMIT`, and `sacct` shows
the state `TIMEOUT`.

Ask for more time with `--time`. The default is {{ facts.default_runtime }}, and
you can ask for up to {{ facts.max_runtime }}, or {{ facts.long_max_runtime }}
with `--qos=long`. See [Run Long or Big-Memory
Jobs](../use/long-and-bigmem-jobs.md). We generally don't extend jobs that are
already running, so set the limit with some headroom when you submit.

## `oom_kill` or `OUT_OF_MEMORY`

The job used more memory than it asked for, and Slurm stopped it. The output
file mentions `oom_kill` or the out-of-memory handler, and `sacct` shows the
state `OUT_OF_MEMORY`.

Ask for more with `--mem`. To see how much memory a finished job used, run:

```bash
sacct -j <jobid> --format=JobID,State,MaxRSS,ReqMem
```

For jobs that need more memory than `normal` nodes have, see [Run Long or
Big-Memory Jobs](../use/long-and-bigmem-jobs.md).

## `couldn't chdir to '...': No such file or directory: going to /tmp instead`

The job couldn't reach the directory it was started from. There are two common
causes.

If the path starts with `/afs` or `~/afs-home`, the job was submitted from a
directory in AFS. AFS is only available on the login nodes, not on compute
nodes. Copy the files to your home or scratch directory and submit from there.
See [Use AFS](../use/afs.md).

If the path is in your home or scratch directory, there may have been a
short-lived problem with FarmShare's storage. Submit the job again. If it keeps
happening, email {{ facts.support_email }} with the job ID and the node name.

## My `#SBATCH` Options Are Ignored

Slurm reads `#SBATCH` lines only at the top of the script, before the first
command. Any `#SBATCH` line after a command, or after a blank line followed by a
command, is ignored. Move all of them to right after the `#!/bin/bash` line.
Keep the `#` at the start of each one; it's part of the directive.

## My Cancelled Job Is Stuck in `CG`

`CG` means the job is completing: Slurm is cleaning up after it. This usually
clears on its own and doesn't hold up your other jobs. If it's still there after
a few hours, email {{ facts.support_email }} with the job ID, and we can clear
it.

## Every Job on One Node Fails

If your jobs fail only when they land on a particular node, the node may have a
problem. The node name is in the `NODELIST` column of `squeue` and in `sacct`
output. Email {{ facts.support_email }} with the node name and a job ID, and we
can take the node out of service and fix it.

## Getting Help

[Get Help](get-help.md) lists what to include in a support request. For job
problems, include the job ID, the batch script or the command you ran, and any
error text, copied as text.
