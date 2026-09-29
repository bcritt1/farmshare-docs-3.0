# FarmShare Docs Style Guide

This guide is for anyone writing or editing these docs: SRC staff, community
contributors, and anyone drafting with AI tools. The two finished pages,
[OnDemand and Desktops](src/fix/ondemand.md) and [Set Up a
Course](src/teaching/set-up-a-course.md), are the reference for how a page
should read. When this guide and those pages disagree, ask.

## Who We're Writing For

Most readers are students using FarmShare for a class and researchers doing
unsponsored work. Instructors and TAs setting up courses have their own section.
Readers come to the docs to get something done or to fix something that broke.
They aren't here to learn how FarmShare is built.

Assume different amounts of experience in different sections. Get Started and
Teaching assume the reader has never used a terminal. Other sections assume
basic shell use and link to a terminal-basics page for anyone who needs it.
Reference pages assume nothing and explain nothing; they're for looking things
up.

## Voice

Write plainly and directly, in the second person. Use imperatives for steps
("Open OnDemand", not "You should open OnDemand"). Contractions are fine.

Most of the time the job is to state facts clearly for someone who doesn't know
them yet. The troubleshooting entries on the OnDemand page are the register to
aim for: neutral, informational, with commands in code blocks. Warmth comes from
being clear and from giving reasons. It doesn't come from a friendly tone.

"We" means SRC staff. Use it where it helps, which is mostly when explaining a
limit or saying no. Don't frame whole pages as a conversation with the reader.

