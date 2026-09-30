---
tags:
    - troubleshooting
    - ssh
---

These are the most common problems connecting to FarmShare with SSH. For
first-time setup, see [Log In for the First
Time](../get-started/first-login.md).

!!! note "Outages"
    If logins are failing for everyone, FarmShare may be down. Outages and
    maintenance are announced in
    [`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack.

## My Password or Duo Is Rejected

Check [`{{ facts.announce_channel }}`]({{ facts.announce_url }}) first. Most
rejected logins happen during outages or maintenance.

If FarmShare is up, check that you're using your SUNet ID and SUNet password,
and that your SUNet ID is full-service. A full-service ID is one that includes
Stanford email. See [Is FarmShare Right for
Me?](../get-started/is-farmshare-right.md).

## `Connection closed by … port 22` or `Connection refused`

A login node may be down or being restarted. This usually happens during
maintenance. Check [`{{ facts.announce_channel }}`]({{ facts.announce_url }}),
and make sure you're connecting to `{{ facts.login_host }}` rather than a
specific login node, so you're sent to one that's working.

## SSH Warns That the Host Key Has Changed

Compare the fingerprint SSH shows with these:

```text
{{ facts.host_key_ed25519 }} (ED25519)
{{ facts.host_key_rsa }} (RSA)
```

If it matches, remove the old key and connect again:

```sh
ssh-keygen -R {{ facts.login_host }}
```

If it doesn't match, don't connect. Email {{ facts.support_email }}.

## My SSH Key Doesn't Work

FarmShare doesn't accept SSH keys. Log in with your SUNet password and Duo, or
use a Kerberos ticket instead of a password. See [Set Up
SSH](../use/ssh-setup.md).

## SSH Connects Me to the Wrong Machine

A `Host` entry in your `~/.ssh/config` may be matching more names than you meant
it to, for example a pattern like `Host *.stanford.edu`. Check the file for
entries that match `{{ facts.login_host }}`, and make the one for FarmShare
specific.

## I Can't SSH to a Compute Node

You can only connect to a compute node while you have a job running on it. See
[SSH to a Compute Node](../use/ssh-compute-node.md).

## VS Code Remote-SSH Keeps Disconnecting

Connecting VS Code to FarmShare over Remote-SSH isn't supported. Use the VS Code
app in [OnDemand]({{ facts.ondemand_url }}) instead. See [Use VS
Code](../use/vs-code.md).

If you use Remote-SSH anyway, expect a second Duo prompt when it copies its
server files, and check that your home directory isn't full, since that also
breaks it.

## `Invalid account or account/partition combination`

You see this when you submit a job or start an OnDemand session before your
account is fully set up. Part of your account is created the first time you log
in to a login node. Log in once with `ssh SUNetID@{{ facts.login_host }}`, or in
OnDemand select **Clusters** > **FarmShare Shell Access**, then try again.
