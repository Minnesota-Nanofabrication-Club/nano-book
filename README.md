> ### 🔬 Minnesota Nanofabrication Club
> New here? Start at the club website — what we're building, current projects, and how to join:
> **https://minnesota-nanofabrication-club.github.io/club_website/**

---

# ASIC Network docs template

Fork this repo to start a new docs book for the network. It's a plain
[mdBook](https://rust-lang.github.io/mdBook/) with the ASIC Network look
applied via `theme/` — no build tooling to install for writing, just markdown.

`theme/` is a **git submodule** (see [asic-network-docs/theme](../theme)),
not a copy — the visual layer is shared and versioned separately from any
one book's content. Clone with submodules:

```
git clone --recurse-submodules <this-repo-url>
# or, after a plain clone:
git submodule update --init
```

To change how a book looks without touching its content, point the
submodule at a different theme commit/branch (see the theme repo's README).

## Set up a new book

1. Fork/copy this repo, rename it to `<your-track>-tutorials`.
2. In `book.toml`, replace every `EDIT ME` value (title, repo URL).
3. In `theme/header.hbs`, check the "Home" link points at the right main site.
4. GitHub repo settings → **Pages** → **Source: GitHub Actions** (one-time, per repo).
5. Write your first page (`src/TEMPLATE.md` → copy it, fill it in, add it to
   `src/SUMMARY.md`), push to `main`. The included workflow builds and deploys
   on every push.

## Writing pages

- One `src/*.md` file per page. Copy `src/TEMPLATE.md` to start a new one.
- List pages, in order, in `src/SUMMARY.md` — nesting/sections are supported,
  see [mdBook's SUMMARY.md format](https://rust-lang.github.io/mdBook/format/summary.html).
- Link between pages with plain relative links: `[text](other-page.md)`.
- Images live under `src/img/`, referenced relative to the page: `img/foo.png`.
- Raw HTML is allowed (e.g. `<iframe>` embeds for interactive content) —
  unlike the old renderer, mdBook doesn't strip it.

## Preview locally

```
mdbook serve
```

Open `http://localhost:3000`. Rebuilds on save.

## Why mdBook

Every book built from this template reads plain CommonMark markdown plus one
manifest file (`SUMMARY.md`) — no ASIC-Network-specific syntax or link
conventions. That means the same source files also build cleanly with
`mdbook build` on their own, standalone, on any machine or any other site,
and can be composed into a larger "collection" book (multiple universities'
docs combined into one navigation) by pulling their `src/` directories in
and generating a combined `SUMMARY.md` — without touching their content.
