# Contributing

Changes to these docs go through pull requests, the same way the Sherlock docs
work. If you have write access, open a PR from a branch. If you don't, fork the
repo and open a PR from your fork. To report a problem without fixing it, use
the feedback link on any page or open an issue.

## Writing a Change

Read the [style guide](STYLE-GUIDE.md) first. The two finished pages it links to
show how a page should read.

Put numbers and hostnames in `includes/data/facts.yml` and refer to them from
pages. If you add a page, add it to the `nav` in `mkdocs.yml`. If you move or
rename one, also add a redirect under the `redirects` plugin so old links keep
working.

## Previewing

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve
```

The site is served at the path in `site_url`, currently
<http://127.0.0.1:8000/farmshare-docs-3.0/>.

## Checks

Every PR runs the checks in `.github/workflows/checks.yml`. A few things block a
merge: a build that fails in strict mode (usually a broken internal link),
malformed Markdown, a broken external link, an unfilled placeholder, or chatbot
phrasing. Everything else the prose linter finds is a warning for you and your
reviewer to judge.

## Before Asking for Review

Confirm every claim about how FarmShare behaves, not just the numbers, on the
system, in recent support replies, or with the FarmShare admins. If you drafted
with an AI tool, read the draft against the AI Voice section of the style guide
before you open the PR.
