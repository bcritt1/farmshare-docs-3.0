---
tags:
    - storage
    - sharing
---

To share files with other people on FarmShare, put them in a directory those
people can reach and set the file permissions to let them in. FarmShare doesn't
create shared group space automatically, but classes and groups can ask us for a
shared directory.

## Ask for a Group Directory

We set up shared directories for groups on request, in `/home/groups` and
`/scratch/groups`. Email {{ facts.support_email }} with "FarmShare" in the
subject, and say who the group is, what the directory is for, and the SUNet IDs
of the people who need access. Say whether you need home space, scratch space,
or both. Scratch space isn't backed up, so keep copies of anything important
somewhere else.

For a course, the instructor asks for a course directory instead. See [Set Up a
Course](../teaching/set-up-a-course.md).

FarmShare is for coursework and unsponsored research. If your group is sharing
data for sponsored research, see [Sherlock](../resources/sherlock.md).

## How Access Works

Access to files on FarmShare is controlled by ordinary Unix permissions. Each
file and directory has an owner and a group, and separate read, write and
execute permissions for the owner, the group and everyone else. A shared
directory is owned by a group, and the people in that group can use it.

To see a directory's owner, group and permissions:

```bash
ls -ld /home/groups/mygroup
```

To see which groups you're in:

```bash
groups
```

When you create files in a shared directory, give the group the access it needs.
For example, to let the group read and write everything in a folder:

```bash
chgrp -R mygroup /home/groups/mygroup/data
chmod -R g+rwX /home/groups/mygroup/data
```

The capital `X` gives execute permission to directories but not to ordinary
files. People need execute permission on a directory to open anything inside it,
and on every directory above it in the path.

Don't make files readable or writable by everyone (`chmod 777`) to get around a
permission problem. Anyone who logs in to FarmShare could then read or change
them. If the group permissions aren't doing what you expect, [ask
us](../fix/get-help.md).

## When Group Permissions Aren't Enough

Sometimes one group isn't enough, for example when each student needs a private
drop-box folder that only course staff can read. Access control lists (ACLs) can
give individual people their own access to a file or folder. Ask us if you need
them, and describe who should be able to read or change what. We'll set them up
with you, or suggest a simpler arrangement with groups if one works.

## Sharing from Your Home Directory

We don't recommend opening up your home directory to share files. It holds
settings, keys and other private files that shouldn't be readable by others. Ask
for a group directory instead, or copy the files to a place the other people can
already reach.

To share with people who don't use FarmShare, copy the files off FarmShare
first. See [Move Files to and from FarmShare](transfer.md).
