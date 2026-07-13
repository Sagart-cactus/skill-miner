# Skill Miner

A [Claude Code](https://claude.com/claude-code) skill that mines your past session history to discover which reusable **skills** you — or your whole team — should create, then helps you build and prove the best one.

Every time you correct Claude mid-session ("no, we always sign commits", "you should have used the Makefile"), that correction is a rule the AI gets wrong by default. Your transcript history is full of them, along with repeated commands, rebuilt procedures, and pasted handoff docs. Skill Miner digs them out, verifies them against live sources, and turns them into a prioritized skill catalog.

## What it does

- **Inventories** what's already encoded (existing skills, plugins, `CLAUDE.md`) so it never re-proposes it
- **Indexes** your session transcripts without reading whole files (they can be tens of MB)
- **Hunts high-value signals**: mid-flow corrections, repeated hard requirements, standard command sequences, system topology, silent traps
- **Verifies every fact** against live authoritative sources before encoding it — stale snapshots are the #1 way skills rot
- **Proposes a tiered catalog** (build-first / high-value / nice-to-have / fold-into-existing) with evidence and recurrence counts, stress-tested by an adversarial critique pass
- **Builds and evals the winner** — including "bait" test cases built from your real past corrections

### Team mode

Solo mining has a blind spot: your history only contains *your* corner of the system. Skill Miner includes a **collaborative map-reduce mode** — each teammate mines locally, only a sanitized paraphrase-only findings file leaves their machine, and one maintainer merges. Cross-person corroboration separates real conventions from personal habits, and conflicting findings surface undocumented team divergence. Raw transcripts never leave anyone's machine.

## Installation

### Option 1 — Plugin (recommended)

In Claude Code:

```
/plugin marketplace add Sagart-cactus/skill-miner
/plugin install skill-miner@skill-miner
```

### Option 2 — Manual skill install

Copy the skill into your personal skills directory:

```bash
git clone https://github.com/Sagart-cactus/skill-miner.git
cp -r skill-miner/skills/skill-miner ~/.claude/skills/
```

### Option 3 — Standalone prompt

Not using skills? Paste [skill-mining-prompt.md](skill-mining-prompt.md) directly into a Claude Code session. It's the same method as the skill, phrased as a one-shot prompt.

## Usage

Once installed, just ask:

- *"What skills should we create based on my session history?"*
- *"Go through my past sessions and turn my corrections into rules."*
- *"Build a skill catalog for my team."*

The skill works in phases and checks in with you between them.

## Repository layout

```
skills/skill-miner/SKILL.md   # the skill itself
skill-mining-prompt.md        # standalone prompt version
.claude-plugin/               # plugin + marketplace manifests
```

## Privacy note

Session transcripts contain echoed secrets, tokens, and private context. Skill Miner is designed so raw transcripts **never leave your machine** — in team mode only sanitized, human-reviewed paraphrases are shared, and each contributor is the privacy gate for their own findings file.

## License

[MIT](LICENSE)
