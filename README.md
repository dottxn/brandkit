# brandkit

Turns vague brand opinions into a usable strategic backbone for creative work.

Three Claude Code skills (discovery, proposition, concepts) modelled on how real studios work. Each phase earns the next. The canonical output is `BRAND.md`: one file that compresses everything the pipeline produces into a source of truth your team can actually use.

## What it gives you

**`brandkit/BRAND.md`**, the source of truth. It builds up as you run each phase:

| After | BRAND.md contains |
|-------|------------------|
| `/brand-discover` | What we learned: conclusions from research and interview |
| `/brand-proposition` | + What we believe, what we reject, the proposition, the soul |
| `/brand-concepts` | + How it looks and sounds, the signature move, non-negotiables |

The detailed phase files (discovery reports, territory cards, concept directions) live in `brandkit/discovery/`, `brandkit/proposition/`, and `brandkit/concepts/`. BRAND.md is the compressed version, the one you share, reference, and build from.

## Install

```bash
git clone https://github.com/dottxn/brandkit.git ~/.claude/skills/brandkit
cd ~/.claude/skills/brandkit && ./setup
```

## Usage

```
/brand-discover      # Research, observe, challenge
/brand-proposition   # Distill into debatable proposition territories
/brand-concepts      # Explore what it looks, sounds, and feels like
```

Each phase reads the previous phase's output. You can run them standalone, but they're designed to chain.

## How it works

The database trained the method. The skills apply the method.

88 real brands analysed across 11 dimensions: archetypes, positioning scales, creative tensions, visual clusters, voice patterns, anti-patterns. That analysis produced the methodology baked into each skill's instructions. The knowledge base ships alongside so skills can reference specific brands as benchmarks.

The skills don't query the database at runtime. The patterns are the instructions.

## What's in the box

```
brandkit/
├── brand-discover/SKILL.md       # Phase 1: Discovery & immersion
├── brand-proposition/SKILL.md    # Phase 2: Strategy & positioning
├── brand-concepts/SKILL.md       # Phase 3: Creative directions
├── ETHOS.md                      # Philosophy
├── setup                         # Installer
├── bin/
│   ├── brandkit-load-context     # Context assembly utility
│   └── brandkit-browse           # Headless browser for visual research
└── knowledge/
    ├── brands/                   # 88 brands, 11 YAML chunks each
    └── patterns.md               # Methodology patterns extracted from analysis
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- Python 3 (for `brandkit-load-context` and `brandkit-browse`)
- **Optional:** [Playwright](https://playwright.dev/python/) for visual research

```bash
pip3 install playwright && python3 -m playwright install chromium
```

Without Playwright, the skills work fine. WebFetch handles text extraction and the methodology is baked in. With it, the skills can screenshot competitor websites, test responsive layouts, and visually analyse live brands during research. `brandkit-browse` will also use system Chrome if installed, avoiding the Chromium download.
