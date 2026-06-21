# Contributing

This repo is a community starter kit for hardening AI coding assistants
against known prompt-injection patterns. Contributions that improve
coverage, fix false positives/negatives, or port the content to new tools
are welcome.

## Reporting a new attack pattern or a bypass

If you find that the current instructions don't mitigate some pattern:

1. Open an issue describing the **category** of the technique and a
   **generalized, non-operational** description of how it works.
2. Please don't post a fully weaponized, ready-to-use prompt in a public
   issue — describe the mechanism (e.g. "instructions hidden in SVG
   `<title>` metadata get read by some tools and followed") so
   maintainers can write a generalized test case and mitigation, without
   the issue itself functioning as a ready-made attack for others.
3. Maintainers will add a corresponding case to `tests/eval-cases.yaml`
   and update `.github/copilot-instructions.md` as needed.

## Proposing changes to the instructions file

- Keep additions general (principles and patterns), not a long enumerated
  blocklist of exact phrases — phrase-matching is trivially bypassed by
  rewording, and an exhaustive phrase list also makes a handy menu for
  attackers. Prefer describing the *mechanism* of an attack category.
- Add or update a case in `tests/eval-cases.yaml` for anything you add.
- Run `tests/run_eval.py` locally before opening a PR.

## Adding support for a new tool

If you port this to a tool not yet covered in
`docs/porting-to-other-tools.md`, please add a section there describing
the file name/location/syntax that tool expects, and open a PR.

## Code of conduct

Be constructive. This repo exists to help people ship safer AI-assisted
code, not to showcase exploits. Issues or PRs that read primarily as
attack demonstrations rather than proposed improvements may be redirected
to a private report instead.
