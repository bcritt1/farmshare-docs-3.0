---
tags:
    - reference
---

These are terms you'll meet in the FarmShare docs, with what they mean on
FarmShare.

AFS :   An older Stanford file system that some courses and personal web sites
still
    use. On FarmShare it's only available on the login nodes. See [Use
    AFS](../use/afs.md).

Batch job :   A job that runs a script without you watching it, and keeps
running after
    you log out. See [Submit a Batch Job](../use/batch-jobs.md).

Caddyshack Desktop :   An OnDemand desktop with Electrical Engineering course
software. It runs on
    its own `caddyshack` partition, and you can have one running at a time. See
    [Use Caddyshack for EE Courses](../use/caddyshack.md).

Class directory :   A shared directory for a course, at
`/home/classes/<dept>/<number>`. The
    instructor asks for it, and course staff manage its files. See [Set Up a
    Course](../teaching/set-up-a-course.md).

Compute node :   A computer in FarmShare that runs jobs. You get time on one
through the
    scheduler, by submitting a job or starting an OnDemand app. You can SSH to a
    compute node only while you have a job running on it. See [SSH to a Compute
    Node](../use/ssh-compute-node.md).

Data transfer node :   A server for moving files to and from FarmShare, at
`{{ facts.dtn_host }}`.
    See [Move Files to and from FarmShare](../use/transfer.md).

Duo :   Stanford's two-step authentication. Every FarmShare login needs a Duo
    approval.

FarmShare Desktop :   A Linux desktop that runs on a compute node and opens in
your browser
    through OnDemand. Use it for programs with a graphical interface. See [Start
    a Desktop](../use/start-a-desktop.md).

Globus :   A web service for transferring files. FarmShare's Globus endpoint is
called
    "{{ facts.globus_endpoint }}". See [Move Files to and from
    FarmShare](../use/transfer.md).

Home directory :   Your personal directory, `/home/users/<SUNet ID>`, for code,
scripts and
    files you want to keep. It holds {{ facts.home_quota }} and is available on
    every node.

Interactive session :   A job that gives you a shell on a compute node, so you
can work there
    directly. See [Get an Interactive Session](../use/interactive-sessions.md).

Job :   Work you ask the scheduler to run on a compute node, with the CPUs,
memory
    and time you request.

Kerberos :   Stanford's authentication system. A Kerberos ticket can log you in
to
    FarmShare without typing your password, and it gives you access to AFS.

Login node :   The computers you land on when you connect with SSH, named
`rice`. Use them
    to edit files, install software and submit jobs.

Module :   A way of loading software that isn't part of the operating system.
Run
    `module load <name>` to use it. See [Find Installed
    Software](../software/modules.md).

OnDemand :   FarmShare's web portal, at
[{{ facts.ondemand_url }}]({{ facts.ondemand_url }}).
    It has desktops, JupyterLab, RStudio, MATLAB, VS Code, a file browser and a
    terminal.

Partition :   A group of compute nodes that a job can run on, such as `normal`,
`bigmem`
    or `gpu`. Choose one with `--partition`. See [Limits](limits.md).

Purge :   The regular clearing of your scratch directory. Files that haven't
changed
    in {{ facts.purge_days }} days are deleted.

QoS :   Short for "quality of service". A set of limits on your jobs, such as
how
    long they can run and how many CPUs they can use at once. Choose one with
    `--qos`. See [Limits](limits.md).

Scratch directory :   Your directory for large working data, at
`{{ facts.scratch_path }}`. It has
    no size limit and isn't backed up, and files there are purged after
    {{ facts.purge_days }} days without changes.

Slurm :   The scheduler FarmShare uses to decide when and where jobs run.
Commands
    such as `sbatch`, `srun` and `squeue` are part of Slurm.

SUNet ID :   Your Stanford username. You need a full-service SUNet ID to use
FarmShare.

Workgroup :   A Stanford group of people, managed in [Workgroup
    Manager](https://workgroup.stanford.edu). Each course on FarmShare has a
    staff workgroup, whose members can change the class directory's files, and a
    student workgroup that lists the class. See [Set Up a
    Course](../teaching/set-up-a-course.md).
