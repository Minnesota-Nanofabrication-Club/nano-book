> ### 🔬 Minnesota Nanofabrication Club
> New here? Start at the club website — what we're building, current projects, and how to join:
> **https://minnesota-nanofabrication-club.github.io/club_website/**

---

# Nano Book: the club's documentation

How every machine in the Minnesota Nanofabrication Club's fab works, how it
is built, and how to help. It is a plain
[mdBook](https://rust-lang.github.io/mdBook/): every page is a Markdown file
in `src/`, and the site rebuilds itself when you push to `main`.

Content and styling are kept apart. This repository is only content; the look
lives in `theme/`, a **git submodule** pointing at the theme repository.
Clone with it:

```
git clone --recurse-submodules <this-repo-url>
# or, after a plain clone:
git submodule update --init
```

## Writing pages

- One `src/*.md` file per page. Copy `src/TEMPLATE.md` to start a new one.
- List pages, in order, in `src/SUMMARY.md`. `# Gen One Fab`-style lines
  are the sidebar's section headings.
- Link between pages with relative links: `[text](other-page.md)`.
- Images live under `src/img/`, referenced relative to the page.
- Raw HTML is allowed (for example an `<iframe>` embed).

## Machine pages match the website

The club website links each machine card to
`<docs address>/machines/<machine file name>.html`. So a machine's page here
is `src/machines/<same name as the website's content/machines/ file>.md`.
Add or rename a machine on the website, and do the same here. Most machine
pages are stubs (a one-line summary and a "Stub" note) until someone writes
them.

The website's footer also links `getting-started.html` and
`contributing.html`, so keep those two pages.

Pages that moved keep working through `[output.html.redirect]` in
`book.toml`.

## Preview locally

Install mdBook **0.5.x** (the theme needs it; CI uses 0.5.3), then:

```
mdbook serve
```

Open `http://localhost:3000`. It rebuilds on save.

## Publishing

`.github/workflows/deploy.yml` builds and deploys to GitHub Pages on every
push to `main` (Settings → Pages → Source: GitHub Actions, once). To show an
"under construction" page instead, set the repository variable
`SITE_MODE` to `placeholder` (see `.github/workflows/placeholder.yml`).

## Moving from staging to the club's repositories

`book.toml` (`git-repository-url`, `edit-url-template`, `site-url`) and
`.gitmodules` (the theme URL) point at the staging forks. Change them to the
club's repositories, and change the website address in `theme/header.hbs`.
