# Zixi Wang Personal Website

This repository contains the source for <https://zixiwang0o0.github.io>.
It is a Jekyll site for my homepage, writing, portfolio, notes, CV, and small
web experiments.

## Main Structure

- `_posts/`: dated blog posts and writing.
- `_portfolio/projects/`: project pages.
- `_portfolio/notes/`: study notes and supporting technical notes.
- `_portfolio/overview.md`: portfolio overview page.
- `_layouts/` and `_includes/`: shared Jekyll templates.
- `css/`, `js/`, `fonts/`, and `pwa/`: theme and browser assets.
- `img/`: images used by pages, posts, projects, and notes.
- `files/`: downloadable files such as the public CV PDF.
- `experiments/`: standalone demos that are separate from the main Jekyll pages.

## Local Preview

Install Jekyll and the paginate plugin, then run:

```sh
jekyll serve
```

The site is served at <http://127.0.0.1:4000/>.

## Common Updates

To add a post:

1. Create a Markdown file in `_posts/` named `YYYY-MM-DD-title.md`.
2. Add YAML front matter with `layout: post`, `title`, `date`, and optional tags.
3. Put related images under `img/` and reference them with `{{ site.baseurl }}/img/...`.

To add a portfolio project:

1. Create a Markdown file in `_portfolio/projects/`.
2. Set `type: project` in the front matter.
3. Add optional metadata such as `description`, `tech`, `github`, `demo`, or `note`.

To add a portfolio note:

1. Create a Markdown file in `_portfolio/notes/`.
2. Set `type: note` in the front matter.
3. Keep large supporting images grouped by topic under `img/`.

## Navigation

The header navigation is defined explicitly in `_includes/nav.html`:

```text
Home -> Post -> Portfolio -> Archive
```

## Maintenance Notes

- Keep `_config.yml` limited to settings that are actively used by the site.
- Avoid adding new template demo files unless they are part of the live site.
- Prefer grouping new images by post, project, or note topic so `img/` remains navigable.
- `less/`, `Gruntfile.js`, and `package.json` are legacy theme build files; keep them only if you still compile the old theme assets.

## Credits

This site is based on a Jekyll blog theme derived from Hux Blog and later
customized for this personal homepage.
