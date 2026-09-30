---
tags:
    - teaching
    - software
---

If your course needs software that isn't on FarmShare, or guaranteed capacity
for an assignment, the instructor can ask us to install the software or reserve
nodes or GPUs for the class. Both take longer to arrange than a course
directory, so ask as early as you can, before the quarter starts.

**Before you start:** check what's already installed with `module spider
<name>`. See [Find Installed Software](../software/modules.md).

## Course Software

We can install software for a course in one of these ways:

| Option | Good for |
|---|---|
| A module | Software other courses or researchers might also use. Everyone loads it with `module load`. |
| An install in the course directory | Software only your course needs, or a specific version. Your course staff can also install it there themselves. See [Install Software Yourself](../software/install-yourself.md). |
| A shared container | A complete environment with many packages, set up once and used by every student in the same way. See [Containers](../software/containers.md). |

Programs with a graphical interface run in a [FarmShare
Desktop](../use/start-a-desktop.md) in OnDemand. Students open a terminal in the
desktop, load the module and start the program.

<!-- NEEDS REVIEW: When course software isn't licensed yet, is "tell us what
license your department has or who is paying" the right process? -->

For commercial software, check [Licensed
Software](../software/licensed/index.md) first. If what you need isn't licensed
on FarmShare yet, tell us what license your department has or who is paying for
one.

## Reserved Nodes and GPUs

<!-- NEEDS REVIEW: What window can a class reservation cover, and how much lead
time does it need? -->

For an assignment, exam or competition that has to run at a set time, we can
hold some of FarmShare's nodes or GPUs for your class. A reservation covers a
specific window, such as the week or two of an assignment, and while it lasts
the reserved resources are kept for your students.

FarmShare has {{ facts.gpu_nodes * facts.gpus_per_node }} GPUs, shared by
everyone. If your students need GPUs at the same time, especially near the end
of the quarter, a reservation is the most reliable way to make sure they get
them.

<!-- NEEDS REVIEW: What is the class reservation process, and do students use a
reservation by adding its name to their jobs? -->

When a reservation is ready, we'll tell you its name. Students add it to their
jobs, for example in a batch script:

```bash
#SBATCH --reservation=<name>
```

## Ask for Software or a Reservation

Email {{ facts.support_email }} with "FarmShare" and your course number in the
subject, and include:

1. The course number and quarter.
2. For software: its name, a link to its website, the version you need, and
   whether it needs a license.
3. For a reservation: the dates and times, how many students, and what each
   student needs, such as CPUs, memory or GPUs.
4. Roughly how many students will use it at once.

## Things to Know

Test the software on FarmShare yourself, the way your students will use it,
before the first assignment that needs it. Problems are much easier for us to
fix before a deadline than during one.

If you're not sure whether FarmShare can handle the whole class working at once,
ask us. We can tell you what to expect and which desktop size or job settings to
recommend to students. See also [Get Ready for Class Day](class-day.md).
