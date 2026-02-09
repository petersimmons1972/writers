# Writers - Historical Writing Style Research

A standalone research system for studying and applying historical journalist writing styles.

## Purpose

This project captures authentic writing styles of deceased journalists through:
- Comprehensive research corpus collection
- Pattern extraction and analysis
- Actionable writing guidelines
- Validation frameworks

## Structure

```
corpus/
├── ernie-pyle/          # WWII embedded reporter, "The Soldier's Correspondent"
├── edward-murrow/       # CBS broadcast journalist, London Blitz reporter
└── [future writers]/

tools/
├── extract-patterns.md  # Pattern extraction methodology
└── validate-voice.md    # Validation framework
```

## Current Writers

### Ernie Pyle (1900-1945)
- **Specialty**: Embedded combat reporting, human-centered storytelling
- **Known For**: "The worm's eye view", Pulitzer Prize 1944
- **Corpus Status**: 8 samples (Phase 1)

### Edward R. Murrow (1908-1965)
- **Specialty**: Broadcast journalism, crisis reporting
- **Known For**: "This is London" broadcasts, Buchenwald report
- **Corpus Status**: 13 samples (Phase 1)

## Integration

This project is consumed by the [Generals project](../generals/) for operational content creation:
- Writers project = Pure research (corpus, patterns, guidelines)
- Generals project = Operational integration (deployments, XP, missions)

Generals profiles reference writer corpus: `~/projects/writers/corpus/{name}/`

## Philosophy

We honor these journalists by:
1. Collecting extensive authentic samples (not guessing their style)
2. Extracting observable patterns (not mystical "essence")
3. Creating actionable guidelines (not vague principles)
4. Validating against authentic samples (not subjective judgment)

## Current Focus

Creating LinkedIn content about AI topics while honoring authentic historical writing styles. The goal is embodying their voices naturally, with AI detection avoidance as a side benefit.

---

**Project Status**: Active development
**License**: Private
**Created**: 2026-02-09
