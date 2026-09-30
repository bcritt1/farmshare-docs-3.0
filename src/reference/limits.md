---
tags:
    - reference
    - slurm
---

These are the run-time and resource limits that apply to your jobs. The limits
are the same for everyone, and we don't change them for individual people. If
your work needs more than FarmShare allows, see
[Sherlock](../resources/sherlock.md).

## Partitions

A partition is a group of nodes. Choose one with `--partition`. If you don't,
your job goes to `normal`.

| Partition | For | Default time | Maximum time |
|---|---|---|---|
| `normal` | Most batch jobs | {{ facts.default_runtime }} | {{ facts.max_runtime }} ({{ facts.long_max_runtime }} with `--qos=long`) |
| `bigmem` | Jobs that need a lot of memory | {{ facts.default_runtime }} | {{ facts.max_runtime }} |
| `gpu` | Jobs that need GPUs | {{ facts.default_runtime }} | {{ facts.max_runtime }} |
| `interactive` | Interactive sessions and OnDemand apps | — | {{ facts.interactive_max_runtime }} |
| `caddyshack` | EE course work only | — | — |

`interactive` and `caddyshack` don't appear in `sinfo` unless you add `-a`.

## Per-User Limits

These limits apply to everything you're running at once. Choose a quality of
service (QoS) with `--qos`. If you don't, your job uses `normal`.

| QoS | Maximum time | CPUs | Memory | GPUs | Running jobs | Queued jobs |
|---|---|---|---|---|---|---|
| `normal` | Partition maximum | {{ facts.qos.normal.cpus }} | | {{ facts.qos.normal.gpus }} | {{ facts.qos.normal.running_jobs }} | {{ facts.qos.normal.submitted_jobs }} |
| `long` | {{ facts.qos.long.max_time }} | {{ facts.qos.long.cpus }} | | | {{ facts.qos.long.running_jobs }} | {{ facts.qos.long.submitted_jobs }} |
| `dev` | {{ facts.qos.dev.max_time }} | {{ facts.qos.dev.cpus }} | {{ facts.qos.dev.mem }} | | {{ facts.qos.dev.jobs }} | {{ facts.qos.dev.jobs }} |
| `interactive` | {{ facts.interactive_max_runtime }} | {{ facts.qos.interactive.cpus }} | {{ facts.qos.interactive.mem }} | | {{ facts.qos.interactive.jobs }} | {{ facts.qos.interactive.jobs }} |
| `bigmem` | Partition maximum | | {{ facts.qos.bigmem.mem }} | | {{ facts.qos.bigmem.running_jobs }} | {{ facts.qos.bigmem.submitted_jobs }} |
| `gpu` | Partition maximum | | | {{ facts.qos.gpu.gpus }} | {{ facts.qos.gpu.running_jobs }} | {{ facts.qos.gpu.submitted_jobs }} |
| `caddyshack` | | {{ facts.qos.caddyshack.cpus }} | {{ facts.qos.caddyshack.mem }} | | {{ facts.qos.caddyshack.jobs }} | {{ facts.qos.caddyshack.jobs }} |

A blank cell means that QoS has no separate limit of that kind.

## Defaults

A job gets one CPU unless you ask for more. On some nodes it gets two, because
each core runs two threads. The default memory depends on the partition, so set
`--mem` if your job needs a known amount. GPUs are only allocated when you ask
for them with `--gpus`.

For how to request these, see [Job Options Reference](../use/job-options.md).
