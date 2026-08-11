# bence.io

The source of [bence.io](https://bence.io). Jekyll, using the
[al-folio](https://github.com/alshedivat/al-folio) theme (v1.2), built by GitHub
Actions and published to the `gh-pages` branch.

Everything on the site is a markdown or YAML file. There is no HTML to edit for
ordinary changes.

## The pages

| URL | File |
| --- | --- |
| `/` | `_pages/about.md` |
| `/cv/` | `_pages/cv.md` (content comes from `_data/cv.yml`) |
| `/cv.pdf` | `cv.pdf` in the repository root |
| `/projects/` | `_pages/projects.md`, one file per project in `_projects/` |
| `/apps/` | `_pages/apps.md` |
| `/contact/` | `_pages/contact.md` (links come from `_data/socials.yml`) |
| `/blog/` | `_pages/blog.md`, one file per post in `_posts/` |

The navigation menu builds itself from the `nav:` and `nav_order:` lines in the front
matter of each page in `_pages/`. Add a page with `nav: true` and it appears in the
menu, on desktop and mobile, with no other change. Light/dark mode is part of the
theme (`enable_darkmode` in `_config.yml`) and remembers the reader's choice.

## The placeholder slots

Nothing on the site is written for you. Every piece of prose is a clearly-marked slot
showing `[ ... to be written ]` on the page until you fill it in. Each one is a single
line in a single file:

| What | File | Line |
| --- | --- | --- |
| Profession / one-line title, under your name on the home page | `_pages/about.md` | `subtitle:` |
| Small block beside the portrait (location, affiliation, anything) | `_pages/about.md` | `more_info:` |
| Home page intro | `_pages/about.md` | the body text |
| Email address | `_data/socials.yml` | `email:` (commented out) |
| How you prefer to be reached | `_pages/contact.md` | the body text |
| Contact page strapline | `_pages/contact.md` | `description:` |
| CV opening paragraph | `_data/cv.yml` | `summary:` |
| Email on the CV page | `_data/cv.yml` | `email:` (commented out) |
| CV page strapline | `_pages/cv.md` | `description:` |
| Projects page strapline | `_pages/projects.md` | `description:` |
| Apps page strapline and body | `_pages/apps.md` | `description:` and body |
| Each project's write-up | `_projects/<name>.md` | the body text |
| Blog strapline | `_config.yml` | `blog_description:` |
| Contact note under the links | `_config.yml` | `contact_note:` |

Everything that is *not* a slot was lifted from the CV PDF in your own wording — the
job titles, dates, achievements and one-line project descriptions. The CV page is
generated from `_data/cv.yml`, so the CV flows through to the site automatically and
is never retyped in HTML.

The Cambridge address `bh525@cantab.ac.uk` has been removed from the entire site, and
the build now fails if it ever reappears in the published output. **The CV PDF is a
separate matter: its contents cannot be edited here, so if the PDF carries that
address it is still on the site inside `/cv.pdf`.**

## How to do the common things

**Update the CV.** Edit `_data/cv.yml` — the page at `/cv/` is generated from it.
Replace the PDF by overwriting `cv.pdf` in the root; the download button and the
`/cv.pdf` URL both point at that one file, so there is nothing else to change.

**Add a project.** Copy any file in `_projects/`, for example:

```yaml
---
layout: page
title: A new thing
permalink: /projects/a-new-thing/
description: One line, shown on the card.
img: assets/img/a-new-thing.png   # optional; the card works without it
importance: 1                      # lower numbers sort first
category: code                     # 'code' or 'research'; see _pages/projects.md
---

Markdown from here on.
```

To add a new category, add it to `display_categories` in `_pages/projects.md`.

**Add an app.** `/apps/` is deliberately empty right now. When there is something to
put there, either write it up like a project entry, or drop a self-contained HTML
page into `assets/` and frame it in `_pages/apps.md`:

```liquid
<iframe src="{{ '/assets/html/your-app.html' | relative_url }}" width="100%" height="500px" frameborder="0"></iframe>
```

**Add a blog post.** Create `_posts/YYYY-MM-DD-a-title.md` with front matter:

```yaml
---
layout: post
title: a title
date: 2026-08-11 10:00:00 +0100
description: one line, shown in the post list
tags: whatever you like
---
```

**Change a contact link.** Edit `_data/socials.yml`. A value that is filled in
appears on `/contact/` and in the footer icons; a value that is commented out does
not appear anywhere. No phone number is published — that file explains why.

**Add a portrait to the home page.** Put the image in `assets/img/` and put its
filename in the `profile: image:` line of `_pages/about.md`. Nothing else changes.

## Embedding things in a post

`_posts/2026-08-10-embedding-things.md` is a working example of every embed the site
supports: syntax-highlighted code, maths, responsive and zoomable images, an iframe
around a self-contained program, Plotly, Chart.js and Vega-Lite charts, and a Jupyter
notebook rendered inline from `assets/jupyter/`. Copy from it rather than looking up
the syntax.

**That post is a reference, not a real one.** Delete `_posts/2026-08-10-embedding-things.md`
whenever it has stopped being useful — nothing else depends on it.

## Deployment

Pushing to `main` runs `.github/workflows/deploy.yml`, which builds the site and
pushes the result to the `gh-pages` branch; GitHub Pages serves that branch at
bence.io (the `CNAME` file pins the domain). The workflow fails the build if `/cv`,
`/cv.pdf`, `/projects`, `/apps`, `/contact` or `/blog` are missing from the output,
so a broken route cannot ship quietly.

The theme cannot be built by GitHub Pages' own Jekyll (it uses plugins Pages does not
allow), which is why the build happens in Actions. **Settings → Pages → Build and
deployment → Source must be set to `gh-pages`.** That is a one-off manual setting:
the Actions token is not permitted to change it, so if it is ever reset, every page
except `/cv.pdf` will 404 until it is set back.

### Working on it locally

Requires Ruby and Bundler:

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000
```
