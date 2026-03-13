# Feynman Finder

A Claude Code skill that maps the frontiers of scientific knowledge. Given a research topic, it traces empirical constants, fitted models, and competing theories back to their upstream assumptions — then identifies where the field may have taken a wrong turn. The output is a set of PhD-worthy research directions grounded in genuine gaps in understanding.

> "What I cannot create, I do not understand." — Richard Feynman

## Quick Start

```bash
git clone <this-repo>
cd feynman-finder
claude
```

Then run:

```
/feynman-finder ion evaporation mechanisms in ionic liquid ion sources
```

The skill is auto-discovered from `.claude/skills/` — no installation step needed.

### Install for All Projects

To make the skill available everywhere, copy it to your personal skills directory:

```bash
cp -r .claude/skills/feynman-finder ~/.claude/skills/
```

## What It Does

Given a research topic, Feynman Finder works through five phases:

1. **Scope** — Narrows broad topics to a specific phenomenon (asks you to pick if too broad)
2. **Survey** — Maps governing equations, classifying every parameter as fundamental, derived, or empirical
3. **Trace** — Walks the assumption tree backward from each empirical parameter to find where first-principles derivation broke down
4. **Cluster** — Groups breakdowns by shared root assumptions to find the highest-leverage branch points
5. **Evaluate** — Assesses each branch point: historical context, adjacent field solutions, new tools available
6. **Synthesize** — Generates ranked PhD research directions with concrete attack vectors

It applies thinking frameworks from Feynman, Einstein, Hamming, Kuhn, and Polya to evaluate which problems are worth working on.

## Output

Reports are written to `reports/` as markdown files. Each report includes:

- A landscape overview of the field
- A table of empirical breakdowns (constants, fitted models, competing theories)
- An assumption tree tracing each breakdown to its root cause
- Ranked branch points where the field may have gone wrong
- Concrete PhD research directions with 6-month plans and risk assessments
- Full references (preferring open-access sources)

## Example Topics

```
/feynman-finder lithium dendrite nucleation at solid electrolyte interfaces
/feynman-finder energy cascade in the inertial subrange of isotropic turbulence
/feynman-finder chemo-mechanical degradation at solid-state electrolyte interfaces
```

If the topic is too broad (e.g., "battery chemistry"), the skill will survey the area and ask you to pick a sub-topic before proceeding.

## Repository Structure

```
feynman-finder/
├── .claude/
│   └── skills/
│       └── feynman-finder/
│           └── SKILL.md          # The skill definition (source of truth)
├── reports/                      # Generated research reports
├── research-cache/               # Cached sources and working notes (gitignored)
├── CLAUDE.md                     # Project instructions for Claude Code
└── README.md
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- Web search and fetch permissions (the skill searches for papers, theses, and course materials)

## License

MIT
