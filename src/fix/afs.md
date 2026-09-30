---
tags:
    - troubleshooting
    - afs
    - storage
---

AFS is available on FarmShare's login nodes only, which is behind most of the
problems below. [Use AFS](../use/afs.md) covers where AFS is and how to work
with it.

## `couldn't chdir to '...': No such file or directory: going to /tmp instead`

The job was submitted from a directory in AFS, such as one under `/afs` or
`~/afs-home`. AFS isn't available on compute nodes, so the job can't reach that
directory when it starts.

Copy the files to your home or scratch directory on a login node, then submit
the job from there:

```sh
cp -r ~/afs-home/project ~/project
cd ~/project
sbatch job.sh
```

If the path in the error is in your home or scratch directory rather than AFS,
see the same error on
[Jobs](jobs.md#couldnt-chdir-to-no-such-file-or-directory-going-to-tmp-instead).

## I Can't See My AFS Files in OnDemand or a Desktop

All OnDemand apps, including desktops, JupyterLab and RStudio, run on compute
nodes, where AFS isn't available. `~/afs-home` shows up there but can't be
opened.

To reach AFS from OnDemand, select **Clusters** > **FarmShare Shell Access**,
which opens a terminal on a login node. From there, copy what you need into your
home or scratch directory, and then use the copy in your OnDemand session.

## `Permission denied` in AFS After I've Been Logged In a While

AFS access depends on a Kerberos ticket, which expires. When it does, AFS stops
letting you read or write files you normally can. Renew it on the login node:

```sh
kinit && aklog
```

`kinit` asks for your SUNet password. `aklog` then uses the new ticket to give
you access to AFS again.

## `Connection timed out` When I Open `~/afs-home`

The AFS connection on a login node sometimes stops responding, and commands like
`ls ~/afs-home` hang or time out. Other login nodes are usually still working.

Log out and connect again to `{{ facts.login_host }}`, which may put you on a
different login node. If it keeps happening, run `hostname` and email the node
name to {{ facts.support_email }}. For editing a web site in AFS, use
`{{ facts.afs_web_host }}` instead, as described below.

## FarmShare Shell Access Always Puts Me on the Same Login Node

The **FarmShare Shell Access** app in OnDemand always opens on the same login
node. If AFS isn't working on that node, connect with SSH to
`{{ facts.login_host }}` instead, which spreads connections across the login
nodes:

```sh
ssh SUNetID@{{ facts.login_host }}
```

## I Need to Edit My Web Site in AFS

For quick tasks like editing files for a personal or course web site hosted in
AFS, use `{{ facts.afs_web_host }}` instead of FarmShare. It's set up for that
kind of work, and the AFS connection on FarmShare's login nodes is there only
for convenience.

## Getting Help

[Get Help](get-help.md) lists what to include in a support request. For AFS
problems, include the login node name (run `hostname`), the AFS path, and the
full error, copied as text.
