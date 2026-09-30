---
tags:
    - software
    - modules
---

Software on FarmShare comes from two places. Common tools are installed as part
of the operating system and work as soon as you log in. Specialized and newer
software is provided as modules, which you load when you need them.

## Software That's Already There

The operating system, {{ facts.os }}, includes many standard tools. Run them
directly:

```bash
python3 --version
```

```text
Python {{ facts.python_system_version }}
```

## Load a Module

Modules give you software that isn't in the operating system, or a newer or
specially built version of something that is. Loading a module sets up your
environment so the software is found:

```bash
module load python
python3 --version
```

```text
Python {{ facts.python_module_version }}
```

Loading a module only affects your current session. In a batch job, load the
modules the job needs inside the script.

`ml` is a shorter way to type `module`. `ml python` does the same thing as
`module load python`.

## Find Software

To list every module, run:

```bash
module avail
```

To search for a module by name, use `module spider`. It also finds modules that
`module avail` doesn't show until something else is loaded:

```bash
module spider cuda
```

To search module names and descriptions for a word, use `module keyword`:

```bash
module keyword chemistry
```

Some modules have more than one version. Without a version, `module load` picks
the default. To choose one, name it, for example
`module load {{ facts.cuda_module }}`.

## Letters in `module avail`

| Letter | Meaning |
|---|---|
| `D` | The default version, loaded when you don't name one |
| `L` | Currently loaded |
| `g` | Built for GPUs; use it in jobs on the GPU nodes |
| `S` | Sticky; `module purge` leaves it loaded unless you add `--force` |

## Module Commands

| Command | Short form | What it does |
|---|---|---|
| `module avail` | `ml av` | Lists available software |
| `module spider <name>` | `ml spider <name>` | Searches for software by name |
| `module keyword <word>` | `ml key <word>` | Searches names and descriptions |
| `module whatis <name>` | `ml whatis <name>` | Shows a short description |
| `module help <name>` | `ml help <name>` | Shows help for a module |
| `module load <name>` | `ml <name>` | Loads a module |
| `module unload <name>` | `ml -<name>` | Unloads a module |
| `module list` | `ml` | Lists loaded modules |
| `module purge` | `ml purge` | Unloads all modules |
| `module save <set>` | `ml save <set>` | Saves the loaded modules as a named set |
| `module restore <set>` | `ml restore <set>` | Loads a saved set |

FarmShare uses Lmod. Its [user
guide](https://lmod.readthedocs.io/en/latest/010_user.html) covers the rest.

## If It Isn't Here

You can [install software yourself](install-yourself.md), or [ask us to add
it](request.md).
