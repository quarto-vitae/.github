<div align="center">
<img src="https://raw.githubusercontent.com/quarto-vitae/quarto-vitae.github.io/main/images/vitae-hex.svg" width="120" alt="Quarto Vitae hex logo">

# Quarto Vitae

Quarto extensions for writing CVs, résumés, and biographies.

[quarto-vitae.github.io](https://quarto-vitae.github.io/)
</div>

Every template here shares the same entry syntax: a listing is a table (written
by hand, or printed by a code cell) inside a div with a `style`, such as

```markdown
::: {.entries style="detailed"}
| what             | with                | when      |
|------------------|---------------------|-----------|
| Ph.D. in Physics | University of Paris | 1891-1895 |
:::
```

Because the syntax is shared, switching designs is a one-line change to
`format:` — the same document renders in whichever of the templates below you
point it at.

## Templates

| Template | Design | Install |
|---|---|---|
| [**awesomecv**](https://github.com/quarto-vitae/awesomecv) | [Awesome-CV](https://github.com/posquit0/Awesome-CV) by Byungjin Park — a LaTeX CV with a matching cover letter format. | `quarto use template quarto-vitae/awesomecv` |
| [**hyndman**](https://github.com/quarto-vitae/hyndman) | The CV style used by [Rob J Hyndman](https://github.com/robjhyndman/CV) — a shaded header box and coloured sans-serif section headings. | `quarto use template quarto-vitae/hyndman` |
| [**latexcv**](https://github.com/quarto-vitae/latexcv) | All seven designs from [jankapunkt/latexcv](https://github.com/jankapunkt/latexcv), from a plain centred résumé to a tinted sidebar — one repo, seven `format:` values. | `quarto use template quarto-vitae/latexcv` |

Rendering these needs a LaTeX installation (`quarto install tinytex` if you
have none). Each repository's README covers its YAML options, listing styles,
and colour/font customisation in full.

## Creating a new template

Templates are built on [**curriculum**](https://github.com/quarto-vitae/curriculum),
the Lua filter that every template above embeds. It is the shared machinery
that lets a `.entries` table become a CV listing in any format, and it's what
"teaches" an ordinary Quarto extension to speak the vitae entry syntax:

- An author writes a listing as a table, or a code cell prints one and tags it
  with `#| vitae: {style: ..., fields: ...}`.
- `curriculum` finds that data, applies any `fields` renaming, and hands each
  entry to your template's handler for that style — one small pandoc template
  per listing shape (`entries/detailed.tex`, `entries/brief.tex`, ...).
- Everything else — an author's YAML header, section headings, colours — is
  ordinary Quarto format code with no filter involvement.

So building a new template means writing the usual Quarto extension (a
document class, a pandoc template, fonts) plus a handler per listing style you
support, and embedding `curriculum` into it with:

```bash
quarto add quarto-vitae/curriculum --embed yourcv
```

The full guide — `_extension.yml` conventions, resolving and overriding
handlers, style-naming conventions, and the embedding workflow in detail — is
at [quarto-vitae.github.io/creating-templates](https://quarto-vitae.github.io/creating-templates.html),
with [awesomecv](https://github.com/quarto-vitae/awesomecv) as a working
template to read alongside it.
