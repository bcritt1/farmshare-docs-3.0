---
tags:
    - software
---

Stanford licenses several commercial programs for use on FarmShare. You don't
need to buy or activate anything yourself. Load the program's module and it
finds the license on its own.

## What's Licensed

| Software | Module | Usually run | Page |
|---|---|---|---|
| MATLAB | `matlab` | OnDemand MATLAB app, or batch jobs | [MATLAB](matlab.md) |
| Gaussian and GaussView | `gaussian` | GaussView in a desktop, Gaussian in batch jobs | [Gaussian and GaussView](gaussian.md) |
| Stata | `stata` | Interactive session or batch jobs | [Stata](stata.md) |
| Ansys, including HFSS | `ansys` | FarmShare Desktop | [Ansys and HFSS](ansys.md) |
| SAS | `sas` | Batch jobs | [SAS](sas.md) |
| Mathematica | `mathematica` | Desktop, or scripts in batch jobs | [Mathematica](mathematica.md) |
| Gurobi | `gurobi` | Batch jobs | [Gurobi](gurobi.md) |
| Schrödinger | `schrodinger` | Desktop | [Schrödinger](schrodinger.md) |
| Sentaurus | Provided by EE | Caddyshack Desktop | [Sentaurus](sentaurus.md) |

Versions change when licenses are renewed. To see which versions are installed
now, run `module spider` with the module name:

```bash
module spider matlab
```

## Who Can Use It

Anyone with a FarmShare account can use the licensed software, for the same work
FarmShare is for: coursework and unsponsored research. If your research is
sponsored, use [Sherlock](../../resources/sherlock.md) instead. Sentaurus is the
exception. It's licensed and supported by Electrical Engineering, not by us.

Licenses are shared by everyone on FarmShare, and some allow only a limited
number of people to run the program at once. If a program says it can't get a
license, the licenses may all be in use. Try again a little later, and if it
keeps happening, [let us know](../../fix/get-help.md).

## Programs with a Graphical Interface

Programs with a graphical interface, such as GaussView or the Ansys Electronics
Desktop, run in a FarmShare Desktop. Start a desktop in OnDemand, open a
terminal in it, load the module and start the program. See [Run GUI
Programs](../../use/gui-programs.md).

Everything you start in a desktop stops when the desktop session ends, including
calculations that are still running. For long calculations, submit a [batch
job](../../use/batch-jobs.md) instead.

## Licensed Software for a Course

If your course needs one of these packages, say so when you ask for your course
setup, so we can check that it's installed and working before the quarter
starts. If the course needs software that isn't licensed on FarmShare yet, ask
as early as you can and say who will pay for the license. A new license takes
much longer to arrange than installing free software. See [Request Course
Software or Reserved Nodes](../../teaching/course-software-and-reservations.md).

For other software, see [Request Software](../request.md).
