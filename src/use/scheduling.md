---
tags:
    - slurm
---

When you submit a job, it waits in a queue until the scheduler finds room for
it. Knowing how the scheduler picks the next job helps when yours is taking a
while to start.

## Priority

Each waiting job has a priority. It goes up the longer the job has waited, and
it depends on the job's size and on how much of FarmShare you've used recently.
Someone who has run a lot of jobs lately gets somewhat lower priority than
someone who hasn't, so heavy use by one person doesn't lock others out. This is
called fair share.

Your choice of partition and QoS also affects where and when a job runs. For
example, the GPU nodes also accept `normal` jobs, but they don't start a
`normal` job while any `gpu` job is waiting.

## Why Nodes Can Look Idle While Jobs Wait

A large job, or one that needs something scarce like GPUs, can wait until enough
resources are free at the same time. The scheduler holds resources back for it
as they free up. Meanwhile, it fills the gaps with smaller, shorter jobs that
will finish before the large job is due to start. This is called backfill.

As a result, `sinfo` can show idle nodes while jobs are still waiting. Those
nodes are usually being held for a job that's about to start.

Shorter time limits help your jobs start sooner, because they fit into more of
these gaps. Set `--time` close to what the job needs.

## See When a Job Might Start

```bash
squeue -u $USER --start
```

This prints the scheduler's current estimate for each of your waiting jobs. The
estimate changes as other jobs finish early or new ones arrive.

The queue is busiest in the weeks before exams.
