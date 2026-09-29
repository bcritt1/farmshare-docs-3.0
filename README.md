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

1. Push this repo to GitHub.
2. In the repo, go to **Settings > Pages** and set **Source** to
   **GitHub Actions**. This needs admin rights on the repo. If Pages is disabled
   for the org, an org owner has to allow it.
3. Every push to `main` then builds and deploys the site through
   `.github/workflows/deploy.yml`.

## Rename or move the repo

Only four lines in `mkdocs.yml` name the owner or URL: `site_url`, `repo_name`,
`repo_url` and `edit_uri`. After a rename or a transfer (for example into
`stanford-rc/farmshare-docs`), update those. For a custom domain such as
`docs.farmshare.stanford.edu`, also add a `src/CNAME` file with the domain.

## Where things live

| Path | What it is |
|---|---|
| `src/` | Pages. One topic per page, so pages can be moved or merged. |
| `mkdocs.yml` | Site config and the nav. Moving a page means editing one line here and adding a redirect. |
| `includes/data/facts.yml` | Every number and name the pages use (quotas, hostnames). Pages say `{{ facts.home_quota }}`, never "50 GB". |
| `includes/` | Shared text snippets. |
| `styles/FarmShare/`, `.vale.ini` | Prose lint rules. Error-level rules block a merge; warnings are for reviewers. |
| `.github/workflows/` | `checks.yml` (build, Markdown, links, prose) and `deploy.yml` (GitHub Pages). |
