---
tags:
    - reference
    - storage
---

Each place you can keep files on FarmShare has its own size limit and rules for
how long files stay.

| Location | Path | Size limit | Backed up | Cleared out | Available on |
|---|---|---|---|---|---|
| Home | `~` (`/home/users/$USER`) | {{ facts.home_quota }} | Short-term | Never | All nodes |
| Scratch | `{{ facts.scratch_path }}` | None | No | Files not modified in {{ facts.purge_days }} days | All nodes |
| Class and group home | `/home/classes`, `/home/groups` | On request | Ask us | Ask us | All nodes |
| Class and group scratch | `/scratch/classes`, `/scratch/groups` | On request | No | Ask us | All nodes |
| Local temporary | `/tmp` | Node's local disk | No | When the job ends | Each node, separately |
| AFS | `~/afs-home`, `/afs` | Managed by University IT | Managed by University IT | Never | Login nodes only |

Home is for things you want to keep: code, scripts, configuration files, small
data sets and results. Scratch is for working data that doesn't fit in home.
Copy anything you need to keep out of scratch before it's cleared. Scratch isn't
backed up.

`$SCRATCH` isn't set on FarmShare. Use the full path,
`{{ facts.scratch_path }}`.

There's no quota command. `df` shows the size of the whole shared file system,
not your share of it, so check your usage with `du`:

```sh
du -sh ~
```

`du` shows the home limit as `{{ facts.home_quota_du }}`.

On compute nodes, `/tmp` belongs to the running job and is deleted when the job
ends. On login nodes, it's cleared often.

Class and group directories are set up on request. See [Set Up a
Course](../teaching/set-up-a-course.md) or email {{ facts.support_email }}.

For how to choose among these, see [Where to Put Your
Files](../get-started/where-to-put-files.md). For AFS, see [Use
AFS](../use/afs.md).
