# AGENT-README

> Orientation for AI coding agents working in this repo. Human docs: README.md.

## Type

scripts

## Purpose

Pure-shell terminal tab title, status & task manager with theme support: tab titles, colors, status text, urgency levels, emojis, and full themes from the shell — plus per-tab todos, time-in-state reports, history search, and asciinema recording. Works with iTerm2, Ghostty, Kitty, WezTerm, Alacritty, and more.

## Stack

POSIX shell libraries (`lib/`) + bash/zsh adapters (`shell/`) + thin CLI wrappers (`bin/`); Bash 4.0+ / Zsh 5.0+, no external dependencies; a small Rust helper lives in `rust/`.

## Dev mode

```bash
make install                     # commands -> ~/.local/bin, libs -> ~/.local/share/tabbing-on/
eval "$(tabbing-init zsh)"       # add to .zshrc (or tabbing-init bash)
```

## Ports / URLs

- none (library/CLI)

## Tests

```bash
make test        # cargo test in rust/; shell side has no test framework — manual via bin/demo-runner
```

## Gotchas

- Only `lib/render.sh` is sourced at shell init to keep prompt hooks fast — heavy libs load on demand via `bin/` wrappers.
- DC mode (`TABBING_ON_DC_MODE=1`, direnv-config integration) stores state per-directory, not per-tab: entering a directory restores its last title/status; `tabbing-off` clears.
- Auto-sets `CLAUDE_CODE_DISABLE_TERMINAL_TITLE=1` so Claude Code doesn't clobber tab titles; Claude Code statusline bridge via `tabbing-on --claude`.
