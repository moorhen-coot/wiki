# Moorhen wiki (retired)

The Moorhen wiki has moved to the Moorhen documentation at <https://moorhen.org/docs/>.

This repository now only serves a migration page at <https://moorhen-coot.github.io/wiki/>:

- `index.html` is the migration page.
- `404.html` redirects every old wiki URL to the migration page.
- `images/` holds the screenshots the old articles used. They are kept because
  pages elsewhere may still link to them through `raw.githubusercontent.com`.

## Deployment

GitHub Pages serves the root of the `main` branch as plain static files
(Settings → Pages → "Deploy from a branch", `main`, `/`). `.nojekyll` turns the
Jekyll build off. There is no GitHub Actions workflow: pushing to `main` is the
whole deployment.

## Old articles

The Jekyll blog and its articles were removed. The last published versions are
in the history at commit
[`fd9e42c`](https://github.com/moorhen-coot/wiki/tree/fd9e42c/blog/_posts).
