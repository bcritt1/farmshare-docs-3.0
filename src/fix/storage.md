---
tags:
    - troubleshooting
    - storage
---

These are the most common problems with storage, quotas and moving files. For
where files belong in the first place, see [Storage Locations and
Quotas](../reference/storage.md).

## `No space left on device` or `Disk quota exceeded`

Your home directory is full. When that happens, OnDemand sessions can't start,
some jobs fail right away, and uploads stop partway through.

Connect with SSH and check how much space you're using:

```sh
ssh SUNetID@{{ facts.login_host }}
du -sh ~
```

The limit is {{ facts.home_quota }}, which `du` shows as
`{{ facts.home_quota_du }}`. To see which directories are taking the most space,
including hidden ones:

```sh
du -h --max-depth=1 ~ | sort -h
```

Caches from pip, conda and similar tools often take the most space, and they're
safe to delete:

```sh
rm -rf ~/.cache/*
```

Move large data you still need to your scratch directory,
`{{ facts.scratch_path }}`. See [Check and Free Up
Space](../use/free-up-space.md) for more ways to clear space.

## I Deleted Files but I'm Still Over My Quota

Check for large hidden directories, like `~/.cache`, `~/.conda` or `~/.local`,
which `ls` doesn't show by default. The `du` command in the previous problem
includes them.

## `df` Shows a Huge Disk That's Almost Empty, or Almost Full

`df` reports on the whole shared file system that everyone's home directories
live on, not on your share of it. Use `du -sh ~` instead. FarmShare doesn't have
a quota command.

## I Need More Space in My Home Directory

We give everyone {{ facts.home_quota }} of home space and can't raise it for
individual people. FarmShare's storage is shared and free, and keeping home the
same size for everyone is how we keep it fair.

For bigger data, use your scratch directory. It has no size limit, but files you
haven't modified in {{ facts.purge_days }} days are deleted, so copy anything
you need to keep somewhere else. Classes and groups can ask for shared
directories by emailing {{ facts.support_email }}.

## My Files in Scratch Are Gone

Files in scratch that haven't been modified in {{ facts.purge_days }} days are
deleted automatically, and scratch isn't backed up, so we can't restore them.
Keep anything you need long term in your home directory or off FarmShare.

## I Can't Find My Old Scratch Data After the December 2025 Upgrade

Scratch data from before the December 2025 upgrade wasn't copied to the new
storage automatically, and the old path, `/farmshare/user_data/$USER`, no longer
exists. Email {{ facts.support_email }} to ask whether your old data can be
copied over.

## I Deleted Something From My Home Directory by Mistake

Home directories have short-term backups, so a recently deleted file may be
recoverable. Email {{ facts.support_email }} as soon as you can with the full
path of what you lost and roughly when it was deleted.

## My Upload Fails Partway Through

In WinSCP this can show up as `Error code 4`. The usual cause is a full home
directory. See [`No space left on device` or
`Disk quota exceeded`](#no-space-left-on-device-or-disk-quota-exceeded).

For large uploads, use the data transfer node, `{{ facts.dtn_host }}`, or
Globus. See [Move Files to and From FarmShare](../use/transfer.md).

## The Transfer Node Resets My Connection

If connections to `{{ facts.dtn_host }}` reset or are refused while other
FarmShare connections work, the problem is probably on our side. Email
{{ facts.support_email }} with the time it happened and the command or program
you used.

## I Can't Reach My AFS Files From a Job or OnDemand

AFS is only available on the login nodes. Copy the files you need to your home
or scratch directory first. See [Use AFS](../use/afs.md).
