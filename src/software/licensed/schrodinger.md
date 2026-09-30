---
tags:
    - software
---

The Schrödinger suite, including Maestro, is licensed on FarmShare and comes
from the `schrodinger` module. Run Maestro in a FarmShare Desktop.

## Start Maestro

**Before you start:** start a FarmShare Desktop in
[OnDemand]({{ facts.ondemand_url }}). See [Run GUI
Programs](../../use/gui-programs.md).

Open a terminal in the desktop and run:

```bash
module load schrodinger
maestro &
```

Run `module spider schrodinger` to see the installed versions. Some Schrödinger
tools can use GPUs. See [Use GPUs](../../use/gpus.md) for how to get one.

## Things to Know

Jobs you start from Maestro in a desktop stop when the desktop session ends.
Choose a session length that covers them.

If a tool reports that the license doesn't include it, or that no license is
available, email {{ facts.support_email }} with "FarmShare" in the subject and
include the tool's name and the message.
