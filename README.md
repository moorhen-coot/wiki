# Moorhen wiki (retired)

The Moorhen wiki has moved to the Moorhen documentation at <https://moorhen.org/docs/>.

This repository now only serves a migration page at <https://moorhen-coot.github.io/wiki/>:

- `index.html` is the migration page.
- `404.html` redirects every old wiki URL to the migration page.
- `images/` holds the screenshots the old articles used. The archived articles
  and pages elsewhere link to them through `raw.githubusercontent.com`.

## Deployment

GitHub Pages serves the root of the `main` branch as plain static files
(Settings → Pages → "Deploy from a branch", `main`, `/`). `.nojekyll` turns the
Jekyll build off. There is no GitHub Actions workflow: pushing to `main` is the
whole deployment.

## Old articles (archive)

The Jekyll blog was removed, but its articles are kept for archive as plain
Markdown in `blog/_posts/`, with their screenshots in `images/`. They are not
rendered by the site and nothing on the site links to them.

Every article starts with a warning: they are outdated and must not be used
with Moorhen 1.0 or later.
