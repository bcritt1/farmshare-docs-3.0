---
tags:
    - troubleshooting
    - policy
---

These questions come up often in support requests. Each answer says what you can
do instead.

## Why Can't I Get More Home Space?

Everyone gets {{ facts.home_quota }} of home space. FarmShare is a shared
system, and that's the amount we can offer for free while keeping it working
well for everyone, so we can't raise it for individual people. If you need more
space, use your scratch directory for working data, or
[Oak](../resources/oak.md) for data you need to keep.

Your scratch directory, `{{ facts.scratch_path }}`, has no size limit. We clear
out files there that haven't changed in {{ facts.purge_days }} days, so keep
copies of anything important somewhere else. Classes and groups can ask for
shared directories by emailing {{ facts.support_email }}. If you've run out of
space, [Check and Free Up Space](../use/free-up-space.md) shows what's usually
taking it up.

## Why Can't I Raise My Job Limits?

Everyone on FarmShare has the same limits on CPUs, memory, GPUs and run time.
FarmShare is a shared system, and these limits keep it working well for
everyone, so we don't raise them for individual people.

If your work regularly needs more than FarmShare allows, or it's sponsored
research, it belongs on [Sherlock](../resources/sherlock.md). The current limits
are on [Limits](../reference/limits.md).

## Why Can't I Use `sudo`?

Only administrators can change the system on FarmShare, because it's shared by
everyone.

You can install most software yourself, in your home directory, without
administrator rights. See [Install Software
Yourself](../software/install-yourself.md). If you need a system package, [ask
us](../software/request.md) to install it.

## Why Can't You Extend My Session?

Interactive sessions, including desktops, run for up to
{{ facts.interactive_max_runtime }}. We generally don't extend them, because
keeping sessions time-limited is how everyone gets a turn on the interactive
nodes.

If your work takes longer than that, or doesn't need you to watch it, run it as
a [batch job](../use/batch-jobs.md). Batch jobs keep running when you close your
browser, and they can run for up to {{ facts.max_runtime }}, or
{{ facts.long_max_runtime }} with the `long` option. Set the time limit with
some headroom when you submit, since we generally don't extend running jobs
either.

If a desktop seems to have ended while you were away, it may still be running
behind the screen lock. See [My Password Won't Unlock the
Desktop](ondemand.md#my-password-wont-unlock-the-desktop).

## Why Can't I Log In With an SSH Key?

Stanford's [Minimum Security
Standards](https://uit.stanford.edu/guide/securitystandards) require both a
password, or an equivalent credential like a Kerberos ticket, and two-step
authentication for systems like FarmShare. SSH keys don't meet that requirement,
so FarmShare doesn't accept them.

To avoid typing your password every time, use a Kerberos ticket instead. [Set Up
SSH](../use/ssh-setup.md#use-kerberos-instead-of-your-password) shows how.

## Where Can I See If FarmShare Is Having Trouble?

We post outages, maintenance and other service news in
[`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack. Check there
first. If nothing's posted and FarmShare isn't working for you, email
{{ facts.support_email }} with what you tried and when.

## Why Isn't AFS Available in My Jobs?

AFS is an older Stanford file system, and FarmShare connects to it only on the
login nodes, as a convenience for reaching course materials and personal files
still stored there. It isn't available on compute nodes or in OnDemand.

Copy what you need from AFS into your home or scratch directory on a login node,
and use the copy in your jobs. See [Use AFS](../use/afs.md).
