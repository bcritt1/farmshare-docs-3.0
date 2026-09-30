---
tags:
    - storage
    - transfer
---

You can move files between your computer and FarmShare with any tool that uses
SSH, or with Globus. For a few small files, connecting to
`{{ facts.login_host }}` is fine. For anything large, use FarmShare's data
transfer node, `{{ facts.dtn_host }}`, which is set up for moving data.

Like every SSH connection to FarmShare, connecting to the data transfer node
asks for your password and Duo.

## Copy Files With scp

`scp` works like `cp`, with a host name on one side. Run these on your own
computer, not on FarmShare.

To copy a file from your computer to your FarmShare home directory:

```sh
scp results.csv sunetid@{{ facts.dtn_host }}:~/
```

To copy a file from FarmShare to the current folder on your computer:

```sh
scp sunetid@{{ facts.dtn_host }}:~/results.csv .
```

## Copy Folders With rsync

`rsync` is better for whole folders and for keeping copies in sync, because it
only transfers files that have changed. This copies a local folder `data` into
your scratch directory:

```sh
rsync -av data/ sunetid@{{ facts.dtn_host }}:/scratch/users/sunetid/data/
```

If a transfer is interrupted, run the same command again, and rsync picks up
where it left off.

## Graphical Apps

If you'd rather drag and drop, apps like [WinSCP](https://winscp.net/)
(Windows), [Cyberduck](https://cyberduck.io/) (Windows, macOS) and
[SecureFX](https://uit.stanford.edu/software/scrt_sfx) (licensed by Stanford)
connect over SSH. Use `{{ facts.dtn_host }}` as the server, and your SUNet ID
and password to log in.

## Cloud Storage With rclone

[rclone](https://rclone.org/) can copy files to FarmShare from your computer
over SSH. Run on a FarmShare login or compute node, it can also copy files from
cloud storage services it supports.

## Globus

[Globus](https://www.globus.org/) transfers files through a web browser. It's
the fastest option for large transfers, and it can move files between FarmShare
and your computer or other Globus endpoints, such as Sherlock and Oak.

To use it, open the [{{ facts.globus_endpoint }}]({{ facts.globus_url }})
endpoint and log in with the organization "Stanford University". You can also
reach Globus from the **Files** app in [OnDemand]({{ facts.ondemand_url }}).

## If a Transfer Fails

If an upload fails partway through, check whether your home directory is full.
Copy large data to your scratch directory instead. See [Check and Free Up
Space](free-up-space.md).
