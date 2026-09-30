---
tags:
    - storage
    - afs
---

AFS is an older Stanford file system that some courses and personal web sites
still use. On FarmShare, you can reach your AFS files and course materials
stored in AFS, but only from the login nodes.

## Where to Find AFS

On a login node, your AFS home directory is at `~/afs-home`, and the rest of AFS
is under `/afs`. AFS isn't available on compute nodes or in OnDemand sessions,
including desktops. A job that tries to use a directory in AFS fails with an
error about not being able to change to that directory.

## Work on a Copy

Don't run jobs or heavy work directly on files in AFS. Copy what you need into
your FarmShare home or scratch directory first, from a login node:

```sh
cp -r ~/afs-home/project ~/project
```

## Log Back In to AFS

AFS access uses a Kerberos ticket. If you get permission errors in AFS after
being logged in for a while, renew your access:

```sh
kinit && aklog
```

## Edit a Web Site in AFS

For quick tasks like editing files for a web site hosted in AFS, use
`{{ facts.afs_web_host }}` instead of FarmShare. It's set up for that.
