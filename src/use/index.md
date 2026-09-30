---
tags:
    - ondemand
    - slurm
    - storage
---

You can use FarmShare in your web browser through OnDemand, or run jobs on its
compute nodes from a terminal. These pages are grouped by the kind of work.

## Work in Your Browser

| Page | What it covers |
|---|---|
| [Start a Desktop](start-a-desktop.md) | A Linux desktop on FarmShare, in your browser |
| [Use JupyterLab](jupyterlab.md) | Jupyter notebooks in OnDemand |
| [Use RStudio](rstudio.md) | RStudio in OnDemand |
| [Use VS Code](vs-code.md) | The VS Code editor in OnDemand |
| [Run GUI Programs](gui-programs.md) | Programs with a graphical interface, run in a desktop |
| [Use Caddyshack for EE Courses](caddyshack.md) | The Caddyshack Desktop and the EE `caddy` machines |

## Run Jobs

| Page | What it covers |
|---|---|
| [Submit a Batch Job](batch-jobs.md) | Writing a batch script and submitting it with `sbatch` |
| [Get an Interactive Session](interactive-sessions.md) | A shell on a compute node with `salloc` |
| [Use GPUs](gpus.md) | Asking for GPUs in batch and interactive jobs |
| [Run Long or Big-Memory Jobs](long-and-bigmem-jobs.md) | Jobs that need more time or memory than `normal` gives |
| [Run Many Jobs at Once](job-arrays.md) | Job arrays for running the same script on many inputs |
| [Run Parallel and MPI Jobs](mpi.md) | Jobs that use many cores or several nodes |
| [Job Options Reference](job-options.md) | Common `#SBATCH` options |
| [How Jobs Get Scheduled](scheduling.md) | Why jobs wait and what helps them start sooner |

## Manage Your Files

| Page | What it covers |
|---|---|
| [Check and Free Up Space](free-up-space.md) | Checking home directory usage and making room |
| [Move Files to and from FarmShare](transfer.md) | Copying files with `scp`, `rsync`, graphical apps and Globus |
| [Share Files with a Group](sharing.md) | Group directories and file permissions |
| [Use AFS](afs.md) | Reaching your Stanford AFS files from the login nodes |

## Connect in Other Ways

| Page | What it covers |
|---|---|
| [Set Up SSH](ssh-setup.md) | Kerberos tickets and other SSH clients |
| [SSH to a Compute Node](ssh-compute-node.md) | Connecting to a node where your job is running |
| [Use the Login Nodes](login-nodes.md) | What to run on the login nodes and what to run as a job |
