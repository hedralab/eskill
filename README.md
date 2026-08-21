# eSkill — Meta-skill: build top-tier Agent Skills

eSkill is the **skill for creating skills** — a production workflow distilled from the
official [Agent Skills spec](https://agentskills.io/specification), Anthropic's
[skill-creator](https://github.com/anthropics/skills) eval loop, and real lessons from
building/shipping egram + the eSeed project.

## What it gives you

- **12-pillar production process**: Core (agentskills.io spec) · UX (Apple HIG) ·
  Validation · Docs & Traps · Ops (12-Factor) · Eval (skill-creator) · Writing (Apple) ·
  Growth (AARRR) · Commercial · Consulting (SPIN + Mom Test) · Market (JTBD) ·
  **Simulation & Variable Scan** (put yourself in the user's shoes → simulate 5 scenarios →
  scan 6 variable groups before writing)
- **Numbered-file workflow (0→n)**: every build generates 0-goal → 1-market → 2-plan →
  3-SKILL.md → 4-eval → 5-check + docs/ — state on disk, review layer by layer
- **Spec rules**: frontmatter (name/description/license/compatibility/metadata),
  progressive disclosure (<500 lines), 1-level references
- **Eval loop**: forward-test with real-looking prompts, qualitative + quantitative review
- **Naming** (Apple-style e-family: `e` + one word — eSkill, eSeed, egram)
- **Validator**: `scripts/validate-skill.py` — catches broken frontmatter, bad names,
  broken refs, oversized SKILL.md, and leaks (`--leak --brand`)

## Quickstart (3 prompts)

1. `Create a skill that <does X> and check it works` — eSkill interviews you, then builds it
2. `Improve this skill: <path>` — eSkill applies the eval loop and fixes it
3. `Validate this skill: <path> [--leak]` — run the validator

## Structure

```
eskill/
├── SKILL.md                     # 12-pillar process + golden rules (Vietnamese — author-facing)
├── README.md                    # This file (English — public-facing)
├── LICENSE                      # Use-only (custom)
├── RELEASE-NOTES.md             # changelog (Keep a Changelog + semver)
├── .version-bump.json           # current version + files to sync on bump
├── CODE_OF_CONDUCT.md           # contributor covenant
├── .gitignore · .pre-commit-config.yaml
├── agents/openai.yaml           # marketplace/UI metadata
├── .claude-plugin/ · .codex-plugin/ · .cursor-plugin/   # plugin manifests
├── .github/                     # FUNDING + issue/PR templates
├── assets/                      # icon
├── template/SKILL.md            # copy-ready skill skeleton (full frontmatter)
├── references/
│   ├── spec-rules.md            # agentskills.io spec rules
│   ├── naming.md                # Apple-style e-family naming
│   ├── sales-discovery.md       # SPIN + Mom Test (step-0 interview)
│   ├── top1-benchmark.md        # Pillar 2: find + verify a top-1 benchmark
│   ├── simulation-variables.md  # Pillar 12: simulate + scan variables
│   ├── numbered-output.md       # 0→n file workflow + docs/ (state on disk)
│   ├── eval-loop.md             # test → evaluate → fix loop
│   ├── test-prompts-template.md # 5 test-prompt types
│   ├── rubric.md                # pre-registered pass/fail rubric
│   ├── docs-driven.md           # docs = hard gate 100%
│   ├── 12-factor-skills.md      # maintainable skill ops
│   ├── apple-writing.md         # concise SKILL.md writing
│   ├── openai-yaml.md           # agents/openai.yaml guide
│   ├── checklist-thuong-mai.md  # commercialization + safety checklist
│   ├── market-research.md       # Pillar 11: research before build
│   └── ban-tren-github.md       # Pillar 9: sales funnel — execute via ehub/egram
├── examples/echeck/             # complete reference skill
└── scripts/
    ├── validate-skill.py        # validator: --leak --brand "a,b"
    └── eval-skill.py            # eval harness: test set + --verify
```

## Release

Version: `2.2.1` — see [RELEASE-NOTES.md](RELEASE-NOTES.md).
Process: edit → bump `.version-bump.json` → update RELEASE-NOTES → `gh release create vX.Y.Z`
(details: `references/ban-tren-github.md`).

## Install

Recommended — one command via [skills.sh](https://skills.sh):

```bash
npx skills add hedralab/eskill
```

Claude Code — plugin marketplace:

```
/plugin marketplace add hedralab/eskill
/plugin install eskill
```

Manual — copy the folder into your agent skills dir:

```bash
cp -RL eskill ~/.deepseek/skills/eskill    # DeepSeek TUI (resolve symlinks)
# or ~/.claude/skills/eskill
# or ~/.codex/skills/eskill
```

**⚠️ Symlink:** in this repo `skills/eskill` is a symlink → `~/.deepseek/.agents/skills/eskill`.
When copying/packaging, use `cp -RL` (or `tar -h`) to resolve it — plain `cp -R` copies the
symlink itself and breaks the package on other machines.

## License

**Use-only.** See [LICENSE](LICENSE). You may USE this skill for personal or internal
purposes. Modification, redistribution, and commercial use are NOT permitted; all other
rights are reserved.
