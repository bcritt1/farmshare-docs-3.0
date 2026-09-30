---
tags:
    - troubleshooting
    - gpu
    - slurm
---

These are common problems with GPU jobs on FarmShare: jobs that fail right away,
jobs that can't see a GPU, and jobs that wait a long time for one. For problems
that affect all jobs, see [Jobs](jobs.md).

!!! note "Outages"
    If GPU jobs are failing for everyone, FarmShare may be down. Outages and
    maintenance are announced in
    [`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack.

## My GPU Job Fails Right Away With Exit Code `0:53`

`sacct` shows the job as `FAILED` or `CANCELLED` with exit code `0:53` after a
few seconds, and there's no `slurm-<jobid>.out` file. This usually means your
home directory is full, so the job can't write its output file. It has nothing
to do with the GPU itself.

Check how much space you're using:

```sh
du -sh ~
```

We give everyone {{ facts.home_quota }} of home space. `du` reports sizes in
GiB, so a full home directory shows as about `{{ facts.home_quota_du }}`.
Machine learning packages and downloaded models take up a lot of it. Caches from
pip, conda and similar tools are safe to delete:

```sh
rm -rf ~/.cache/*
```

Move large data sets, checkpoints and models to your scratch directory,
`{{ facts.scratch_path }}`. [Check and Free Up Space](../use/free-up-space.md)
shows how to find what's taking up room.

If your home directory isn't full, the node the job landed on may have a
problem. Get the node name with
`sacct -j <jobid> --format=JobID,State,ExitCode,NodeList`, and email
{{ facts.support_email }} with it and the job ID.

## My Job Doesn't See a GPU

If `nvidia-smi` says it can't find a GPU, or PyTorch reports
`torch.cuda.is_available()` as `False`, check where the code is running.

The login nodes don't have GPUs, so GPU code has to run in a job. GPUs also
aren't allocated unless you ask for them, even on the `gpu` partition. Include
both options:

```bash
#SBATCH --partition=gpu
#SBATCH --gpus=1
```

Put `nvidia-smi` at the start of the job script. If it lists a GPU and your
program still doesn't use it, the problem is in the software. PyTorch,
TensorFlow and many other packages install with their own copy of the CUDA
libraries, so install a GPU build of the package in a [virtual
environment](../software/python.md). If you need the CUDA toolkit to compile
code, load it with `module load {{ facts.cuda_module }}`.

<!-- NEEDS REVIEW: How do you request a GPU in the OnDemand JupyterLab and
desktop forms? -->

The same applies to JupyterLab and desktops in OnDemand: the session only has a
GPU if you asked for one when you launched it.

## My GPU Job Is Waiting in the Queue

There are {{ facts.gpu_nodes * facts.gpus_per_node }} GPUs on FarmShare, shared
by everyone, so GPU jobs often wait longer than CPU jobs. It's busiest in the
weeks before exams and near assignment deadlines. Run `squeue -u $USER` and
check the reason in the last column.
[Jobs](jobs.md#my-job-is-waiting-in-the-queue) explains each one.

Each person can use up to {{ facts.qos.gpu.gpus }} GPUs at a time, and jobs past
that limit wait until your other GPU jobs finish. Asking for one GPU instead of
several, and for a shorter `--time`, helps a job start sooner.

Interactive GPU sessions usually wait longer than batch jobs, because batch jobs
that ask for GPUs are scheduled first. For anything more than a quick test,
submit a batch job.

## My Job Is Pending and the GPU Nodes Are Down

GPU nodes sometimes stop accepting jobs because of a hardware fault, and they
need an administrator to bring them back. If your GPU job has been pending for a
long time and several GPU nodes show as `drain` or `down` in `sinfo -p gpu`,
email {{ facts.support_email }} with the node names. We have to restart those
nodes before they can run jobs again.

## My GPU Job Needs More Than {{ facts.max_runtime }}

<!-- NEEDS REVIEW: Can a GPU job run for up to 7 days on the normal partition
with the long QoS and one GPU, and which GPU limit applies to it? -->

The `gpu` partition doesn't allow the `long` QoS. To run a GPU job for up to
{{ facts.long_max_runtime }}, submit it to the `normal` partition with the
`long` QoS and ask for one GPU:

```bash
#SBATCH --partition=normal
#SBATCH --qos=long
#SBATCH --gpus=1
```

The `normal` QoS allows {{ facts.qos.normal.gpus }} GPU per person. See
[Limits](../reference/limits.md) and [Run Long or Big-Memory
Jobs](../use/long-and-bigmem-jobs.md). If your program can save checkpoints as
it runs, a job that stops early can restart from the last one instead of from
the beginning.

## Getting Help

[Get Help](get-help.md) lists what to include in a support request. For GPU
problems, include the job ID, the node name, the batch script, and the output of
`nvidia-smi` from inside the job, copied as text.
