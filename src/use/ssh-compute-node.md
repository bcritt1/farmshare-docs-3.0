---
tags:
    - ssh
    - jobs
---

You can connect with SSH to a compute node while you have a job running on it.
This is mainly useful for checking on a running job, for example to watch its
memory and CPU use with `top`.

**Before you start:** you need a job running on the node, either a batch job,
an interactive session or an OnDemand app.

## Find the Node

`squeue` shows which node each of your running jobs is on, in the last column:

```bash
squeue -u $USER
```

## Connect from a Login Node

Compute nodes are on FarmShare's private network, so you reach them through a
login node. Log in to FarmShare, then connect to the node by its short name:

```bash
ssh wheat-01
```

## Connect Straight from Your Own Computer

To skip the separate login step, use `-J` to pass through a login node on the
way:

```bash
ssh -J SUNetID@{{ facts.login_host }} SUNetID@wheat-01
```

You approve Duo as usual when you connect.

## Things to Know

You can only connect to nodes where you have a running job. Otherwise the
connection is refused with this message:

```text
Access denied by pam_slurm_adopt: you have no active jobs on this node
```

This keeps compute nodes free for the jobs that were scheduled on them. When
you connect, your SSH session counts as part of your job and shares its cores
and memory, and it ends when the job ends.

Use the short node name, as in the examples. The node's full public hostname
doesn't work from outside FarmShare's private network.

To work interactively on a compute node, you don't need SSH. Start an
[interactive session](interactive-sessions.md) instead, which gives you a
shell on a compute node directly.

## If Something Goes Wrong

See [Logging In](../fix/logging-in.md) and [Jobs](../fix/jobs.md).
