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

## Chess

Three shortcodes, sharing the board colours (`--board-light`,
`--board-dark`, `--board-mark` in `main.css`) and the cburnett piece set:

**`fen`**: a static diagram, drawn as inline SVG at build time (no JavaScript).
Only the piece-placement field of the FEN is used.

```
{{< fen "rnbqkbnr/pppppppp/8/8/4P3/8/PPPP1PPP/RNBQKBNR b KQkq - 0 1" >}}

{{< fen fen="..." caption="After 6. Bc4" orientation="black"
        highlight="f7" arrows="c4f7 f3f7" coords="false" >}}
```

**`mv`**: moves in running text, with piece letters shown as figurines.

```
The game ended {{< mv "16. Qb8+! Nxb8 17. Rd8#" >}}.
```

**`pgn`**: an interactive game viewer ([Lichess PGN Viewer][lpv]), re-themed to
match the site. PGN comments, variations and annotation glyphs are shown.
Give the PGN inline or as a file in the page bundle:

```
{{< pgn caption="Morphy – Duke Karl / Count Isouard, Paris 1858" ply="22" >}}
[White "Paul Morphy"]
1. e4 e5 2. Nf3 d6 {A comment.} ...
{{< /pgn >}}

{{< pgn file="game.pgn" orientation="black" ply="last" moves="bottom" />}}
```

The file form must be self-closed (`/>`). `ply` is the half-move to open on
(or `last`); `moves` is `auto` | `right` | `bottom` | `false`. Without JavaScript the raw PGN is shown.

### Third-party files

- `static/chess/pieces.svg`: pieces by Colin M.L. Burnett, GPLv2+
  (via lichess.org).
- `static/chess/pgn-viewer/`: Lichess PGN Viewer 2.7.3, GPL-3.0-or-later.
  Unmodified `dist/` build from the npm package [`@lichess-org/pgn-viewer`][lpv];
  source at <https://github.com/lichess-org/pgn-viewer>.

[lpv]: https://www.npmjs.com/package/@lichess-org/pgn-viewer

## Menu

Populated from `[[menu.main]]` entries in the site config.

## Example site

See `exampleSite/` for a minimal working configuration. To preview it:

```sh
cd exampleSite
ln -s ../.. themes/personal   # one-time, not committed
hugo server
```

## License

Copyright (C) 2026 Pau Torras

This theme is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation, either version 3 of the License, or (at your option) any later
version. See `LICENSE`.

The bundled Archivo and Fira Mono fonts are under the SIL Open Font License.
