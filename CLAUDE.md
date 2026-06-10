# CLAUDE.md

Guidance for working in this repository.

## What this is

`elisp-helpers` (nix-elisp-helpers) is a Nix library of utility functions for
inspecting and fetching Emacs Lisp packages. It uses
[talyz/fromElisp](https://github.com/talyz/fromElisp) to parse S-expressions.

Public API (exported via `lib` in `flake.nix` / `default.nix`):

- `parseCask` — parse a `Cask` file into an attribute set
- `parseMelpaRecipe` — parse a MELPA-style recipe string
- `parseElpaPackages` — parse an ELPA package list
- `parsePkg` — parse a `*-pkg.el` file
- `fetchTreeFromMelpaRecipe`, `flakeRefAttrsFromMelpaRecipe`, `flakeRefUrlFromMelpaRecipe` — fetch/reference helpers
- `expandMelpaRecipeFiles` — expand `:files` spec in a MELPA recipe

## Fork / branch model

This is a fork of `emacs-twist/elisp-helpers`.

- **`master`** — a pure mirror of `upstream/master`. Do **not** commit here;
  only fast-forward it from upstream.
- **`develop`** — personal integration branch carrying all local changes.
  Rebase onto `master` when upstream moves.
- **topic branches** (`fix/...`, `feat/...`, `docs/...`) — branched off
  `master`, one change each, kept PR-ready for upstream. Merged into `develop`.

`upstream` remote: `https://github.com/emacs-twist/elisp-helpers`.

## Layout

| Path    | Contents                                           |
|---------|----------------------------------------------------|
| `lib/`  | One function per file; `default.nix` exports all   |
| `test/` | Per-function `test-*.nix` files + fixture data     |

## Commands

Unit tests (pure evaluation):

```sh
make test
# or individually:
nix-instantiate --eval --strict --json test/test-recipe.nix | jq
```

## Conventions

- Nix files follow `nixfmt-rfc-style`.
- Each function in `lib/` lives in its own file named after the function.
