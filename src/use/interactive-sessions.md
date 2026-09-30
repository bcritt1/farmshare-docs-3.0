---
tags:
    - slurm
    - jobs
---

An interactive session gives you a shell on a compute node, where you type
commands and see the results as they run. Use one when you need more CPUs or
memory than the login nodes allow, or a GPU, but still want to work by hand.

For a graphical desktop, JupyterLab or RStudio, use
[OnDemand](start-a-desktop.md) instead. Those also run as interactive sessions.

## Start a Session

```bash
salloc --partition=interactive --qos=interactive
```

When the session starts, your prompt changes to the name of the compute node:

```text
salloc: Nodes wheat-01 are ready for job
sunetid@wheat-01:~$
```

Both options are needed. Without them, the request goes to the `normal`
partition and waits in line with batch jobs.

To ask for more than the default resources, add the same options you'd use in a
batch script:

```bash
salloc --partition=interactive --qos=interactive --cpus-per-task=4 --mem=16G --time=04:00:00
```

To add a GPU, include `--gpus=1`. GPUs in interactive sessions are limited, and
batch jobs that ask for GPUs are scheduled first, so the wait can be long.

Type `exit` to end the session and give the resources back.

## Things to Know

Interactive sessions run for up to {{ facts.interactive_max_runtime }}. Each
person can have {{ facts.qos.interactive.jobs }} running at once, with up to
{{ facts.qos.interactive.cpus }} CPUs and {{ facts.qos.interactive.mem }} of
memory across them. We keep these limits so the interactive nodes stay available
for everyone working live, including students in class.

If your work runs longer than a day, or doesn't need you at the keyboard, run it
as a [batch job](batch-jobs.md). A batch job keeps running after you disconnect.

## If Something Goes Wrong

See [Jobs](../fix/jobs.md).
