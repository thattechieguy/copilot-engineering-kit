# Porting these instructions to other AI coding tools

The content in `.github/copilot-instructions.md` is tool-agnostic in
substance — it's written as plain rules an assistant should follow. The
only Copilot-specific parts are the file location and the `applyTo` front
matter syntax used for scoped files. To port:

## Claude Code
Copy the body of `.github/copilot-instructions.md` into a `CLAUDE.md` at
the repo root. Claude Code loads this automatically as project context.
Scoped instructions (the `applyTo` files) can become sections in the same
`CLAUDE.md`, or separate files referenced from it, since Claude Code does
not currently use glob-based auto-loading the way Copilot does.

## Cursor
Copy into `.cursorrules` or `.cursor/rules/*.mdc` depending on your Cursor
version — check current Cursor docs, since this has changed across
releases.

## Codex-based / OpenAI tools
Check the specific tool's documentation for its project-instructions
mechanism (naming and loading conventions vary and change frequently).
The rule content itself in this repo is not tied to any vendor and should
transfer directly.

## General principle when porting
Whatever the file name or location, the goal is the same: get the
assistant to treat (a) the developer's live chat instructions and (b)
this instructions file as the only sources of "things to obey," and
everything else it reads (code, comments, tickets, docs, web content) as
data to analyze rather than commands to follow.
