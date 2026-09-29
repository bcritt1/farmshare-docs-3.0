---
title: OnDemand and desktops
tags: [troubleshooting, ondemand]
---

# OnDemand and desktops

This page covers common problems with [OnDemand]({{ facts.ondemand_url }}) sessions: desktops, JupyterLab, RStudio, MATLAB and VS Code.

!!! note "Outages"
    If sessions are failing for everyone, FarmShare may be down. Outages and maintenance are announced in {{ facts.announce_channel }} on the [SRCC Slack](https://srcc.slack.com/).

## My session says "Completed" right after I launch it

Your session started and then stopped immediately. Most of the time this happens because your home directory is full. OnDemand writes a few small files to your home directory every time a session starts, and when there's no room, the session can't start.

Check how much space you're using. The Files menu in OnDemand may not work while your home directory is full, so connect with SSH instead:

```sh
ssh SUNetID@{{ facts.login_host }}
du -sh ~
```

We give everyone {{ facts.home_quota }} of home space, which `du` shows as `{{ facts.home_quota_du }}`. If you're close to that, see [Check and free up space](../use/free-up-space.md) to find what's taking it up. Caches from pip, conda and similar tools are the usual culprits, and they're safe to delete:

```sh
rm -rf ~/.cache/*
```

If your home directory isn't full and this is your first time using FarmShare, see the next problem.

## `Invalid account or account/partition combination`

Your FarmShare account hasn't been fully set up yet. The part of your account that lets you run sessions and jobs is created the first time you log in to a login node, and OnDemand doesn't do that for you.

To fix it, open [OnDemand]({{ facts.ondemand_url }}) and select **Clusters** > **FarmShare Shell Access**. Once the terminal opens, you're done; you can close it. Then start your session again.

Logging in once with `ssh SUNetID@{{ facts.login_host }}` does the same thing.

## My desktop is stuck on "Connecting", or noVNC says it can't connect

This usually means something went wrong on our side, often during an outage or right after maintenance. Check {{ facts.announce_channel }} for news.

If there's no outage, delete the session and start a new one. In OnDemand, go to **My Interactive Sessions** and select **Delete** on the stuck session. Anything unsaved in that session is lost, but files you saved to your home or scratch directory are still there.

## My password won't unlock the desktop

The desktop locks itself after it's been idle for a while, and it unlocks with your SUNet password. Sometimes it rejects the password even when you type it correctly. Characters can get changed on the way from your keyboard, through your browser, to the remote desktop.

Try typing the password again, slowly. If that doesn't work, paste it in instead:

1. Open the drawer on the left edge of the desktop window and select the clipboard icon.
2. Paste your password into the text box there, then close the drawer.
3. Click in the password field on the desktop and press ++ctrl+shift+v++.

If you still can't get in, you can delete the session from **My Interactive Sessions** and start a new one, but anything unsaved in it is lost. If there's work in that session you need, [ask us](get-help.md) before you delete it. We can unlock a running session for you.

To keep it from happening, you can turn the lock off in each new desktop. Open **Applications** > **Settings** > **Xfce Screensaver**, go to the **Lock Screen** tab, and turn off **Enable Lock Screen**. If you do, lock your own computer when you step away, because anyone using your browser could get into the session.

## My session is waiting in the queue

Desktops and other OnDemand sessions share the same pool of compute nodes as everyone else's interactive work. When those nodes are busy, your session waits until there's room. It's busiest in the weeks before exams and near assignment deadlines.

Smaller sessions start sooner, so if you don't need a Large or Very Large desktop, choose a smaller size. You can also leave the request in the queue and ask OnDemand to email you when it starts.

## I can't start a second desktop

You can run one desktop of each type at a time. A second FarmShare Desktop won't start while the first is still running. To switch, delete the running session from **My Interactive Sessions** first.

## My session ended before my work finished

Interactive sessions run for up to {{ facts.interactive_max_runtime }}. We usually can't extend a session once it's running. Keeping sessions time-limited is how everyone gets a turn on the interactive nodes.

If your work takes longer than that, or doesn't need you to watch it, run it as a [batch job](../use/batch-jobs.md) instead. Batch jobs keep running when you close your browser, and they can run for up to {{ facts.max_runtime }}, or {{ facts.long_max_runtime }} with the `long` option.

If your session seemed to end but you were only away for a while, it may still be running behind the screen lock. See [My password won't unlock the desktop](#my-password-wont-unlock-the-desktop).

## `No space left on device`

Your home directory is full. It's the same cause as sessions that stop right after launch. See [My session says "Completed" right after I launch it](#my-session-says-completed-right-after-i-launch-it).

## R packages won't install in RStudio

Some R packages fail to install from inside RStudio even though they install fine from a terminal. Install them from an R console in a terminal instead:

```sh
ml r
R
```

```r
install.packages("packagename")
```

The packages go into your personal library, so RStudio can load them afterward. Some packages also need system libraries that only we can install. If the install error mentions a missing library, [ask us](get-help.md) and include the package name and the full error.

## Still stuck

[Get help](get-help.md) explains what to send us so we can sort it out quickly. Include the session type, the time it failed, and any error text, copied as text rather than a screenshot.
