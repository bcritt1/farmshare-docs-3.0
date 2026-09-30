---
tags:
    - troubleshooting
    - software
    - modules
---

The problems below come up when finding, loading and installing software on
FarmShare. Problems specific to R in RStudio are also covered on [OnDemand and
Desktops](ondemand.md).

## The Software I Need Isn't Installed

Search the module tree first. `module spider` finds modules that `module avail`
doesn't list until something else is loaded:

```bash
module spider <name>
```

If it isn't there, you can often [install it
yourself](../software/install-yourself.md) with uv, Pixi, Micromamba or Spack.
If it's general-purpose software that other people would use too, or it needs to
be installed system-wide, [ask us to add it](../software/request.md). We install
most open-source software on request.

For a course, ask well before the software is needed, so there's time to install
and test it. See [Request Course Software or Reserved
Nodes](../teaching/course-software-and-reservations.md).

## `singularity: command not found` or `apptainer: command not found`

Apptainer, formerly called Singularity, is a module, so it isn't on your path
until you load it:

```bash
module load apptainer
```

In a batch job, put the `module load` line in the script before the `apptainer`
or `singularity` command. See [Containers](../software/containers.md).

## `module: command not found`

The `module` command is set up when your shell starts on a FarmShare node, so it
should be there in every terminal and batch job.

It can be missing when a program runs commands through a plain `sh` shell, for
example R's `system()` function. Load the modules you need in the terminal or
job script before you start the program, instead of from inside it.

If `module` is missing in an ordinary terminal, check whether you've changed
`~/.bashrc` or `~/.profile` recently. If you haven't, the node may have a
problem. Run `hostname` and email the node name to {{ facts.support_email }}.

## I Can't Use `sudo` or `apt install`

FarmShare is shared by everyone, so only administrators can install system
packages. [Common Questions](common-questions.md#why-cant-i-use-sudo) explains
why.

Most software can be installed in your home directory without administrator
rights. See [Install Software Yourself](../software/install-yourself.md). If you
need a system package, [ask us](../software/request.md) and include the package
name.

## `No space left on device` While Installing

Your home directory is full. Package managers download to caches in your home
directory, and environments are often large, especially for machine learning.

Check how much space you're using:

```sh
du -sh ~
```

We give everyone {{ facts.home_quota }} of home space. `du` reports sizes in
GiB, so a full home directory shows as about `{{ facts.home_quota_du }}`. Caches
from pip, uv, conda and similar tools are safe to delete:

```sh
rm -rf ~/.cache/*
```

Delete environments you no longer use. [Check and Free Up
Space](../use/free-up-space.md) shows how to find what else is taking up room.

## Apptainer Images Fill My Home Directory

`apptainer pull` saves the image in the current directory, and it keeps a cache
of downloaded layers in your home directory. Pull images from your scratch
directory instead, and clear the cache after pulling:

```bash
cd {{ facts.scratch_path }}
apptainer pull docker://ubuntu:24.04
apptainer cache clean
```

Scratch files that haven't changed in {{ facts.purge_days }} days are deleted,
so keep a copy of any image you can't download again.

## I Want to Use Docker

Docker isn't available on FarmShare. Podman uses the same commands, and
Apptainer can run images from Docker Hub. See
[Containers](../software/containers.md).

## R Packages Won't Install in RStudio

Some R packages fail to install from inside RStudio even though they install
fine from a terminal. Install them from an R console in a terminal instead:

```sh
ml r
R
```

```r
install.packages("packagename")
```

If the error says a system library is missing, the package depends on code
written in another language, such as C. You can install those libraries with
Pixi or Micromamba (see
[R](../software/r.md#packages-that-need-system-libraries)), or [ask
us](../software/request.md) to install the library, with the package name and
the full error.

## RStudio and `module load r` Give Different Versions of R

The RStudio app in OnDemand and the `r` module are updated separately, so they
may not have the same version. Packages you install for one version of R aren't
available in another, which can make packages seem to disappear.

Check which version you're in by running this in R:

```r
R.version.string
```

Install the packages again in whichever version you use.

## A Program I Built Myself Stopped Working

If a program you compiled or installed in your home directory now fails with
`error while loading shared libraries`, it was probably built against system
libraries that changed when FarmShare was upgraded. Rebuild it, or reinstall it
with a package manager. See [What's Changed](../about/whats-changed.md).

## Getting Help

[Get Help](get-help.md) lists what to include in a support request. For software
problems, include the module names and versions you loaded, the command you ran,
and the full error, copied as text.
