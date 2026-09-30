---
tags:
    - slurm
    - gpu
---

FarmShare has {{ facts.gpu_nodes }} GPU nodes, each with
{{ facts.gpus_per_node }} {{ facts.gpu_model }} GPUs. To use them, submit a job
to the `gpu` partition and ask for GPUs with `--gpus`.

## Request a GPU in a Batch Job

```bash title="gpu-job.sh"
#!/bin/bash
#SBATCH --job-name=gpu-example
#SBATCH --partition=gpu
#SBATCH --gpus=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=32G
#SBATCH --time=02:00:00

nvidia-smi
python3 train.py
```

GPUs aren't allocated unless you ask for them, even on the `gpu` partition.
Running `nvidia-smi` at the start of the job shows which GPU the job got.

## Use a GPU Interactively

```bash
salloc --partition=interactive --qos=interactive --gpus=1
```

Interactive GPUs are limited, and batch jobs that ask for GPUs are scheduled
first, so an interactive GPU session can wait a long time. For anything longer
than a quick test, a batch job usually starts sooner.

## Software for GPUs

The CUDA toolkit is available as a module:

```bash
module load {{ facts.cuda_module }}
```

Many Python packages, including PyTorch and TensorFlow, install with their own
copy of the CUDA libraries, so you may not need the module at all. Install them
in a [virtual environment](../software/python.md).

Modules built for GPUs are marked with a `g` in `module avail`. See [Find
Installed Software](../software/modules.md).

## Things to Know

Each person can use up to {{ facts.qos.gpu.gpus }} GPUs at a time, across up to
{{ facts.qos.gpu.running_jobs }} running jobs. There are
{{ facts.gpu_nodes * facts.gpus_per_node }} GPUs on FarmShare, shared by
everyone, so this limit keeps a few large jobs from filling them all.

GPU jobs have the same time limits as other jobs: {{ facts.default_runtime }} by
default and up to {{ facts.max_runtime }}.

For a course that needs GPUs for an assignment, instructors can ask us to
reserve some. See [Request Course Software or Reserved
Nodes](../teaching/course-software-and-reservations.md).

## If Something Goes Wrong

See [GPUs](../fix/gpus.md).
