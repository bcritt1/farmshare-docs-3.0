---
tags:
    - resources
    - storage
---

Oak is Stanford Research Computing's long-term storage service for research
groups. It's a separate service from FarmShare, with its own documentation, and
it isn't mounted on FarmShare.

## When Oak Is Useful

FarmShare has no long-term storage beyond your home directory, and scratch files
are deleted after {{ facts.purge_days }} days without changes. Oak is for
research data that a group needs to keep and share over the long term.

Because Oak isn't mounted on FarmShare, you can't use files on Oak directly in a
FarmShare job. Copy the data you need into your scratch directory,
`{{ facts.scratch_path }}`, with `rsync` or Globus, and copy results back when
the work is done. See [Move Files to and from FarmShare](../use/transfer.md).

Oak can hold low- and moderate-risk data, but not high-risk data. It isn't
backed up unless the group adds backups.

## Getting Oak Storage

A faculty member or PI rents Oak space for their group, month to month. Ask your
advisor or PI whether your group already has space. Current prices are on
University IT's [Research Computing Storage
Rates](https://uit.stanford.edu/rates/rcstorage) page.

See the [Oak documentation](https://docs.oak.stanford.edu/) to get started.
