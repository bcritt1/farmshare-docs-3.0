---
tags:
    - getting-started
    - storage
---

FarmShare gives you two main places to keep files: your home directory, for
things you want to keep, and your scratch directory, for large working data.
Both are available on every login and compute node.

| Location | Path | Size limit | Backed up | Cleared out |
|---|---|---|---|---|
| Home | `~` or `/home/users/$USER` | {{ facts.home_quota }} | For a short time | No |
| Scratch | `{{ facts.scratch_path }}` | None | No | Files unchanged for {{ facts.purge_days }} days |
| Local temporary space | `/tmp` | The node's local disk | No | When your job ends |

## Home

Your home directory is for files you want to keep: code, scripts, configuration
files, small data sets, and results. It's backed up for a short time, so files
you delete by mistake can sometimes be recovered.

Your home directory holds {{ facts.home_quota }}, the same for everyone. For
larger working data, use scratch. For data you need to keep long term, use
[Oak](../resources/oak.md) if your group has space there.

Keep an eye on how full it is. When your home directory fills up, OnDemand
sessions can't start and jobs can fail. See [Check and Free Up
Space](../use/free-up-space.md).

## Scratch

Your scratch directory, `{{ facts.scratch_path }}`, is for working data that's
too big for your home directory. It has no size limit.

We clear out files in scratch that haven't been changed in
{{ facts.purge_days }} days, so it isn't a place to keep anything long term.
Copy results you need to your home directory or to [Oak](../resources/oak.md),
and delete old files when you're done with them. Don't try to work around the
clean-up.

## Local Temporary Space

Every node has local storage at `/tmp` on fast flash drives. On compute nodes,
`/tmp` belongs to your job and is deleted when the job ends. Use it for
temporary files that a job reads and writes many times.

## Class and Group Directories

Courses and groups can ask for shared directories in `/home/classes`,
`/home/groups`, `/scratch/classes` and `/scratch/groups`. Instructors, see [Set
Up a Course](../teaching/set-up-a-course.md). For a group directory, email
{{ facts.support_email }}.

## AFS

Your Stanford AFS files are available on the login nodes only. See [Use
AFS](../use/afs.md).

## Programs That Scan Files

FarmShare's storage is shared by everyone, and programs that constantly watch or
scan large numbers of files can slow it down for the whole cluster. If you use a
tool that indexes or watches files, such as some editor extensions or backup
tools, set it to look only at your own project folders. Keep it out of `/home`,
`/scratch` and AFS as a whole.
