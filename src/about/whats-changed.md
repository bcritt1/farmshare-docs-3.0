---
tags:
    - about
---

Changes to FarmShare that affect how you use it are listed here, newest first.
Day-to-day announcements, such as maintenance and outages, are posted in
[`{{ facts.announce_channel }}`]({{ facts.announce_url }}) on Slack.

## December 2025

FarmShare moved to new hardware and new storage, with major software updates. It
now runs {{ facts.os }}.

!!! review "Needs Review"
    Can scratch data from before the December 2025 upgrade still be copied over,
    and for how long?

Scratch data wasn't moved to the new storage automatically. If you had files in
scratch before the upgrade and can't find them, email {{ facts.support_email }}
to ask whether they can be copied over. See [My Old Scratch Path Doesn't
Exist](../fix/storage.md#my-old-scratch-path-doesnt-exist). The old scratch
path, `/farmshare/user_data/$USER`, no longer exists. Your scratch directory is
now `{{ facts.scratch_path }}`.

Installed software and module versions changed. If a module you used before is
missing or has a different version, run `module spider <name>` to see what's
installed now, and [ask us](../software/request.md) if something you need is
gone. Programs you compiled yourself, and Python or R packages installed for an
older version, may need to be reinstalled. See [Software and
Modules](../fix/software.md#a-program-i-built-myself-stopped-working).

## Winter Quarter 2025

The previous FarmShare environment, FarmShare 2, was retired, and
`{{ facts.login_host }}` became the name for the login nodes. Home directories
moved from `/home/$USER` to `/home/users/$USER`. If a script has the old path
typed into it, change it to `~` or `$HOME`, which always point to your home
directory.
