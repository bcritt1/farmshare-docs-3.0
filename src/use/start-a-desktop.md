---
tags:
    - ondemand
    - desktop
---

A FarmShare Desktop is a Linux desktop that runs on a FarmShare compute node and
opens in your web browser. Use it for programs that need a graphical interface,
or when you want a terminal and a file browser side by side.

**Before you start:** log in to FarmShare once. See [Log In for the First
Time](../get-started/first-login.md).

## Start the Desktop

1. Go to [OnDemand]({{ facts.ondemand_url }}) and log in with your SUNet ID.
2. Select **Interactive Apps** > **FarmShare Desktop**.
3. Choose a size and the number of hours you want. Larger sizes get more CPU
   cores and memory. For example, Large has 8 cores and Very Large has 16.
4. If you want an email when the desktop is ready, select the email option.
5. Select **Launch**.

The session appears under **My Interactive Sessions**. When it's ready, select
the button on the session to open the desktop in a new browser tab.

If you're in an EE course that uses Caddyshack, start a Caddyshack Desktop
instead. See [Use Caddyshack for EE Courses](caddyshack.md).

## Work in the Desktop

The desktop runs on a compute node, not a login node. It has the same software
and the same home and scratch directories as the login nodes, so you can open a
terminal and use `module load` there as usual. AFS is the exception: it isn't
available in a desktop. See [Use AFS](afs.md).

To run a program with a graphical interface, see [Run GUI
Programs](gui-programs.md).

You can close the browser tab without ending the session. The desktop keeps
running, and you can reopen it from **My Interactive Sessions**. When you're
finished, select **Delete** on the session to end it and free its cores for
other people.

## Things to Know

A desktop can run for up to {{ facts.interactive_max_runtime }}, and it ends
when the hours you asked for run out. Save your work to your home or scratch
directory as you go, because anything unsaved is lost when the session ends.

A desktop gets only the cores and memory of the size you chose, not the whole
node. For work that needs more, or that runs longer than a day, use a [batch
job](batch-jobs.md).

You can run one FarmShare Desktop at a time. Desktops share compute nodes with
everyone else's interactive work, so when FarmShare is busy your session may
wait in the queue before it starts. Smaller sizes usually start sooner. To see
how busy FarmShare is before you launch, select **Clusters** > **System Status**
in OnDemand.

The desktop locks itself after it's been idle for a while. It unlocks with your
SUNet password.

## If Something Goes Wrong

See [OnDemand and Desktops](../fix/ondemand.md) for sessions that won't start,
won't connect, won't unlock or end early.
