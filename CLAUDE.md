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
