---
tags:
    - ondemand
    - python
---

The JupyterLab app in OnDemand runs Jupyter notebooks on a FarmShare compute
node, in your web browser. Your notebooks and data are in your FarmShare home
and scratch directories, so nothing needs to be copied to your own computer.

**Before you start:** log in to FarmShare once. See [Log In for the First
Time](../get-started/first-login.md).

## Start JupyterLab

1. Go to [OnDemand]({{ facts.ondemand_url }}) and log in with your SUNet ID.
2. Select **Interactive Apps** > **JupyterLab**.
3. Fill in the form with the resources and number of hours you need, then select
   **Launch**.
4. When the session under **My Interactive Sessions** is ready, select the
   button on it to open JupyterLab in a new browser tab.

When you're finished, select **Delete** on the session in
**My Interactive Sessions**. Closing the browser tab doesn't end the session.

## Use Your Own Python Packages

To use packages you've installed yourself, put them in a virtual environment and
install that environment as a Jupyter kernel. It then appears in JupyterLab's
list of kernels.
[Python](../software/python.md#use-an-environment-in-jupyterlab) has the
commands.

Each kernel you add is a separate environment in your home directory, and
environments count toward your {{ facts.home_quota }} home quota. Delete ones
you no longer use.

## Things to Know

A JupyterLab session can run for up to {{ facts.interactive_max_runtime }}. It
gets only the cores and memory you asked for, so a notebook that needs more has
to be restarted in a bigger session. Long computations that don't need you to
watch them are better as a [batch job](batch-jobs.md), which keeps running after
you close your browser.

AFS isn't available in JupyterLab sessions. Copy anything you need from AFS to
your home or scratch directory first. See [Use AFS](afs.md).

If you're teaching with JupyterLab, test the app with your course's environment
well before class, and tell us early if anything fails. See [Get Ready for Class
Day](../teaching/class-day.md).

## If Something Goes Wrong

See [OnDemand and Desktops](../fix/ondemand.md).
