---
tags:
    - ssh
    - connecting
---

These are optional ways to make connecting to FarmShare easier: Kerberos, so you
don't type your password on every connection, and other SSH clients. For the
basics, see [Log In for the First Time](../get-started/first-login.md).

## Why SSH Keys Don't Work

Stanford's [Minimum Security
Standards](https://uit.stanford.edu/guide/securitystandards) require both a
password (or an equivalent credential, like a Kerberos ticket) and two-step
authentication for systems like FarmShare. SSH keys don't meet that requirement,
so FarmShare doesn't accept them.

## Use Kerberos Instead of Your Password

If your computer has Kerberos, you can get a Kerberos ticket once and use it in
place of your password when you connect. A ticket lasts
{{ facts.kerberos_lifetime }} and can be renewed for up to
{{ facts.kerberos_renewable }}, so you type your password much less often. You
still approve Duo when you connect.

1. Get a ticket:

    ```sh
    kinit sunetid@stanford.edu
    ```

2. Check that you have one:

    ```sh
    klist
    ```

3. On some computers you also need to turn on Kerberos (GSSAPI) in your SSH
   configuration. Add this to `~/.ssh/config` on your own computer:

    ```text title="~/.ssh/config"
    Host {{ facts.login_host }}
      GSSAPIKeyExchange yes
      GSSAPIAuthentication yes
      GSSAPIRenewalForcesRekey yes
      PreferredAuthentications gssapi-with-mic,publickey,keyboard-interactive,password
    ```

Then connect with `ssh sunetid@{{ facts.login_host }}` as usual.

Keep `Host` entries in `~/.ssh/config` specific, like the one above. An entry
that matches too broadly can send connections for other Stanford hosts to the
wrong place.

## Other SSH Clients

The `ssh` command built into macOS, Linux and Windows works for most people.
These clients are alternatives:

| Client | Platforms | Notes |
|---|---|---|
| [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) | Windows | Free. Enter `{{ facts.login_host }}` as the host name and select **Open**. |
| [MobaXterm](https://mobaxterm.mobatek.net/) | Windows | Includes an X server for displaying graphical programs. The Home Edition is free. |
| [SecureCRT](https://uit.stanford.edu/software/scrt_sfx) | Windows, macOS | Licensed by Stanford for its community. |

For graphical programs, a [FarmShare Desktop](start-a-desktop.md) in OnDemand is
usually more reliable than displaying them over SSH.

## Mosh

[Mosh](https://mosh.org/) is an alternative to SSH for macOS and Linux. It logs
in with SSH, then keeps its own connection going, so your session survives
changes of network, and even your laptop going to sleep. It's also more
responsive on slow connections.
