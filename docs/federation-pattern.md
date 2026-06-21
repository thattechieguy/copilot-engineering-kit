# Federating this across many repos (platform-team pattern)

This repo works fine adopted one-off by a single team. If you're a
platform or security team trying to make this the **default** for every
new repo across an org, here's the pattern, summarized.

## The shape of it

1. **A registry repo** (separate from this one) holds the
   organization's approved instruction bundles, versioned and signed.
   This `copilot-skill-guard` repo can be vendored in as the starting
   bundle.
2. **A distribution mechanism** (a GitHub App, Action, or webhook
   listener on repo-creation events) pulls the current signed bundle and
   commits it into every newly created repo, e.g. under
   `.github/copilot-instructions.md` and `.github/instructions/`.
3. **A CI check in each repo** re-fetches and re-verifies the signed
   bundle on every PR, and fails the build if the in-repo copy has
   drifted from the registry's signed version. This is what makes the
   baseline practically hard to silently edit away, since GitHub doesn't
   have a true "read-only file" concept — protection comes from branch
   rules + required reviewers + this verification check working
   together, not from file permissions alone.
4. **An exception process** for teams with a genuine reason to deviate,
   so the system doesn't get quietly forked the first time someone hits
   a real edge case.

## Minimal version, if you don't want to build all of that yet

- Mark this repo as a GitHub **template repository** at the org level.
- New repos created "from template" inherit these files by default.
- This is weaker than the full pattern above (nothing stops someone
  editing or deleting the file after creation), but it's a one-setting
  change and gets you a sane default immediately.

## A fuller writeup

The reasoning behind each piece (why signing matters, why pull-based
verification beats a static injected copy, how to structure the registry
repo itself, and how to wire a repo-creation webhook) is worth writing up
as a full internal design doc tailored to your org's GitHub setup
(GitHub Enterprise vs. Enterprise Cloud, existing GitHub Apps, etc.) — the
right implementation details depend on specifics like your org's app
permissions model and CI provider.
