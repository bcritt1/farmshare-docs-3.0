---
tags:
    - slurm
    - reference
---

The options below work on the command line with `sbatch`, `salloc` and `srun`,
and as `#SBATCH` lines in a batch script. Run `man sbatch` for the full list, or
see the [Slurm documentation](https://slurm.schedmd.com/documentation.html).

## Common Options

| Option | Short form | What it sets | Default |
|---|---|---|---|
| `--partition` | `-p` | Which group of nodes the job runs on | `normal` |
| `--qos` | `-q` | Which set of limits applies (`normal`, `long`, `interactive`, `dev`, `bigmem`, `gpu`) | `normal` |
| `--cpus-per-task` | `-c` | CPU cores per task | 1 (2 on some nodes) |
| `--mem` | | Total memory for the job | Depends on the partition |
| `--mem-per-cpu` | | Memory per CPU core, instead of `--mem` | Depends on the partition |
| `--gpus` | `-G` | Number of GPUs | None |
| `--time` | `-t` | Maximum run time, as `hours:minutes:seconds` or `days-hours:minutes:seconds` | {{ facts.default_runtime }} on `normal` |
| `--job-name` | `-J` | Name shown in `squeue` and the output file | The script name |
| `--output` | `-o` | Where printed output goes | `slurm-<jobid>.out` |
| `--ntasks` | `-n` | Number of tasks, for parallel programs | 1 |

## Slurm Commands

| Command | What it does |
|---|---|
| `sbatch` | Submits a batch script to run later |
| `salloc` | Starts an interactive session with the resources you ask for |
| `srun` | Runs a command on allocated resources |
| `squeue` | Lists jobs that are waiting or running |
| `scancel` | Cancels a job |
| `sinfo` | Shows partitions and node status |
| `sacct` | Shows past jobs and how they ended |

The `interactive` and `caddyshack` partitions are hidden from `sinfo` and
`squeue` by default. Add `-a` to see them.
