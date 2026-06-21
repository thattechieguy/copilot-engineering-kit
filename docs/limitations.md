# Limitations — read this before relying on this repo

This repo provides **instruction-level mitigations** for a known family of
prompt-injection patterns aimed at AI coding assistants (GitHub Copilot,
and similar tools that read repo-level custom instructions). It is useful,
but it is not a security boundary, and it should not be marketed or relied
on as one. Some specific caveats:

## 1. Instructions are guidance, not sandboxing

Custom instructions shape model behavior probabilistically. They do not
enforce anything the way a permission system, network policy, or
sandboxed execution environment does. A sufficiently novel or obfuscated
attack may still succeed even with this file in place. Treat this as one
layer in defense-in-depth, alongside:
- Least-privilege scopes for any AI agent with repo/CI/infra access
- Required human review on security-sensitive diffs (auth, secrets,
  permissions, data access)
- Static analysis / secret scanning / dependency scanning in CI
- Logging and audit trails for AI-assisted changes

## 2. Coverage is necessarily incomplete

The categories addressed here (direct override, structured-output /
schema injection, roleplay framing, combined techniques, multi-turn
manipulation) reflect commonly documented patterns at the time this repo
was written. New techniques will appear. This repo is meant to be a
living baseline — see `CONTRIBUTING.md` for how to propose new patterns
and mitigations as they're identified.

## 3. Different tools honor instructions differently

GitHub Copilot's handling of `.github/copilot-instructions.md` and
`.github/instructions/*.instructions.md` (with `applyTo` front matter) is
specific to Copilot and may change as the product evolves — check
GitHub's current documentation, since instruction-file behavior is a
product feature that gets updated independently of this repo. Other
tools (Claude Code, Cursor, Codex-based tools, etc.) use different
mechanisms (`CLAUDE.md`, `.cursorrules`, etc.) and would need an adapted
version of this content. See `docs/porting-to-other-tools.md`.

## 4. This does not replace verifying generated output

Even with strong instructions, AI-generated code should still go through
normal review, testing, and security scanning before merging. This repo
reduces the chance the assistant gets steered into actively malicious
output; it does not guarantee correctness, security, or that generated
code is free of bugs.

## 5. No warranty

This is a community starter kit, provided as-is, for people to adapt.
There is no guarantee it prevents any specific attack. If you find a
bypass, please open an issue (see `CONTRIBUTING.md`) so the patterns can
be documented and addressed — responsibly, not as a how-to for others.
