---
tags:
    - ondemand
    - vs-code
---

The VS Code app in OnDemand runs the VS Code editor on a FarmShare compute
node, in your web browser. It's the supported way to use VS Code with
FarmShare, and it needs nothing installed on your own computer.

**Before you start:** log in to FarmShare once. See [Log In for the First
Time](../get-started/first-login.md).

## Start VS Code

1. Go to [OnDemand]({{ facts.ondemand_url }}) and log in with your SUNet ID.
2. Select **Interactive Apps** > **VS Code**.
3. Fill in the form with the resources and number of hours you need, then
   select **Launch**.
4. When the session under **My Interactive Sessions** is ready, select the
   button on it to open VS Code in a new browser tab.

The built-in terminal in VS Code is a shell on the same compute node, where you
can load modules and run your code.

When you're finished, select **Delete** on the session in **My Interactive
Sessions**. Closing the browser tab doesn't end the session.

## Remote-SSH from Your Own Computer

We don't support connecting the VS Code app on your own computer to FarmShare
with the Remote-SSH extension, or editors built on it such as Cursor. It isn't
blocked at the moment, but that may change, and we can't troubleshoot it for
you.

Remote-SSH copies its own server program into your home directory and runs it
on a login node, and each connection it opens has to get through Duo. When
something in that chain fails, such as a Duo prompt the extension doesn't show
you or a full home directory, the connection tends to hang rather than give a
clear error. The OnDemand app doesn't depend on any of that, and your code
runs on a compute node with the resources you asked for rather than on a shared
login node.

## Things to Know

A VS Code session can run for up to {{ facts.interactive_max_runtime }}, and
it gets only the cores and memory you asked for. For work that runs longer, or
doesn't need you to watch it, use a [batch job](batch-jobs.md).

VS Code extensions you install are saved in your home directory and count
toward your {{ facts.home_quota }} home quota.

AFS isn't available in VS Code sessions. See [Use AFS](afs.md).

## If Something Goes Wrong

See [OnDemand and Desktops](../fix/ondemand.md).
