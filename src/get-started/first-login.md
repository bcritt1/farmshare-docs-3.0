---
tags:
    - getting-started
    - ssh
    - ondemand
---

You can use FarmShare from a terminal, by connecting with SSH, or from a web
browser, through [OnDemand]({{ facts.ondemand_url }}). Either way, you log in
with your SUNet ID, your SUNet password, and Duo two-step authentication.

The first time you log in, FarmShare finishes setting up your account. Until
that happens, you can't start OnDemand apps or submit jobs, so log in once using
one of the methods below before you do anything else.

## Log In From a Terminal

Macs and Linux computers have a terminal application built in. On Windows, use
PowerShell or Windows Terminal, or the [Windows Subsystem for
Linux](https://learn.microsoft.com/en-us/windows/wsl/about) if you have it set
up.

1. Open your terminal.
2. Type the following, replacing `sunetid` with your own SUNet ID, and press
   ++enter++:

    ```sh
    ssh sunetid@{{ facts.login_host }}
    ```

3. Enter your SUNet password when asked. The terminal doesn't show anything as
   you type it.
4. Choose a Duo option, for example `1` for a Duo Push, and approve it on your
   phone.

When it works, you see a welcome message and a prompt like this:

```text
sunetid@rice-01:~$
```

You're now on one of FarmShare's login nodes. The name `{{ facts.login_host }}`
picks whichever login node is least busy, so you won't always land on the same
one. To log out, type `exit`.

SSH keys don't work on FarmShare. Every login needs your password, or a Kerberos
ticket (see [Set Up SSH](../use/ssh-setup.md)), plus Duo.

### The First-Time Host Key Question

The first time you connect, SSH asks whether you trust the server:

```text
ED25519 key fingerprint is {{ facts.host_key_ed25519 }}.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Check that the fingerprint matches one of FarmShare's:

- `{{ facts.host_key_ed25519 }}` (ED25519)
- `{{ facts.host_key_rsa }}` (RSA)

If it matches, type `yes`. SSH remembers the answer and won't ask again. If it
doesn't match, don't connect, and [contact us](../fix/get-help.md).

## Log In From a Web Browser

1. Go to [OnDemand]({{ facts.ondemand_url }}).
2. Log in with your SUNet ID, password and Duo.
3. If this is your first time using FarmShare, select **Clusters** >
   **FarmShare Shell Access**. A terminal opens in a new tab. That completes
   your account setup, and you can close the tab.

From the OnDemand dashboard you can start a desktop, JupyterLab, RStudio, MATLAB
or VS Code, and browse your files.

If an OnDemand app fails with
`Invalid account or account/partition combination`, your first login hasn't
happened yet. Do step 3 and try again.

## Next Steps

- [Run your first job](first-job.md)
- [Start a desktop](../use/start-a-desktop.md)
- [Where to put your files](where-to-put-files.md)
