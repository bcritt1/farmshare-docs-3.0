---
tags:
    - slurm
    - jobs
    - mpi
---

A program can use more than one CPU core in two main ways. A multithreaded
program runs as one process that uses several cores on one node. An MPI program
runs as several processes, called tasks or ranks, that pass messages to each
other, and they can be spread across nodes. You ask Slurm for each kind
differently.

**Before you start:** you should know how to write and submit a batch script.
See [Submit a Batch Job](batch-jobs.md).

## Run a Multithreaded Program

Ask for one task with several CPUs, and tell the program how many threads to
use. Many programs, including those built with OpenMP, read the
`OMP_NUM_THREADS` variable:

```bash title="threads.sh"
#!/bin/bash
#SBATCH --job-name=threads-example
#SBATCH --ntasks=1               # (1)!
#SBATCH --cpus-per-task=8        # (2)!
#SBATCH --mem=16G
#SBATCH --time=01:00:00

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK   # (3)!
./my_program
```

1. One process.
2. Eight cores for that process, all on the same node.
3. Uses as many threads as there are cores, without typing the number twice.

Python and R packages that use threads often have their own setting. Check the
package's documentation, and set it from `SLURM_CPUS_PER_TASK` the same way.

## Run an MPI Program

Load the OpenMPI module, then start the program with `mpirun` inside the job.
`mpirun` starts one process for each task Slurm gave the job:

```bash title="mpi.sh"
#!/bin/bash
#SBATCH --job-name=mpi-example
#SBATCH --ntasks=16              # (1)!
#SBATCH --cpus-per-task=1        # (2)!
#SBATCH --mem-per-cpu=2G         # (3)!
#SBATCH --time=01:00:00

module load openmpi              # (4)!
mpirun -np $SLURM_NTASKS ./my_mpi_program
```

1. Sixteen MPI processes.
2. One core for each process.
3. Memory for each core, so the total grows with the number of tasks.
4. Loads OpenMPI, which provides `mpirun` and the compiler wrappers.

To compile your own MPI program, load the same module and use the compiler
wrappers, such as `mpicc` for C:

```bash
module load openmpi
mpicc -o my_mpi_program my_mpi_program.c
```

Compile and run with the same MPI module, so the program finds the libraries it
was built with.

To try MPI interactively, start an [interactive
session](interactive-sessions.md) with the number of cores you want, then run
`mpirun` from its shell.

## Run Across More Than One Node

If your job fits on one node, keep it on one node. It's simpler, and a smaller
request usually starts sooner. If you need more processes than one node has, ask for
nodes and tasks per node:

```bash
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=16
```

Test a small version of the job first. Check that the output reports the
number of ranks you expected, not the same rank repeated, which means the
processes started separately instead of as one MPI program.

## Things to Know

Ask for the number of cores your program uses. A program that uses 4 cores
gets no faster if you ask for 16, and a bigger request waits longer to start.
On some nodes, a request for one CPU gets two, because each core runs two
hardware threads.

The per-person limits on CPUs and jobs are on [Limits](../reference/limits.md).

## If Something Goes Wrong

See [Jobs](../fix/jobs.md). If an MPI program runs but its processes don't
talk to each other, [ask us](../fix/get-help.md), and include your batch
script and output.
