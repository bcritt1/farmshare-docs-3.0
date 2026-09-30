---
tags:
    - software
    - containers
---

A container bundles a program with everything it needs to run, so it works the
same way on FarmShare as on the computer where it was built. FarmShare has two
container tools: Apptainer, which is the usual choice for jobs, and Podman,
which works like Docker. Docker itself isn't available.

## Apptainer

Load the module, then pull an image from a registry such as [Docker
Hub](https://hub.docker.com/):

```bash
module load apptainer
apptainer pull docker://ubuntu:24.04
```

This creates an image file, `ubuntu_24.04.sif`, in the current directory. Run
commands inside it with `apptainer exec`:

```bash
apptainer exec ubuntu_24.04.sif cat /etc/os-release
```

| Command | What it does |
|---|---|
| `apptainer pull` | Downloads an image from a registry and saves it as a `.sif` file |
| `apptainer run` | Runs the image's default command |
| `apptainer exec` | Runs a command you choose inside the image |
| `apptainer shell` | Opens an interactive shell inside the image |

In a batch job, load the module and call `apptainer exec` in the script.
Apptainer was formerly called Singularity, and most Singularity instructions
still work.

## Podman

Podman uses the same commands as Docker, so instructions written for Docker
usually work if you replace `docker` with `podman`:

```bash
podman run --rm docker.io/library/ubuntu:24.04 cat /etc/os-release
```

## Things to Know

Container images are large. Keep `.sif` files in your scratch directory
(`{{ facts.scratch_path }}`) rather than your home directory, and keep a copy of
any image you can't download again, since scratch files are cleared out after
{{ facts.purge_days }} days without changes.

To share an image with a class, instructors can ask us to put it in the class
directory. See [Set Up a Course](../teaching/set-up-a-course.md).

## If Something Goes Wrong

See [Software and Modules](../fix/software.md).
