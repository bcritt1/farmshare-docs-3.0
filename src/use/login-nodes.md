---
tags:
    - login-nodes
---

When you connect to `{{ facts.login_host }}`, you land on one of FarmShare's
login nodes, which are named `rice`. You'll use them to edit files, manage your
data, install software and submit jobs.

## What You Can Do on a Login Node

FarmShare allows more on its login nodes than many clusters do. You can do
substantial work on them, such as compiling software, testing scripts, and
running short analyses. Each person's use of a login node is limited, though,
and work that needs more than those limits should run as a job.

When your work needs more than a login node allows, a GPU, or all of a node's
resources to itself, run it as a job on a compute node instead. See [Submit a
Batch Job](batch-jobs.md) or [Get an Interactive
Session](interactive-sessions.md).

## Which Login Node You Get

`{{ facts.login_host }}` sends each new connection to whichever login node is
least busy, so you may land on a different one each time. Your files are the
same on all of them.

The **FarmShare Shell Access** terminal in OnDemand always opens on `rice-01`.
If you're setting up a class, have students connect with SSH to
`{{ facts.login_host }}` so they spread out across the login nodes.

## AFS

AFS is only available on the login nodes, not on compute nodes or in OnDemand
sessions. See [Use AFS](afs.md).
