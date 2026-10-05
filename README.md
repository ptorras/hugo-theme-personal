# hugo-theme-personal

A quiet, readable Hugo theme: serif body copy, grotesque headers, a
table of contents on every post, solarized-light code blocks, and
Tufte-style side notes for footnotes.

## Fonts

- Body text: **Charter** (falls back to Georgia/Cambria/serif — not bundled,
  since it ships with most operating systems).
- Headers and UI text: **Archivo** (bundled, SIL OFL, variable weight).
- Code: **Fira Mono** (bundled, SIL OFL, regular + bold).

## Required site config

Chroma must emit CSS classes (not inline styles) so `css/chroma.css`
(generated with `hugo gen chromastyles --style=solarized-light`) actually
applies:

```toml
[markup.highlight]
  noClasses = false
  style = "solarized-light"
```

## Table of contents

Shown automatically at the top of every post that has headings. Disable
per-page with `toc: false` in front matter.

## Side notes

Write footnotes the normal Hugo/Markdown way (`text[^1]` + `[^1]: ...`).
`js/sidenotes.js` rewrites them into margin notes at load time; without
JavaScript they render as an ordinary footnote list at the bottom of the
post.

## Menu

Populated from `[[menu.main]]` entries in the site config.

## Example site

See `exampleSite/` for a minimal working configuration. To preview it:

```sh
cd exampleSite
ln -s ../.. themes/personal   # one-time, not committed
hugo server
```
