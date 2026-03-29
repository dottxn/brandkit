# brandkit

Claude Code skills for brand design. Three phases — discovery, proposition, concepts — modelled on how real studios work.

Ships with 88 brands analysed across 11 dimensions. The methodology is baked into the skills. The knowledge base is the R&D.

## Install

```bash
git clone https://github.com/dottxn/brandkit.git ~/.claude/skills/brandkit
cd ~/.claude/skills/brandkit && ./setup
```

## Usage

Open Claude Code in any project and run the skills in sequence:

```
/brand-discover      # Research, observe, challenge
/brand-proposition   # Distill, position, articulate
/brand-concepts      # Explore visual directions, voice, content
```

Each phase produces files in `brandkit/` in your working directory. Each phase reads the previous phase's output. You can run them standalone, but they're designed to chain.

### `/brand-discover`

Structured brand immersion. Stakeholder interview (5-7 adaptive questions), desk research, competitive landscape, observation synthesis across 4 lenses (product, audience, experience, landscape), and challenges framed as questions.

Works on existing brands (audit) and new brands (explore).

**Output:** `brandkit/discovery/`

### `/brand-proposition`

Strategic distillation. Finds themes in the discovery, builds pillars, maps competitive positioning, and arrives at the reframe — the single insight that changes how you see the brand.

For new brands, presents 2-3 genuinely different strategic directions.

**Output:** `brandkit/proposition/`

### `/brand-concepts`

Creative direction exploration. Translates the proposition into visual worlds, voice directions, content ideas, and applied moments. Produces directions — not final territories, but openings that a team can develop.

**Output:** `brandkit/concepts/`

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

### Knowledge

88 brands across 17 categories. Each brand has up to 11 YAML chunks:

| Chunk | What it captures |
|-------|-----------------|
| `positioning` | Category, archetypes, positioning scales, price tier |
| `soul` | Feels like, core belief, creative tension, decision filter, what would break it |
| `voice` | Personality, tone traits, anti-traits, guardrails |
| `visual-dna` | Colours, typography, 19 visual tags, composition logic |
| `visual-language` | Photography, graphic language, type treatment, layout, trend posture |
| `competitive` | Competitors, visual clusters, strategic cluster, norms broken |
| `strategy` | Purpose, mission, vision, values |
| `insights` | Learned insights, what nobody copies |
| `anti-patterns` | Visual, strategic, tonal, cultural anti-patterns |
| `visual-reasoning` | Type logic, colour logic, composition philosophy |
| `references` | Source URLs and evidence |

### How it works

The skills don't query the knowledge base at runtime. The methodology — positioning scales, soul frameworks, competitive patterns, visual clusters, anti-pattern categories — is baked into the skill instructions from analysing 88 brands. The knowledge ships alongside so you can reference specific brands when the skills need benchmarks.

`bin/brandkit-load-context` assembles chunks for specific tasks, respecting token budgets defined in `knowledge/brands/_retrieval-rules.yaml`.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- Python 3 (for `brandkit-load-context` and `brandkit-browse`)
- **Optional:** [Playwright](https://playwright.dev/python/) for visual research

```bash
pip3 install playwright && python3 -m playwright install chromium
```

Without Playwright, the skills work fine — WebFetch handles text extraction and the methodology is baked in. With it, the skills can screenshot competitor websites, test responsive layouts, and visually analyse live brands during research. `brandkit-browse` will also use system Chrome if installed, avoiding the Chromium download.

Browser approach inspired by [gstack](https://github.com/anthropics/gstack).
