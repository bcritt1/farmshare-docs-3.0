---
tags:
    - ondemand
    - desktop
    - caddyshack
---

The Caddyshack Desktop is an OnDemand desktop for Electrical Engineering
courses. It runs on FarmShare and comes set up for EE course software, and from
it you can connect to the EE department's `caddy` machines.

Two groups run the pieces you'll use. We, Stanford Research Computing (SRC), run
FarmShare and OnDemand, including the Caddyshack Desktop session itself. EE IT
runs the `caddy` machines, the EE course software and the course setup scripts.
Knowing which is which gets your question to the right people the first time.

**Before you start:** log in to FarmShare once. See [Log In for the First
Time](../get-started/first-login.md).

## Start a Caddyshack Desktop

1. Go to [OnDemand]({{ facts.ondemand_url }}) and log in with your SUNet ID.
2. Select **Interactive Apps** > **Caddyshack Desktop**.
3. Fill in the form and select **Launch**.
4. When the session under **My Interactive Sessions** is ready, select the
   button on it to open the desktop.

You can run one Caddyshack Desktop at a time, with up to
{{ facts.qos.caddyshack.cpus }} CPUs and {{ facts.qos.caddyshack.mem }} of
memory. To start a new one, delete the old session in
**My Interactive Sessions** first.

## Connect to the Caddy Machines

The Caddyshack Desktop doesn't have AFS, and some EE course tools, such as
HSPICE, expect AFS and a Red Hat environment. For those, connect from the
desktop to one of the `caddy` machines, which EE IT runs:

1. In the desktop, open a terminal.
2. Connect to a caddy machine with graphics forwarding turned on.
   `caddy.best.stanford.edu` connects you to the least busy one:

    ```bash
    ssh -XY SUNetID@caddy.best.stanford.edu
    ```

3. Start the `tcsh` shell, then follow your course's setup instructions:

    ```bash
    tcsh
    ```

Run your course's setup commands from `tcsh`, not from the default `bash` shell.
Course setup files written for `tcsh` don't work in `bash`, so don't add them to
your `~/.bashrc`.

If `ssh` sends you somewhere other than a caddy machine, check `~/.ssh/config`
on FarmShare for a `Host` entry that matches too broadly.

EE IT's [FarmShare and Caddy Cluster
FAQ](https://ee.stanford.edu/student-resources/it-resources/ondemand-faq) and
[EE Instructional Computing
Resources](https://ee.stanford.edu/student-resources/it-resources/ee-instructional-computing-resources)
pages cover the caddy machines and EE software in more detail.

## Who to Contact

| Problem | Contact |
|---|---|
| OnDemand won't load, or the Caddyshack Desktop won't start, connect or unlock | SRC: {{ facts.support_email }}, with "FarmShare" in the subject |
| Your FarmShare home directory is full, or FarmShare is down | SRC: {{ facts.support_email }} |
| You can't log in to a caddy machine, or something is wrong on one | EE IT: `action@ee.stanford.edu` |
| EE course software, licenses, or course setup scripts | EE IT: `action@ee.stanford.edu` (TAs and instructors: `ta-itsupport@ee.stanford.edu`) |

We can't fix problems on the caddy machines or with EE software, because EE IT
manages them. If you're not sure which group to ask, write to one and copy the
other.

## If Something Goes Wrong

For problems starting or using the desktop session, see [OnDemand and
Desktops](../fix/ondemand.md).
