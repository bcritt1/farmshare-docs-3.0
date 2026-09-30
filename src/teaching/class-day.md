---
tags:
    - teaching
---

Most problems students hit in the first session on FarmShare can be caught a
few days ahead. Go through these checks before a class or assignment that uses
FarmShare, and pass the student ones on to your class.

## Students Have Logged In Once

A student's FarmShare account is finished the first time they log in to a login
node. Until then, OnDemand apps and jobs fail with
`Invalid account or account/partition combination`. Have every student log in
once before the first class, by SSH or through **Clusters** >
**FarmShare Shell Access** in OnDemand. [Log In for the First
Time](../get-started/first-login.md) has the steps.

## Students' Home Directories Aren't Full

When a home directory is full, OnDemand sessions stop right after they start,
and jobs fail. Everyone's home directory holds {{ facts.home_quota }}, and
Python environments and package caches fill it faster than students expect.

A few days before class, have students check their usage on a login node:

```sh
du -sh ~
```

If it's close to `{{ facts.home_quota_du }}`, [Check and Free Up
Space](../use/free-up-space.md) shows how to clear it. For course data sets,
use the course directory or class scratch space rather than copies in each
student's home directory.

## The Software Works

Run the assignment on FarmShare yourself, the way students will: the same
modules, the same OnDemand app, the same desktop size. Software can change
between quarters, and a missing module is much easier for us to fix a week
before class than on the day. If something is missing, see [Request Course
Software or Reserved Nodes](course-software-and-reservations.md).

## There's Room for Everyone

OnDemand desktops and other interactive sessions share a pool of compute nodes
with everyone else on FarmShare. A class of students usually fits, but FarmShare
is busiest in the weeks before exams and near deadlines, and sessions can wait
in the queue then.

To help students get started:

- Recommend the smallest desktop size that works for the assignment. Smaller
  sessions start sooner.
- Tell students they can leave a request in the queue and ask OnDemand to email
  them when it starts.
- Students can check how busy FarmShare is in OnDemand under **Clusters** >
  **System Status** before they start a session.

If you expect the whole class to work at the same time, [ask us](../fix/get-help.md)
what to expect.

## GPUs Are Reserved If You Need Them

FarmShare has {{ facts.gpu_nodes * facts.gpus_per_node }} GPUs for everyone,
and batch jobs that ask for GPUs are scheduled ahead of interactive sessions. If
students need a GPU in a desktop or interactive session, the wait can be long
and hard to predict. For an assignment that depends on GPUs, ask us to reserve
some for the class. See [Request Course Software or Reserved
Nodes](course-software-and-reservations.md).

## Students Connect to the Login Nodes the Right Way

The **FarmShare Shell Access** terminal in OnDemand always opens on the same
login node, `rice-01`. For a class working in terminals at the same time, have
students connect with SSH to `{{ facts.login_host }}` instead, which spreads
them across the login nodes. Heavy work, such as running a large program for the
whole class, belongs in a desktop or an [interactive
session](../use/interactive-sessions.md) on a compute node.

## You Know How to Reach Us

Email {{ facts.support_email }} with "FarmShare" and "urgent" in the subject if
something breaks close to class. We answer during business hours, so a problem
reported on a weekend is picked up on the next business day. Outages and
maintenance are announced in
[`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack.
