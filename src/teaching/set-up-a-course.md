---
tags:
    - teaching
---

The instructor of a course can ask for a shared course directory on FarmShare.
It comes with two workgroups: one for course staff, who can change the files,
and one for students.

Students don't need a course setup to use FarmShare. Anyone with a full-service
SUNet ID can log in and use it for coursework. A course setup is only needed for
shared course files.

## What the Setup Includes

When we set up a course, we create a directory for it at
`/home/classes/<dept>/<number>`, for example `/home/classes/cs/101`. You own the
directory.

We also create two Stanford workgroups for the course:

| Workgroup | Who belongs in it | Who manages it |
|---|---|---|
| `farmshare:<dept>-<number>-staff` | You and your TAs or CAs | You |
| `farmshare:<dept>-<number>` | Your students | Your course staff |

Your course staff can add and change files in the course directory. Everyone
else can read them, including other FarmShare users as well as your students. If
some files shouldn't be visible outside the class, such as solutions or student
data, say so in your request and we'll set up permissions with you.

Because the staff workgroup manages the student workgroup, your TAs can add and
remove students themselves.

If you need scratch space for the course, for large datasets that students all
read, ask for a class scratch directory at the same time.

## Ask for a Course Setup

The request has to come from the instructor of record for the course. We check
the instructor against ExploreCourses, so we can't act on a request that only
comes from a TA. If your TA is handling the details, send the request yourself
and copy them.

Email {{ facts.support_email }} with "FarmShare course setup" in the subject,
and include:

1. The course number and quarter, for example CS 101, Winter 2027.
2. The SUNet IDs of anyone who should be in the staff workgroup.
3. Whether you'll need class scratch space, course software, or reserved nodes
   for an assignment.

Ask as early as you can, ideally a few weeks before the quarter starts. The
first weeks of each quarter are our busiest time, and course software and
reserved nodes take longer to arrange than a directory does. See [Request course
software or reserved nodes](course-software-and-reservations.md).

## After We Set It Up

Add your TAs to the staff workgroup, and have them add students to the student
workgroup, in [Workgroup Manager](https://workgroup.stanford.edu).

Each student also needs to log in to FarmShare once before the first assignment.
The first login finishes creating their account, and until then OnDemand and job
submission won't work for them. Send them [Log in for the first
time](../get-started/first-login.md).

We don't create a separate directory for each student. Students keep their own
work in their home or scratch directories. If you want students to hand in work
through the course directory, ask us for drop-box folders, and we'll set up
permissions for them. See [Add students and TAs](add-students-and-tas.md).

## If Something Goes Wrong Before Class

If something breaks close to a class or a deadline, email
{{ facts.support_email }} with "FarmShare" and "urgent" in the subject. Our
support hours are business days, so problems reported on a weekend are picked up
on the next business day. [Get ready for class day](class-day.md) has a
checklist of common problems to check for in advance.
