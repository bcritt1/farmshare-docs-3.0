# FarmShare docs 3.0

A draft of new documentation for FarmShare, Stanford Research Computing's
cluster for coursework and unsponsored research. The setup follows the [Sherlock
docs](https://github.com/stanford-rc/www.sherlock.stanford.edu): MkDocs with the
Material theme, deployed to GitHub Pages.

## Preview locally

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve
```

Then open <http://127.0.0.1:8000/farmshare-docs-3.0/>. The path matches
`site_url` in `mkdocs.yml`, so it changes if the repo is renamed. `mkdocs serve`
keeps running until you stop it with Ctrl-C.

## Publish on GitHub Pages

Deployment works the same way as on the Sherlock docs.

1. Push this repo to GitHub. The `deploy` workflow runs `mkdocs gh-deploy`,
   which builds the site and pushes it to a `gh-pages` branch.
2. After that first run, go to **Settings > Pages** in the repo, set **Source**
   to **Deploy from a branch**, and choose `gh-pages`. This needs admin rights
   on the repo. If Pages is disabled for the org, an org owner has to allow it.
3. Every push to `main` that changes the site then redeploys it.

## Writing Docs

Read the [style guide](STYLE-GUIDE.md) and the [contributing
guide](CONTRIBUTING.md). The [writing plan](WRITING-PLAN.md) lists every page
and the order to write them in.

## Rename or move the repo

Only four lines in `mkdocs.yml` name the owner or URL: `site_url`, `repo_name`,
`repo_url` and `edit_uri`. After a rename or a transfer (for example into
`stanford-rc/farmshare-docs`), update those. For a custom domain such as
`docs.farmshare.stanford.edu`, also add a `src/CNAME` file with the domain.

## Where This Differs From the Sherlock Docs

The setup, checks, deploy and page layout follow the Sherlock docs. There are
two deliberate differences:

- Headings use title case. Sherlock uses sentence case.
- The checks include a Vale prose-lint job (`styles/FarmShare/`) that Sherlock
  doesn't have.

## Where things live

| Path | What it is |
|---|---|
| `src/` | Pages. One topic per page, so pages can be moved or merged. |
| `mkdocs.yml` | Site config and the nav. Moving a page means editing one line here and adding a redirect. |
| `includes/data/facts.yml` | Every number and name the pages use (quotas, hostnames). Pages say `{{ facts.home_quota }}`, never "50 GB". |
| `includes/` | Shared text snippets. |
| `styles/FarmShare/`, `.vale.ini` | Prose lint rules. Error-level rules block a merge; warnings are for reviewers. |
| `.github/workflows/` | `checks.yml` (build, Markdown, links, prose) and `deploy.yml` (GitHub Pages). |
