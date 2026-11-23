# Avrae Customizations — Repo Instructions

This repo stores custom Avrae Discord bot content: aliases, snippets, and
GVARs. It is structured to match what the
[avrae-autoupdate](https://github.com/1drturtle/avrae-autoupdate) tool
expects, so that auto-update can be wired up later without reorganizing
anything. **Auto-update itself (the GitHub Action, secrets, workflow file)
is intentionally not set up in this repo yet.** Do not add
`.github/workflows/update_avrae.yml` or an `AVRAE_TOKEN` secret unless
explicitly asked to.

## Documentation reference

For all alias/snippet/GVAR code (syntax, available functions, cvars,
draconic expressions, etc.), validate against the official Avrae docs:

https://avrae.readthedocs.io/en/stable/index.html

Do not rely on outside blog posts, Reddit threads, or memory of Avrae
syntax — check the above docs when writing or editing any customization
code. No other documentation source should be used for this.

## Required folder structure

Every collection gets its own folder under `collections/`. Every alias
(including subaliases) gets its own folder containing its `.alias` code
file and a matching `.md` doc file. Snippets live directly under the
collection folder (no subfolder). GVARs live under `gvars/`.

```
avrae-customizations/
├── collections/
│   └── <collection-name>/
│       ├── <alias-name>/
│       │   ├── <alias-name>.alias
│       │   ├── <alias-name>.md
│       │   └── <subalias-name>/
│       │       ├── <subalias-name>.alias
│       │       └── <subalias-name>.md
│       ├── <snippet-name>.snippet
│       └── <snippet-name>.md
├── collections.json
├── gvars/
│   └── <gvar-name>.gvar
└── gvars.json
```

Rules:

- One top-level folder per collection under `collections/`.
- One folder per alias, named identically to the alias. The folder holds
  the `<name>.alias` code and a `<name>.md` doc file for that alias.
- A subalias is a folder nested inside its parent alias's folder,
  following the same `<name>.alias` / `<name>.md` pattern.
- Snippets are flat files directly in the collection folder: a
  `<name>.snippet` code file paired with a `<name>.md` doc file. Snippets
  do not get their own folder.
- GVARs are flat files under `gvars/`, named `<name>.gvar`.
- `collections.json` (repo root) maps each collection folder path to its
  Avrae collection ID, e.g. `{"collections/cool-collection": "COLLECTION-ID"}`.
- `gvars.json` (repo root) maps each GVAR file path to its Avrae GVAR ID,
  e.g. `{"gvars/my-gvar.gvar": "gvar-id"}`.
- Every `.alias` and `.snippet` file must have a same-named `.md` file
  next to it describing what it does.

When creating a new alias, subalias, snippet, or GVAR, always create the
matching files/folders in this structure — never place code files loose
at the repo root or outside this layout.

## Shared images

`images/` (repo root) is a flat, shared folder for any image used by any
alias, snippet, or collection in this repo — it's not scoped to a single
collection. Files there are named descriptively, e.g.
`triboar-book-club-collection-cover.webp`.

```
avrae-customizations/
└── images/
    └── <descriptive-name>.<ext>
```

Rules:

- Any alias/snippet in any collection may reference any file in
  `images/` — it is shared across the whole repo, not duplicated per
  collection.
- Images are referenced **only** via their `raw.githubusercontent.com`
  URL, e.g.:
  `https://raw.githubusercontent.com/cloudedturtle/avrae-customizations/main/images/<file>`
  Never use a relative path, a `github.com/.../blob/...` URL, or any
  other host.
- Do not nest `images/` under `collections/` — it stays a single
  top-level folder.

## Creating new aliases

Before writing a new alias (or subalias/snippet), check its proposed
name and functionality against **both**:

1. **Aliases already in this repo** — across all collections, not just
   the one it's going into.
2. **Avrae's own built-in/core commands** — the commands that ship with
   the bot itself (`!check`, `!save`, `!attack`, `!cast`, `!i`, `!r`,
   `!g`, etc.), not just other custom aliases. Confirm via the Avrae
   docs (cheatsheets and command references) and/or `!help <name>` in
   Discord, which reports whether a command by that name already
   exists.

Look for:

- **Naming conflicts** — a new alias/command name that collides with,
  or is easily confused with, an existing custom alias or a built-in
  command.
- **Overlapping functionality** — logic that substantially duplicates
  what an existing alias (or a built-in command) already does.
- **Shareable logic** — if the new alias needs code that's identical or
  near-identical to part of an existing one, prefer extracting it into
  a GVAR module (Avrae's `using()` import mechanism — see the
  [Aliasing API docs](https://avrae.readthedocs.io/en/stable/aliasing/api.html#using-imports))
  over copy-pasting it into both. Note this requires the GVAR to be
  created in Avrae first, with its ID added to `gvars.json`.

Flag anything found before writing the new alias's code, rather than
creating it in isolation.
