---
tags:
    - ondemand
    - r
---

The RStudio app in OnDemand runs RStudio on a FarmShare compute node, in your
web browser. It uses your FarmShare home directory, so your scripts, data and
installed R packages are the same ones you'd see from a terminal.

**Before you start:** log in to FarmShare once. See [Log In for the First
Time](../get-started/first-login.md).

## Start RStudio

1. Go to [OnDemand]({{ facts.ondemand_url }}) and log in with your SUNet ID.
2. Select **Interactive Apps** > **RStudio**.
3. Fill in the form with the resources and number of hours you need, then
   select **Launch**.
4. When the session under **My Interactive Sessions** is ready, select the
   button on it to open RStudio in a new browser tab.

When you're finished, select **Delete** on the session in **My Interactive
Sessions**. Closing the browser tab doesn't end the session.

## Install Packages

Packages you install go into a personal library in your home directory,
because the shared library isn't writable. `install.packages()` in the RStudio
console works for most packages.

Some packages fail to install from inside RStudio but install from R in a
terminal. If you install from a terminal, use the same version of R that
RStudio uses. R keeps a separate personal library for each minor version,
such as 4.4 and 4.5, so packages installed with a different version won't show
up in RStudio.

To check which version RStudio is running, type this in the RStudio console:

```r
R.version.string
```

Then, in a terminal, run `module spider r` to see which R versions are
installed, and load the one that matches before you start R. [R](../software/r.md)
has more on packages and project environments.

## Things to Know

The version of R in RStudio is set by the app, and it can differ from the
default you get with `module load r`.

An RStudio session can run for up to {{ facts.interactive_max_runtime }}, and
it gets only the cores and memory you asked for. For long analyses that don't
need you to watch them, write an R script and run it as a [batch
job](batch-jobs.md).

Your personal R library counts toward your {{ facts.home_quota }} home quota.

## If Something Goes Wrong

See [OnDemand and Desktops](../fix/ondemand.md), which includes what to do when
R packages won't install in RStudio.
