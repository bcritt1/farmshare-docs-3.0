# Writing Plan

The full page list for the new FarmShare docs, with the order to write them in.
Stub pages for everything below already exist in `src/`, and the nav in
`mkdocs.yml` follows this list. Write pages to the [style
guide](STYLE-GUIDE.md).

Tier 1 pages cover the problems readers ask support about most often, so they're
written first. Tier 2 completes the main reader paths, and tier 3 is everything
else. The Source column says where to start: **adapt** means the Sherlock docs
page applies with FarmShare names and paths swapped in, **rewrite** means use
the Sherlock page for depth but FarmShare facts throughout, and **new** means
there's no Sherlock equivalent.

## Home

| Page | Purpose | Source | Tier |
|---|---|---|---|
| Home | What FarmShare is and who it's for. A pointer to `#farmshare-announce` for outages. Entry points for class, research, teaching, and coming from Sherlock. | rewrite | 1 |

## Get Started

| Page | Purpose | Source | Tier |
|---|---|---|---|
| Is FarmShare Right for Me? | Eligibility, cost, data risk, what it's not for | new | 2 |
| Log In for the First Time | SSH and OnDemand, Duo, the first login creating your account | rewrite | 1 |
| Run Your First Job | Script, submit, check, find output | rewrite | 2 |
| Where to Put Your Files | Home vs scratch vs `/tmp`, purge, no long-term storage | new | 1 |
| Coming from Sherlock | What's different if you know Sherlock | new | 3 |

## Use FarmShare

| Page | Purpose | Source | Tier |
|---|---|---|---|
| Start a Desktop | FarmShare Desktop, sizes, limits, screen lock | rewrite | 1 |
| Use JupyterLab | | rewrite | 2 |
| Use RStudio | Including package installs | rewrite | 2 |
| Use VS Code | The OnDemand app; Remote-SSH is unsupported | rewrite | 2 |
| Run GUI Programs | MATLAB, GaussView, Ansys and others in a desktop | new | 2 |
| Use Caddyshack for EE Courses | Includes who supports what | new | 2 |
| Submit a Batch Job | | rewrite | 2 |
| Get an Interactive Session | | rewrite | 2 |
| Use GPUs | | rewrite | 2 |
| Run Long or Big-Memory Jobs | | rewrite | 3 |
| Run Many Jobs at Once | Job arrays | adapt | 3 |
| Run Parallel and MPI Jobs | | new | 3 |
| Job Options Reference | | adapt | 3 |
| How Jobs Get Scheduled | | adapt | 3 |
| Check and Free Up Space | | rewrite | 1 |
| Move Files to and from FarmShare | | rewrite | 2 |
| Share Files with a Group | | rewrite | 3 |
| Use AFS | | new | 3 |
| Set Up SSH | Config, Kerberos, fewer Duo prompts | rewrite | 3 |
| SSH to a Compute Node | | new | 3 |
| Use the Login Nodes | | new | 3 |

## Software

| Page | Purpose | Source | Tier |
|---|---|---|---|
| Find Installed Software | Modules | adapt | 2 |
| Request Software | | new | 1 |
| Python | | adapt | 2 |
| R | | adapt | 2 |
| Conda-Style Environments | Micromamba, Pixi | rewrite | 2 |
| Install Software Yourself | No sudo | rewrite | 3 |
| Containers | Apptainer, Podman | rewrite | 3 |
| AI Coding Agents | | rewrite | 3 |
| Licensed Software: Overview | What's licensed, who can use it, requesting for a course | new | 1 |
| MATLAB | | rewrite | 2 |
| Gaussian and GaussView | | new | 1 |
| Stata | | new | 2 |
| Ansys and HFSS | | new | 1 |
| SAS, Mathematica, Gurobi, Schrödinger, Sentaurus | One page each | new / rewrite | 3 |

The final package list should be confirmed with the FarmShare admins.

## Teaching with FarmShare

| Page | Purpose | Source | Tier |
|---|---|---|---|
| Overview and Timeline | What we can do for a course, and when to ask | new | 1 |
| Set Up a Course | Class directory, workgroups | new | 1 |
| Add Students and TAs | | new | 2 |
| Request Course Software or Reserved Nodes | | new | 2 |
| Get Ready for Class Day | | new | 2 |
| Teaching Materials | | new | 3 |

## Fix a Problem

One page per area. Each page lists its problems and gives the solutions.

| Page | Problems it covers | Tier |
|---|---|---|
| OnDemand and Desktops | Session ends right away, stuck connecting, lock screen, queued, second desktop, first-use account error, RStudio installs | 1 |
| Storage and Files | No space left, quota exceeded, `df` confusion, lost old scratch, transfer and WinSCP errors, DTN resets | 1 |
| Logging In | Password or Duo rejected, connection refused, host key warnings, VS Code Remote-SSH disconnects | 1 |
| Jobs | Pending, account errors, time limit, out of memory, stuck in CG, bad nodes | 2 |
| GPUs | Nodes drained, PyTorch can't see the GPU, CUDA versions | 2 |
| Software and Modules | Missing modules, pip/python mismatch, Apptainer errors | 2 |
| AFS | Not visible from jobs or OnDemand, timeouts, re-authenticating | 3 |
| Common Questions | The "why" questions: unlimited storage, no sudo, no extensions, no SSH keys | 2 |
| Get Help | What to send, hours, office hours, Slack (including `#farmshare-announce` for outages) | 1 |

## Reference

| Page | Source | Tier |
|---|---|---|
| Limits: Partitions, QoS, Time and Memory | rewrite. A simplified summary table in the spirit of Sherlock's `sh_part` output (partition, time default and maximum, per-user CPU, memory and GPU limits), without node lists or system detail. | 2 |
| Storage Locations and Quotas | rewrite | 1 |
| Hardware | rewrite | 3 |
| Software List | rewrite | 2 |
| Policies | rewrite | 3 |
| Glossary | adapt | 3 |

## Additional Resources

Services beyond FarmShare, for readers FarmShare won't serve well. Each page
gives the basics, why you'd use it, and how to get access, then links out.
They're not full user guides.

### Other Stanford Research Computing Services

| Page | Why a FarmShare reader would go there | Tier |
|---|---|---|
| Sherlock (Includes Moving to Sherlock) | Sponsored research, bigger jobs, group storage | 2 |
| Oak | Long-term research storage | 3 |
| Nero | GCP-based platform, high-risk data | 3 |
| Carina | High-risk data on-premises | 3 |
| Marlowe | Large-scale AI | 3 |

### Outside Stanford Research Computing

Each of these pages makes clear the service isn't ours.

| Page | Why a FarmShare reader would go there | Tier |
|---|---|---|
| NSF ACCESS | Free national HPC allocations (access-ci.org), including for students | 3 |
| Google Cloud | Stanford GCP, GCP for courses, and consumer GCP accounts | 3 |

## About FarmShare

| Page | Source | Tier |
|---|---|---|
| What's Changed | new | 3 |
| Supporting FarmShare | rewrite | 3 |
