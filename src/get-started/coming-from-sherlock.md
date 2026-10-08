---
tags:
    - getting-started
    - sherlock
---

If you've used Sherlock, most of FarmShare will be familiar: both use Slurm and
Lmod modules, and you log in the same way. The table lists the differences
you're most likely to run into.

## What's Different

| Topic | Sherlock | FarmShare |
|---|---|---|
| What it's for | Sponsored and departmental research. Not for coursework. | Coursework and unsponsored research. Not for sponsored research. |
| Getting an account | A faculty sponsor requests it. Any SUNet ID level works. | Any full-service SUNet ID. Your account is set up the first time you log in. See [Log In for the First Time](first-login.md). |
| Home directory | 15 GB | {{ facts.home_quota }}, with no increases |
| Checking your usage | `sh_quota` | No quota command. Use `du -sh ~`. |
| Scratch | `$SCRATCH` | `{{ facts.scratch_path }}`. `$SCRATCH` isn't set, and there's no size limit. |
| Group storage | `$GROUP_HOME` and `$GROUP_SCRATCH` for every PI group | None by default. Class and group directories on request. See [Share Files with a Group](../use/sharing.md). |
| Local disk in a job | `$L_SCRATCH` | `/tmp`, which belongs to the job and is deleted when it ends |
| Oak | Available to groups that buy space on it | Not available |
| Login nodes | Light work only | Substantial work is allowed, within per-person limits. See [Use the Login Nodes](../use/login-nodes.md). |
| Interactive shell | `sh_dev` | `salloc --partition=interactive --qos=interactive`. See [Get an Interactive Session](../use/interactive-sessions.md). |
| Partition and limit summary | `sh_part` | No wrapper. See [Limits](../reference/limits.md). |
| `dev` | A partition | A QoS, used with `--qos=dev` |
| Owner and PI partitions | Yes | None. Everyone shares the same partitions and limits. |
| Largest memory | `bigmem` nodes with up to 4 TB | `bigmem`, up to {{ facts.qos.bigmem.mem }} |
| SSH to a compute node | From a login node, with a running job | The same, but compute nodes are on a private network. From your own computer, use `ssh -J`. See [SSH to a Compute Node](../use/ssh-compute-node.md). |
| Containers | Apptainer and Enroot | Apptainer and Podman. See [Containers](../software/containers.md). |
| Module names | For example, `R` | Built with Spack, with lowercase names such as `r`. Search with `module spider`. |
| AI coding agents | Available as modules | No modules. Install them yourself. See [AI Coding Agents](../software/ai-coding-agents.md). |
| Status and announcements | Status and news websites | [`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack |

## What's the Same

Logging in works the same way: your SUNet password or a Kerberos ticket, plus
Duo, and no SSH keys. Both allow low- and moderate-risk data only, never high
risk. Jobs on `normal` get {{ facts.default_runtime }} unless you ask for more,
up to {{ facts.max_runtime }}, or {{ facts.long_max_runtime }} with
`--qos=long`. Files in scratch that haven't changed in {{ facts.purge_days }}
days are removed on both.

If your work is sponsored research, or needs more than FarmShare's limits allow,
it belongs on Sherlock. See [Sherlock](../resources/sherlock.md).
