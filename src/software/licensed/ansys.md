---
tags:
    - software
---

Ansys is licensed on FarmShare for coursework and unsponsored research. The
`ansys` module includes the Ansys Electronics Desktop, which contains HFSS. Run
it in a FarmShare Desktop.

## Start the Electronics Desktop

**Before you start:** start a FarmShare Desktop in
[OnDemand]({{ facts.ondemand_url }}). See [Run GUI
Programs](../../use/gui-programs.md).

Open a terminal in the desktop and run:

```bash
module load ansys
ansysedt &
```

The `&` lets you keep using the terminal while the Electronics Desktop is open.
HFSS is in the Electronics Desktop's project menus.

To see which Ansys versions are installed, run `module spider ansys`. To see
what else the module provides, run `module help ansys`.

## Things to Know

The Electronics Desktop runs inside your desktop session, and so do the
simulations you start from it. When the session ends, they stop. Choose a
session length that covers the simulation, and save your project before the
session runs out.

If you're using Ansys for sponsored research, use your group's own license on
[Sherlock](../../resources/sherlock.md) instead.

### Teaching with Ansys

For a class tutorial, have each student start their own FarmShare Desktop and
run Ansys there. Don't have a whole class run it from the **FarmShare Shell
Access** terminal in OnDemand. That terminal always opens on the same login
node, and fifty copies of Ansys on one login node run slowly for everyone.

Mention Ansys in your course setup request so we can check it before the class.
See [Request Course Software or Reserved
Nodes](../../teaching/course-software-and-reservations.md).

## The Electronics Desktop Crashes When I Save a Project

The Electronics Desktop has had trouble saving projects to network file systems,
which include your home directory. When this happens, it crashes with an error
like `Aborted (core dumped)`, sometimes after `Path is too long`.

To work around it, set the project directory to a folder in `/tmp`, which is on
the node's own disk. In the Electronics Desktop, go to **Tools** > **Options** >
**General Options** > **General** > **Directories** and set the project
directory to `/tmp/$USER` (with your SUNet ID in place of `$USER`).

`/tmp` is on the node your desktop runs on, and it's deleted when the session
ends. Before the session ends, copy your project to your home or scratch
directory:

```bash
cp -r /tmp/$USER/myproject ~/
```

If the crash happens somewhere other than saving, [tell us](../../fix/get-help.md)
what you were doing when it crashed.
