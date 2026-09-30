---
tags:
    - teaching
---

Access to a course directory is controlled by the course's two Stanford
workgroups. You add TAs to the staff workgroup, and course staff add students to
the student workgroup, in [Workgroup Manager](https://workgroup.stanford.edu).

**Before you start:** the course has to be set up. See [Set Up a
Course](set-up-a-course.md).

## Who Manages Which Workgroup

| Workgroup | Members | Managed by |
|---|---|---|
| `farmshare:<dept>-<number>-staff` | You and your TAs or CAs | You |
| `farmshare:<dept>-<number>` | Your students | Anyone in the staff workgroup |

On FarmShare, the workgroups show up as groups named
`farmshare_<dept>-<number>-staff` and `farmshare_<dept>-<number>`. That's the
name you see in `ls -l` output for files in the course directory.

## Add TAs

1. Go to [Workgroup Manager](https://workgroup.stanford.edu) and log in with
   your SUNet ID.
2. Open `farmshare:<dept>-<number>-staff`.
3. Add each TA by SUNet ID.

TAs in the staff workgroup can change files in the course directory and manage
the student workgroup.

## Add Students

1. In [Workgroup Manager](https://workgroup.stanford.edu), open
   `farmshare:<dept>-<number>`.
2. Add each student by SUNet ID.

Students who were logged in to FarmShare when you added them should log out and
log back in, so their new group membership takes effect.

Every student also needs to log in to FarmShare once before they can use
OnDemand or submit jobs. Send them [Log In for the First
Time](../get-started/first-login.md).

## Remove Someone

Remove them from the workgroup in Workgroup Manager. That ends their access to
the course directory. It doesn't affect their own FarmShare account, which stays
active for as long as their SUNet ID does.

## Drop-Box Folders

We don't create a separate directory for each student. If you want students to
hand in work through the course directory, email {{ facts.support_email }} and
describe what you need, for example a folder per student that only that student
and course staff can read. We'll set up the permissions with you and help you
test them before students start using them.

## If Something Goes Wrong

If a student is in the workgroup but still can't reach the course directory
after logging out and back in, email {{ facts.support_email }} with "FarmShare"
in the subject, the student's SUNet ID and the course directory path.
