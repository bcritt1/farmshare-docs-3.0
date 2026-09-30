---
tags:
    - software
---

You can install your own software on FarmShare, in your home directory or in a
class or group directory. You can't install system packages with `sudo` or
`apt`. If you need one, [ask us](request.md).

## Use a Package Manager

A package manager is usually the easiest way to install software without
administrator rights:

| Package manager | Good for |
|---|---|
| [uv](https://docs.astral.sh/uv/) | Python packages. See [Python](python.md). |
| [Pixi](https://pixi.prefix.dev/latest/) or [Micromamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html) | Anything on conda-forge, including libraries other packages depend on. See [Conda-Style Environments](conda-style-environments.md). |
| [Spack](https://spack.readthedocs.io/en/latest/) | Scientific and HPC software built from source |

## Build from Source

Most software that builds with `./configure` and `make`, or with CMake, can be
installed in your home directory by setting the install location:

```bash
./configure --prefix=$HOME/software/myprogram
make
make install
```

Then add its `bin` folder to your path, for example in `~/.bashrc`:

```bash
export PATH=$HOME/software/myprogram/bin:$PATH
```

Compilers and build tools are available as modules. See [Find Installed
Software](modules.md).

## Software for a Class or Group

Classes and groups can install shared software in their own directories, so
everyone uses the same copy. See [Set Up a
Course](../teaching/set-up-a-course.md) for getting a class directory. For
software many classes use, ask us to install it as a module instead.

## Things to Know

Software you install counts toward the quota of the directory it's in, and your
home directory holds {{ facts.home_quota }}. Programs with a graphical interface
need a [desktop session](../use/start-a-desktop.md) to run.

If a program needs Docker, see [Containers](containers.md).
