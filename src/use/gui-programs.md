---
tags:
    - ondemand
    - desktop
    - software
---

Programs with a graphical interface, such as GaussView, ParaView or Ansys, run
on FarmShare inside a FarmShare Desktop. You start them from a terminal in the
desktop, the same way you'd start any other program.

**Before you start:** start a desktop. See [Start a
Desktop](start-a-desktop.md).

## Run a Program in a Desktop

1. In the desktop, open a terminal from the **Applications** menu.
2. Load the program's module. For example, for ParaView:

    ```bash
    module load paraview
    ```

    If you're not sure of the module's name, search for it with
    `module spider`, for example `module spider gaussview`.

3. Run the program by name:

    ```bash
    paraview &
    ```

    The `&` runs the program in the background, so you can keep using the
    terminal. Keep the terminal open while the program runs.

The program's window opens on the desktop. It uses the cores and memory of the
desktop size you chose, so pick a size that fits the program. For heavy
calculations, you can often set up the input in the graphical program and run
the calculation itself as a [batch job](batch-jobs.md).

MATLAB also has its own app in OnDemand, under **Interactive Apps**. See
[MATLAB](../software/licensed/matlab.md). For other licensed programs, such as
[Gaussian and GaussView](../software/licensed/gaussian.md) or [Ansys and
HFSS](../software/licensed/ansys.md), see their pages for who can use them and
how they're set up.

## Displaying Programs over SSH

You can also display a program on your own computer over SSH with X11
forwarding, by connecting with `ssh -X` and running the program on a login
node. This needs an X server on your computer, such as XQuartz on macOS or
MobaXterm on Windows. It's slower than a desktop and less reliable, so we
recommend a FarmShare Desktop instead.

## If Something Goes Wrong

For problems with the desktop itself, see [OnDemand and
Desktops](../fix/ondemand.md). If a module won't load or a program won't
start, see [Software and Modules](../fix/software.md).
