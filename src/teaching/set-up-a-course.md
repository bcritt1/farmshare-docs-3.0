---
title: Set up a course
tags: [teaching]
---

# Set up a course

We can give your course a shared directory on FarmShare, with access groups so your teaching staff can manage files and your students can read them. Students then work in one place with the same files, instead of copying materials around.

You don't need us to set anything up for students just to use FarmShare. Anyone with a full-service SUNet ID can log in and use it for coursework. A course setup is for when you want shared files, or class-managed access to them.

## What you get

When we set up a course, we create a directory for it at `/home/classes/<dept>/<number>`, for example `/home/classes/cs/101`. You own the directory.

We also create two Stanford workgroups to control who can get in:

| Workgroup | Who belongs in it | What they can do in the course directory |
|---|---|---|
| `farmshare:<dept>-<number>-staff` | You and your TAs or CAs | Read and write |
| `farmshare:<dept>-<number>` | Your students | Read |

You manage the staff workgroup, and the staff workgroup manages the student workgroup. That way your TAs can add and remove students without waiting for you.

If you need scratch space for the course, for large datasets that students all read, ask for a class scratch directory at the same time.

## Ask for a course setup

The request has to come from the instructor of record for the course. We check the instructor against ExploreCourses, so we can't act on a request that only comes from a TA. If your TA is handling the details, send the request yourself and copy them.

Email {{ facts.support_email }} with "FarmShare course setup" in the subject, and include:

1. The course number and quarter, for example CS 101, Winter 2027.
2. The SUNet IDs of anyone who should be in the staff workgroup.
3. Whether you'll need class scratch space, course software, or reserved nodes for an assignment.

Ask as early as you can, ideally a few weeks before the quarter starts. The first weeks of each quarter are our busiest time, and course software and reserved nodes take longer to arrange than a directory does. See [Request course software or reserved nodes](course-software-and-reservations.md).

## After we set it up

Add your TAs to the staff workgroup, and have them add students to the student workgroup, in [Workgroup Manager](https://workgroup.stanford.edu).

Each student also needs to log in to FarmShare once before the first assignment. The first login finishes creating their account, and until then OnDemand and job submission won't work for them. [Log in for the first time](../get-started/first-login.md) is a good page to send them.

We don't create a separate directory for each student. Students keep their own work in their home or scratch directories. If you want students to hand in work through the course directory, ask us for a drop box. We can set permissions so students can add files but not see each other's. See [Add students and TAs](add-students-and-tas.md).

## If something goes wrong before class

If something breaks close to a class or a deadline, email {{ facts.support_email }} with "FarmShare" and "urgent" in the subject. Our support hours are business days, so problems reported on a weekend are picked up on the next business day. [Get ready for class day](class-day.md) has a checklist for heading off the common problems.