Leave out cheer ("Congratulations!"), jokes, scolding, and sympathy lines ("we
know this is frustrating").

## Limits and "No" Answers

When the answer is no, or there's a limit, give the reason and then the
alternative. A bare rule reads as cold and dictatorial:

> Home directories are limited to 50 GB. Increases are not available.

Say it the way a person would explain it:

> We give everyone 50 GB of home space. We'd like to offer more, but
> FarmShare's storage is shared and free, and keeping home the same size for
> everyone is how we keep it fair. So we can't raise it for individual people.
>
> For bigger data, use your scratch directory. It has no size limit. We clear
> out files there that haven't changed in 90 days, so keep copies of anything
> important somewhere else.

## How Pages Start

Start with a sentence or two that tells the reader what's on the page, in the
same plain register as the rest of it. There's no set formula, and pages
shouldn't all open the same way. Don't open with a sentence fragment, a dramatic
line, or a pitch for the feature, and don't just repeat the title. Put side
information, such as where outages are announced, in a note admonition below the
opening.

This opening from a first draft read as too friendly and conversational:

> Problems with desktops, JupyterLab, RStudio, MATLAB and VS Code in OnDemand.
> When FarmShare has an outage, sessions fail in all the ways below.

It was replaced with a plain statement of what the page covers:

> This page covers common problems with OnDemand sessions: desktops,
> JupyterLab, RStudio, MATLAB and VS Code.

## Internals and "Why"

Leave out how the system works internally unless the reader needs it to act.
Never put mechanism before the steps. When readers commonly ask why a rule
exists, answer it on the Common Questions page and link there.

Use the facts you know about the system to write reader-level statements, not to
reproduce configuration. "Jobs run for up to 2 hours unless you ask for more,
and at most 2 days" is useful. A partition table with node lists isn't. The
Limits reference page can have a simplified summary table, like Sherlock's
`sh_part` output, without node names or system detail.

## Formatting

Explanations are paragraphs. Use numbered lists only for steps done in order,
tables for comparisons, and bullets sparingly. Don't write bullets that start
with a bold label followed by a colon.

Put commands and error text in code, never only in a screenshot, so readers can
copy and search them. Bold is for interface labels the reader clicks, such as
**My Interactive Sessions**.

## Headings

Use title case for page titles, nav labels, and section headings. Lowercase
articles, coordinating conjunctions and short prepositions unless they come
first or last. Capitalize the particle in phrasal verbs: "Set Up a Course", "Log
In for the First Time".

On troubleshooting pages, each problem gets its own heading. Use the exact error
text, in code, when the reader sees one (`` `No space left on device` ``), and
keep it exactly as the error appears. When there's no error message, describe
the problem in the reader's words: "My Session Says "Completed" Right After I
Launch It".

## Numbers and Names

Every number and hostname comes from `includes/data/facts.yml`. Write
`{{ facts.home_quota }}`, never "50 GB" typed into a page. When a fact changes,
it changes in one place.

Use one term per thing. It's "FarmShare", not "the cluster", "the system" and
"the platform" in turn. Use "SUNet ID", "home directory", "scratch directory"
and "OnDemand" consistently.

## AI Voice

Pages drafted with AI tools are welcome, but they have to read like
documentation written by someone who knows FarmShare. AI-written docs are
recognizable less by particular words than by habits of framing. Watch for these
in any draft:

1. An opening that announces the page without adding anything ("This page
   explains how to…", "In this section, we will…").
2. A first line under a heading that restates the heading.
3. Sections that all have the same shape: intro, list of three, summary.
4. A closing paragraph that sums up what was just said.
5. Vague phrases where a FarmShare fact belongs ("resources may vary",
   "depending on your needs").
6. Stacked hedges ("may potentially", "in some cases, it might").
7. Filler transitions ("Additionally", "Furthermore", "It's worth noting that").
8. Idioms and chatty asides ("the usual culprits", "you're all set").
9. Tidy parallel bullet lists where a paragraph would say it better.
10. Obvious steps explained at length.
11. Promotional words ("seamless", "powerful", "robust") and inflated ones
    ("delve", "leverage", "pivotal").
12. Sentence patterns like "It's not just X, it's Y" and "X serves as Y" where
    "X is Y" would do.

The prose linter catches some of the wording. Most of the list needs a reviewer
who reads the draft as a student would.

## Page Templates

Pages follow the Sherlock docs' layout. A page has no `title:` and no top-level
`#` heading. Its title comes from its label in the `nav` in `mkdocs.yml`, and
the theme shows it at the top of the page. Front matter holds only `tags` (and
`icon`, if used). Prose is wrapped at 80 characters, which the Markdown lint
checks. Code blocks and tables aren't wrapped.

There are three page types. Every page is self-contained: it doesn't depend on
where it sits in the nav, and it states its own prerequisites, so pages can be
moved or merged later.

A **task page** opens with the one-sentence intro and a "Before you start" line
if there's a prerequisite. Then come the steps, a section of things to know
(limits and behavior, each with its reason), and a link to the matching
troubleshooting page. Batch scripts get one annotation per `#SBATCH` line, as on
the Sherlock docs.

````markdown
---
tags:
    - ondemand
    - desktop
---

A FarmShare Desktop is a Linux desktop that runs on FarmShare and opens in
your browser, for programs that need a graphical interface.

**Before you start:** log in to FarmShare once. See [Log In for the First Time](../get-started/first-login.md).

## Start the Desktop

1. Go to [OnDemand]({{ facts.ondemand_url }}).
2. Select **Interactive Apps** > **FarmShare Desktop**.

## Things to Know

## If Something Goes Wrong

See [OnDemand and Desktops](../fix/ondemand.md).
````

A **troubleshooting page** covers one area. It lists each problem as a heading,
which puts every problem in the page's sidebar table of contents. Under each
heading, say what's usually going on, then what to do. If readers can reach the
same problem from two areas, repeat the solution on both pages; that's better
than making them hunt.

````markdown
---
tags:
    - troubleshooting
    - ondemand
---

This page covers common problems with OnDemand sessions: desktops, JupyterLab,
RStudio, MATLAB and VS Code.

!!! note "Outages"
    If sessions are failing for everyone, FarmShare may be down. Outages and maintenance are announced in `{{ facts.announce_channel }}`.

## `Invalid account or account/partition combination`

Your FarmShare account hasn't been fully set up yet. ...
````

A **reference page** is a table with short notes only where a cell needs one.

## Before You Merge

Check every claim about how FarmShare behaves, not just the numbers. Confirm it
on the system, in recent support replies, or with the FarmShare admins. Two
claims in the first sample pages turned out wrong this way: one about why the
desktop lock rejects passwords, and one about who can read course directories.
