---
tags:
    - reference
---

FarmShare is made up of several kinds of machines, each with its own job. All of
them run {{ facts.os }}.

!!! review "Needs Review"
    Is the `bigmem` memory limit per job or per user (across running jobs)?

| Nodes | What they're for |
|---|---|
| `rice` | Login nodes. You connect to these with SSH to edit files, run commands and submit jobs. You can do substantial work on them, within per-user limits. |
| `barley`, `wheat` | Compute nodes for batch jobs. |
| `rye` | Compute nodes for batch jobs, including the `bigmem` partition for jobs that need up to {{ facts.qos.bigmem.mem }} of memory. |
| `oat` | GPU nodes: {{ facts.gpu_nodes }} nodes with {{ facts.gpus_per_node }} {{ facts.gpu_model }} GPUs each. They also run ordinary batch jobs when no GPU jobs are waiting. |
| `iron` | Nodes for interactive sessions, including OnDemand desktops and Caddyshack. |
| `dtn` | Data transfer node, for moving large amounts of data. See [Move Files to and From FarmShare](../use/transfer.md). |

You don't log in to compute nodes directly. You reach them by starting a job or
an OnDemand session. See [Submit a Batch Job](../use/batch-jobs.md) and [Get an
Interactive Session](../use/interactive-sessions.md).

Every node has access to the same home and scratch storage. See [Storage
Locations and Quotas](storage.md).
