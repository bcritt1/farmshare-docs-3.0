---
tags:
    - software
---

The Gurobi optimizer is one of the commercial packages installed on FarmShare.
It's provided as the `gurobi` module. If Gurobi reports a license error when you
run it, email {{ facts.support_email }} with "FarmShare" in the subject and
include the message.

## Use Gurobi

Load the module before you run Gurobi, whether from its own command line or from
Python:

```bash
module load gurobi
gurobi_cl model.lp
```

Run `module spider gurobi` to see the installed versions. If you use `gurobipy`
from Python, install the `gurobipy` version that matches the module's Gurobi
version.

In a batch job, put `module load gurobi` in the script before the command that
runs Gurobi. See [Submit a Batch Job](../../use/batch-jobs.md).

## Things to Know

Don't use a free academic license tied to your own computer. Those licenses
check which computer they're running on, and your jobs run on different
FarmShare nodes each time, so they fail with a host ID error.
