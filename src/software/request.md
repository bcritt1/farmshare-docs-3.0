---
tags:
    - software
---

If software you need isn't on FarmShare, we may be able to install it. We add
software that's useful to many people, either as a module or as a system
package. For something only you need, it's usually faster to [install it
yourself](install-yourself.md).

## Check First

Search the modules before you ask:

```bash
module spider <name>
```

Some software is installed as part of the operating system and isn't a module.
Try running the command directly, or check with `which <name>`.

## Ask Us

Email {{ facts.support_email }} with "FarmShare" in the subject, and include:

1. The name of the software and a link to its website.
2. The version you need, if it matters.
3. What you're using it for, such as a course or a research project.
4. Whether it needs a license.

## Software for a Course

Instructors who need software for a class should ask well before the quarter
starts, since installing and testing takes time. Include the course number and
roughly how many students will use it. See [Request Course Software or Reserved
Nodes](../teaching/course-software-and-reservations.md).

## Licensed Software

Some commercial software, such as MATLAB, Gaussian, Stata and Ansys, is already
licensed on FarmShare. See [Licensed Software](licensed/index.md) for what's
available and how to use it. For software that isn't licensed yet, include who
is paying for the license in your request.
