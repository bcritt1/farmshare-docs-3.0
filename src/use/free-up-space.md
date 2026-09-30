---
tags:
    - storage
---

Your home directory holds {{ facts.home_quota }}. When it's full, OnDemand
sessions can't start, jobs can fail, and uploads stop partway through. This page
shows how to check your usage and make room.

## Check How Much Space You're Using

Run this on a login node:

```sh
du -sh ~
```

`du` reports sizes in GiB, so a full home directory shows as about
`{{ facts.home_quota_du }}`. If the number is at or near that, your home
directory is full.

Don't use `df` for this. Your home directory is on storage shared with everyone
else, and `df` shows the free space on that whole system, not your own usage.
FarmShare doesn't have a `quota` command.

If your home directory is full, the OnDemand **Files** app may not work. Use
SSH, or **Clusters** > **FarmShare Shell Access** in OnDemand, which still works
when your home directory is full.

## Find What's Taking Up Space

This lists each file and folder in your home directory, including hidden ones,
with the largest at the bottom:

```sh
du -h -d 1 --apparent-size ~ | sort -h
```

It can take a while if you have many files. Run it again inside a large folder
to see what's taking up space there.

## Common Culprits

Hidden folders often turn out to be the problem. Caches from pip, conda and
similar tools collect in `~/.cache` and are safe to delete:

```sh
rm -rf ~/.cache/*
```

Python and R environments and packages can also get large, because they install
into your home directory.

## Move Large Data to Scratch

Your scratch directory, `{{ facts.scratch_path }}`, has no size limit, so it's
the place for large data sets and working files. Files there that haven't
changed in {{ facts.purge_days }} days are cleared out, so keep copies of
anything important in your home directory or on [Oak](../resources/oak.md), if
your group has space there.

```sh
mv ~/big-dataset {{ facts.scratch_path }}/
```

See [Where to Put Your Files](../get-started/where-to-put-files.md) for more on
each storage location.
