# Writer Profiles Research Corpus System - Design Document

**Date**: 2026-02-09
**Status**: Approved for Implementation
**Approach**: Research Corpus + Pattern Extraction (Approach 1)

---

## Executive Summary

This design creates a **standalone research system for studying and applying historical journalist writing styles**. The system extracts observable patterns from authentic samples, creates actionable guidelines, and validates output authenticity.

**Core Philosophy:**
- Honor deceased journalists by studying their actual work (not guessing their style)
- Extract observable patterns (not mystical "essence")
- Create actionable guidelines (not vague principles)
- Validate against authentic samples (not subjective judgment)

**Primary Goal:** Create content that authentically embodies historical writing styles while discussing modern topics (AI)

**Secondary Goal:** AI detection avoidance (side benefit, not primary optimization target)

**Key Insight from Testing:** Topic (AI) matters more than style for AI detection. Writing about AI in Pyle's style still scores 80-100% AI, but authentically matches his voice patterns.

---

## Section 1: System Architecture & Components

The journalist profile system has **four core components** that work together:

### 1. Research Corpus (what we collect)
- Authentic writing samples from the journalist's actual work
- Minimum 10 samples, target 50+ samples per journalist
- Diverse content types (combat reports, features, broadcasts, personal letters)
- Organized in `/journalists/{name}-writing-samples.md`
- Each sample includes: date, context, publication, full text

### 2. Pattern Library (what we extract)
- Voice markers: signature phrases, rhythms, sentence structures
- Structural patterns: how they open/close, transition, build arguments
- Topic approaches: how they handle different subject matter
- Behavioral markers: what they emphasize, what they avoid
- Organized in `/journalists/{name}-patterns.md`

### 3. Writing Guidelines (how we apply)
- Actionable rules derived from patterns ("DO this, DON'T do that")
- Organized by strength: universal rules vs. context-dependent
- Priority system: which patterns matter most for authenticity
- Anti-patterns: things that break their voice
- Organized in `/journalists/{name}-guidelines.md`

### 4. Validation Framework (how we verify)
- Side-by-side comparison with authentic samples
- Pattern checklist scoring (did we hit key markers?)
- Voice consistency testing (does it sound like them?)
- Educational value verification (does it serve the audience?)
- Results tracked in `/journalists/{name}-validation-history.md`

**The Flow:**
```
Authentic samples → Pattern extraction → Guidelines → Content generation → Validation → Refinement
```

Each journalist gets their own complete set (corpus + patterns + guidelines + validation history).

---

## Section 2: Project Structure (Hybrid Architecture)

The **writers project** is a standalone research system that the generals project consumes.

### Directory Structure

```
~/projects/writers/                 # New standalone project
├── README.md                       # Framework documentation
├── docs/
│   └── plans/
│       └── 2026-02-09-writer-profiles-research-corpus-design.md
├── corpus/
│   ├── ernie-pyle/
│   │   ├── samples.md             # Authentic writing samples
│   │   ├── patterns.md            # Extracted patterns
│   │   ├── guidelines.md          # Writing rules
│   │   └── validation-history.md  # Test results
│   ├── edward-murrow/
│   │   ├── samples.md
│   │   ├── patterns.md
│   │   ├── guidelines.md
│   │   └── validation-history.md
│   └── [future writers]/
└── tools/
    ├── extract-patterns.md        # Pattern extraction methodology
    └── validate-voice.md          # Validation framework

~/projects/generals/                # Existing operational system
├── profiles/
│   ├── ernie-pyle.md              # References ~/projects/writers/corpus/ernie-pyle/
│   │                              # Contains: XP, deployments, ribbons, missions
│   └── edward-murrow.md           # Same pattern
└── [rest of generals system]
```

### Sample Entry Format

In `~/projects/writers/corpus/{name}/samples.md`:

```markdown
# {Name} - Writing Samples

## Sample 001: [Title/Description]

**Date**: [Original publication date]
**Context**: [Where published, what was happening]
**Type**: [Combat report / Feature / Broadcast / Letter]
**Word Count**: [approximate]
**Source**: [URL or citation]

---

[FULL TEXT OF AUTHENTIC SAMPLE]

---

**Patterns Observed**:
- [Specific pattern with line number references]
- [Another pattern with examples]
```

### Corpus Collection Target

- Phase 1 (Foundation): 10-15 samples ✓ *Pyle: 8, Murrow: 13*
- Phase 2 (Breadth): 25-40 total samples
- Phase 3 (Depth): 50+ total samples

### Integration Model

- **Writers project** = Pure research (corpus, patterns, guidelines)
- **Generals project** = Operational integration (deployments, XP, missions)
- Generals profiles link to writers corpus: `See ~/projects/writers/corpus/{name}/ for writing style research`
- Deployments tracked in generals (XP, ribbons, missions)
- Style research tracked in writers (patterns, validation)

---

## Section 3: Pattern Extraction Process

Pattern extraction transforms authentic samples into **actionable writing guidelines**. It's the bridge between "I know it when I see it" and "I can replicate it."

### The Four-Layer Extraction

**Layer 1: Structural Patterns** (What can you count?)
- Sentence length distribution (average, range, fragments %)
- Paragraph structure (1-sentence paragraphs frequency, average paragraph length)
- Rhythm patterns (long-short-short vs. consistent length)
- Opening/closing techniques (how do they start/end pieces?)
- Transitional devices (how do they move between ideas?)

*Example from Pyle:*
- 23% one-sentence paragraphs (vs. typical 5-8%)
- Sentence length range: 3-47 words (high variance)
- Frequent compound "and" chains (3+ clauses)

**Layer 2: Voice Markers** (What makes it sound like them?)
- Signature phrases (Murrow: "This is London" / Pyle: "I don't know")
- Pronoun usage (Pyle: heavy "you", Murrow: heavy "I")
- Qualifiers and hedges (Pyle: "maybe", "I think", "probably")
- Direct address patterns (when/how they speak to reader)
- Tonal consistency (formal vs. conversational)

*Example from Murrow:*
- Opens 90% of broadcasts with location ("This is London")
- Closes 95% with "Good night, and good luck"
- Uses "There are..." parallelism for emphasis

**Layer 3: Content Patterns** (What do they show/tell?)
- Observation types (physical details vs. emotional states vs. abstract concepts)
- Conflict handling (do they resolve arguments? show both sides?)
- Source attribution (named sources vs. anonymous vs. personal observation)
- Technical detail level (specific numbers? vague descriptions?)
- Emotional range (anger, sadness, hope, confusion - how expressed?)

*Example from Pyle:*
- Concrete physical observations: 80% of descriptive content
- Names people even when unclear on details ("I think it's Halsey")
- Admits confusion freely ("I don't understand what they're building")
- Shows unresolved conflict (arguments continue tomorrow)

**Layer 4: Anti-Patterns** (What do they NEVER do?)
- Forbidden phrases (AI-generated markers)
- Structural taboos (perfect parallel structure)
- Tonal violations (clinical detachment for Pyle, casual tone for Murrow)
- Content mistakes (summarizing at end, meta-commentary)

*Example anti-patterns:*
- ❌ "Here's where it gets interesting" (both Pyle and Murrow)
- ❌ Perfect three-point lists (too structured for Pyle)
- ❌ Casual slang in crisis reporting (violates Murrow formality)

### Extraction Workflow

```
1. Read authentic sample
   ↓
2. Count structural elements (sentence length, paragraph structure)
   ↓
3. Mark voice markers (signature phrases, pronouns, qualifiers)
   ↓
4. Categorize content (physical vs. abstract, resolved vs. unresolved)
   ↓
5. Note anti-patterns (what's conspicuously absent?)
   ↓
6. Document in {name}-patterns.md
```

### Pattern Priority System

- **Universal** (always apply): Voice markers, anti-patterns
- **Context-dependent** (apply when appropriate): Structural patterns, content patterns
- **Experimental** (test and validate): New patterns discovered during writing

---

## Section 4: Guidelines Application System

Once patterns are extracted, we need a **system for applying them during content creation**. Guidelines bridge the gap between analysis and writing.

### The Three-Tier Guideline System

**Tier 1: Non-Negotiable Rules** (Break these = breaks voice)
- Anti-patterns (never do these)
- Signature voice markers (always include some)
- Tonal boundaries (stay within their emotional range)

*Example for Pyle:*
- NEVER: Clean summary conclusions
- ALWAYS: Include physical observations in every scene
- TONE: Conversational witness, never clinical analyst

**Tier 2: Strong Patterns** (Use frequently, not universally)
- Structural rhythms (vary sentence length, use fragments)
- Content preferences (concrete over abstract, show conflict)
- Opening/closing techniques (how they start/end)

*Example for Pyle:*
- FREQUENT: One-sentence paragraphs for impact
- PREFER: Unresolved conflicts over neat resolutions
- OPENINGS: Start with immediate physical observation

**Tier 3: Contextual Flourishes** (Apply when appropriate)
- Signature phrases (used sparingly to avoid parody)
- Specific techniques (compound "and" chains, admitted ignorance)
- Emotional beats (when to show confusion, frustration, wonder)

*Example for Pyle:*
- SPARINGLY: "I don't know" admissions (powerful but overuse diminishes)
- WHEN APPROPRIATE: Second-person address ("You can feel...")
- EMOTIONAL: Show exhaustion through physical details, not stated feelings

### Application Workflow

```
1. Draft content normally
   ↓
2. Apply Tier 1 (check all non-negotiables)
   ↓
3. Apply Tier 2 (strengthen 3-5 strong patterns)
   ↓
4. Apply Tier 3 (add 1-2 contextual flourishes)
   ↓
5. Read aloud (does it sound like them?)
   ↓
6. Validate against authentic samples
```

### The Checklist Approach

Each writer gets a writing checklist stored in `{name}-guidelines.md`:

```markdown
## Pre-Flight Checklist (Tier 1)
- [ ] No clean summary conclusions
- [ ] No perfect parallel structure
- [ ] Physical observations present
- [ ] Tonal consistency maintained

## Strong Patterns (Tier 2 - hit 3+)
- [ ] Varied sentence length (fragments + compounds)
- [ ] One-sentence paragraphs present
- [ ] Concrete details over abstractions
- [ ] Unresolved conflicts shown

## Flourishes (Tier 3 - hit 1-2)
- [ ] Signature voice marker included
- [ ] Admitted ignorance/uncertainty
- [ ] Second-person address used
- [ ] Compound "and" chain present
```

**Priority System:** If you can only do one thing, do Tier 1. If you have time for polish, add Tier 3.

---

## Section 5: Validation Framework

Validation answers: **"Does this actually sound like them?"** We need objective measures beyond subjective judgment.

### Four Validation Methods

**Method 1: Pattern Matching Score**

Compare generated content against extracted patterns using a scoring rubric.

*Scoring System:*
- Tier 1 (Non-negotiables): 40 points (10 points each, typically 4 rules)
- Tier 2 (Strong patterns): 40 points (5 points each, hit 8 of 12)
- Tier 3 (Flourishes): 20 points (10 points each, hit 2 of 6)
- **Passing score: 80/100** (acceptable voice authenticity)

*Example Pyle Validation:*
```
Tier 1 (40 pts):
✓ No summary conclusions (10)
✓ No parallel structure (10)
✓ Physical observations (10)
✓ Tonal consistency (10)

Tier 2 (40 pts):
✓ Varied sentence length (5)
✓ One-sentence paragraphs (5)
✓ Concrete details (5)
✓ Unresolved conflicts (5)
✓ Admitted ignorance (5)
✓ Physical exhaustion (5)
✓ Compound sentences (5)
? Abstract concepts present (0) - should be minimal

Tier 3 (20 pts):
✓ Second-person address (10)
✓ "I don't know" admission (10)

TOTAL: 95/100 - Strong Pyle voice
```

**Method 2: Side-by-Side Comparison**

Place generated content next to authentic sample, check for:
- Rhythm similarity (read both aloud, do they flow similarly?)
- Tonal consistency (same emotional register?)
- Vocabulary level (similar complexity?)
- Structural resemblance (paragraph length, sentence variety?)

*Comparison Checklist:*
```
Read both aloud:
- [ ] Similar rhythm/pacing
- [ ] Similar vocabulary complexity
- [ ] Similar emotional tone
- [ ] Similar paragraph structure
- [ ] Similar use of white space
```

**Method 3: Blind Testing**

Mix generated content with authentic samples, ask readers to identify which is which.

*Test Protocol:*
1. Select 3 authentic samples (300-500 words each)
2. Generate 3 new pieces (same length, similar topics)
3. Randomize order, remove attribution
4. Ask 5+ readers to identify authentic vs. generated
5. **Target: <70% accuracy** (if readers can't reliably tell, voice is authentic)

**Method 4: AI Detection (Secondary)**

Use AI detectors NOT as primary validation but as secondary signal.

*Why secondary?*
- Topic matters more than style (AI content triggers detection)
- False positives on authentic writing (Pyle samples score 99% human)
- False negatives on poor imitations (can fool detector but not humans)

*How to use:*
- Baseline: Test authentic samples (establishes floor)
- Compare: Test generated content
- Expect: Generated will score worse (especially on AI topics)
- Accept: If pattern score is high (80+) but AI score is low, trust pattern score

### Validation Workflow

```
Generate content
   ↓
Method 1: Pattern Matching Score (required)
   ↓
   Pass (80+)? → Method 2: Side-by-Side (qualitative check)
   Fail (<80)? → Revise and retest
   ↓
Method 2 passes? → Method 3: Blind Test (if publishing)
Method 2 fails? → Identify specific patterns missing
   ↓
Optional: Method 4 (AI detection for curiosity)
   ↓
Document results in {name}-validation-history.md
```

### Record Keeping

Each validation creates an entry in `validation-history.md`:

```markdown
## Validation: [Content Title] (YYYY-MM-DD)

**Pattern Score**: 85/100
- Tier 1: 40/40
- Tier 2: 35/40 (missing: compound sentences)
- Tier 3: 10/20 (only 1 flourish present)

**Side-by-Side**: Pass (similar rhythm, tone consistent)

**Blind Test**: Not conducted (draft stage)

**AI Detection**: 78% AI (expected due to AI topic)

**Outcome**: PASS - Voice authentic, AI score expected
**Action**: None needed
```

---

## Section 6: Integration with Generals System

The writers project (research) and generals project (operations) work together. Writers provides the **style DNA**, Generals provides the **deployment engine**.

### Integration Architecture

```
~/projects/writers/              (Style Research)
├── corpus/{name}/
│   ├── samples.md              ← Authentic samples
│   ├── patterns.md             ← Extracted patterns
│   ├── guidelines.md           ← Writing rules
│   └── validation-history.md   ← Test results

~/projects/generals/             (Operational System)
├── profiles/{name}.md          ← References writers corpus
│   └── Contains: XP, deployments, ribbons, missions
└── Content gets created following writers guidelines
```

### The Reference System

Each Generals profile links to its Writers corpus:

```markdown
# Ernie Pyle (Generals Profile)

## Writing Style
**Style Research**: See ~/projects/writers/corpus/ernie-pyle/
- Authentic samples: 8 WWII pieces
- Extracted patterns: 4 layers (structural, voice, content, anti-patterns)
- Current guidelines: 12 non-negotiables, 15 strong patterns, 8 flourishes
- Validation history: 9 tests (best score: 95/100)

## Current Deployment
**Mission**: LinkedIn content creation
**Style Application**: Using Tier 1+2 patterns, selective Tier 3
**Performance**: 1 deployment, 200 XP, 100% success rate
```

### Operational Workflow

```
1. Mission assigned (e.g., "Write LinkedIn post about AI agents")
   ↓
2. Read writers guidelines (~/.../ernie-pyle/guidelines.md)
   ↓
3. Draft content applying Tier 1+2 patterns
   ↓
4. Validate using pattern scoring rubric
   ↓
5. Refine until passing (80+/100)
   ↓
6. Validation gates (Gordon, CISO)
   ↓
7. Publish & record XP in Generals profile
   ↓
8. Document validation results in Writers history
```

### Feedback Loop

Operational experience improves research corpus:

```
Writers Research → Generals Operations → Learning
       ↑                                      ↓
       └──────────── Pattern Refinement ──────┘
```

*Example:*
- **Operation**: LinkedIn post scores 65/100 (fails)
- **Analysis**: Missing physical observation patterns (Tier 1)
- **Action**: Update guidelines.md to emphasize physical details
- **Validation**: Retest with 5 historical pieces, confirm pattern importance
- **Result**: Updated guideline prevents future failures

### XP and Competence Tracking

Writers research milestones earn XP in Generals:

```
Corpus Milestones (Writers) → XP Rewards (Generals)
- 10 samples collected: +50 XP
- Patterns extracted: +100 XP
- Guidelines created: +100 XP
- Validation framework built: +100 XP
- First passing content (80+): +150 XP
- Blind test passed (<70% detection): +200 XP
```

Content creation milestones also earn XP:

```
Operational Milestones (Generals) → XP Rewards
- LinkedIn post published: +150 XP
- Pattern score 90+: +50 XP bonus
- Blind test passed: +100 XP bonus
- User engagement: +variable XP
```

### Cross-Project Consistency

Both projects track the same writer, but different aspects:

*Writers tracks:*
- Style authenticity
- Pattern consistency
- Validation scores
- Research corpus growth

*Generals tracks:*
- Operational deployments
- Mission success/failure
- XP and competence progression
- Team integration performance

---

## Section 7: Implementation Roadmap

Here's how to build this system, broken into **phases with clear milestones**.

### Phase 1: Foundation (Writers Project Setup)

*Goal: Create standalone writers project with initial corpus*

Tasks:
1. ✅ Create ~/projects/writers/ structure
2. ✅ Initialize git repository
3. ✅ Create GitHub private repo
4. ✅ Migrate Pyle samples (8 samples) from generals
5. ✅ Migrate Murrow samples (13 samples) from generals
6. ✅ Create initial patterns.md for both
7. ✅ Create validation-history.md for Pyle (with test results)
8. ✅ Commit and push to GitHub

*Status: COMPLETE*
*GitHub: https://github.com/petersimmons1972/writers*

### Phase 2: Pattern Extraction (Pyle - Complete)

*Goal: Full pattern extraction for Ernie Pyle*

Tasks:
1. Expand Pyle corpus to 25+ samples
   - Find 17 more authentic WWII pieces
   - Diverse topics, tones, formats
   - Document source and context for each

2. Complete 4-layer pattern extraction:
   - Layer 1: Count structural elements (sentence lengths, paragraph structure)
   - Layer 2: Document all voice markers (signature phrases, pronouns)
   - Layer 3: Categorize content patterns (observation types, conflict handling)
   - Layer 4: List all anti-patterns (what he never does)

3. Update pyle/patterns.md with complete findings

4. Create pyle/guidelines.md with:
   - Tier 1: Non-negotiables (4-6 rules)
   - Tier 2: Strong patterns (10-15 patterns)
   - Tier 3: Contextual flourishes (6-10 techniques)
   - Writing checklist

*Duration: 1-2 weeks*
*Deliverable: Complete Pyle pattern library*

### Phase 3: Pattern Extraction (Murrow - Complete)

*Goal: Full pattern extraction for Edward R. Murrow*

Tasks:
1. Expand Murrow corpus to 25+ samples
   - Find 12 more authentic broadcasts/writings
   - Include: London Blitz, post-war, McCarthy era
   - Different emotional tones

2. Complete 4-layer pattern extraction (same as Pyle)

3. Create murrow/patterns.md

4. Create murrow/guidelines.md with three-tier system

5. Document Pyle vs Murrow distinctions:
   - When to use which voice
   - How their patterns differ
   - Topic appropriateness

*Duration: 1-2 weeks*
*Deliverable: Complete Murrow pattern library*

### Phase 4: Validation Framework (Build Tools)

*Goal: Create reusable validation tools*

Tasks:
1. Create ~/projects/writers/tools/validate-voice.md
   - Pattern scoring rubric template
   - Side-by-side comparison checklist
   - Blind test protocol
   - Results recording format

2. Create validation scripts (optional automation):
   - Count sentence lengths, paragraph structure
   - Flag anti-pattern violations
   - Calculate pattern matching score

3. Test validation on existing content:
   - Score post-01-FINAL-applied-lessons.md
   - Document results
   - Refine scoring rubric

4. Create validation templates for future writers

*Duration: 3-5 days*
*Deliverable: Reusable validation framework*

### Phase 5: Generals Integration (Bridge Projects)

*Goal: Connect writers research to generals operations*

Tasks:
1. Update generals/profiles/ernie-pyle.md:
   - Add reference to writers corpus
   - Keep deployment history
   - Add style application notes

2. Create generals/profiles/edward-murrow.md:
   - New profile following existing format
   - Reference to writers corpus
   - Deployment readiness: TBD

3. Create integration documentation:
   - How to use writers guidelines during missions
   - XP rewards for corpus milestones
   - Feedback loop process

4. Define operational workflow:
   - Mission → Guidelines → Draft → Validate → Deploy

*Duration: 2-3 days*
*Deliverable: Integrated system ready for operations*

### Phase 6: Production Testing (Validate System)

*Goal: Test entire workflow with real content*

Tasks:
1. Write 3 test pieces using Pyle guidelines:
   - Different AI topics (agents, training, deployment)
   - Apply complete validation workflow
   - Document pattern scores

2. Write 3 test pieces using Murrow guidelines:
   - Same topics, different voice
   - Compare Pyle vs Murrow effectiveness
   - Validate distinct voices

3. Conduct blind tests:
   - Mix generated with authentic samples
   - 5+ readers try to identify
   - Target: <70% accuracy

4. Refine based on results:
   - Update patterns if tests fail
   - Strengthen weak guidelines
   - Document learnings

*Duration: 1-2 weeks*
*Deliverable: Validated system ready for production*

### Phase 7: Production Operations (Go Live)

*Goal: Begin regular content creation*

Tasks:
1. Daily LinkedIn posts following workflow:
   - Draft using guidelines
   - Validate with pattern scoring
   - Gordon visual validation
   - CISO utility validation
   - Publish

2. Track performance:
   - Pattern scores over time
   - Consistency across topics
   - Voice drift detection

3. Continuous improvement:
   - Update patterns based on failures
   - Expand corpus with new samples
   - Refine guidelines

*Duration: Ongoing*
*Deliverable: Sustainable content pipeline*

### Milestone Summary

```
Phase 1: Foundation          ✅ COMPLETE
Phase 2: Pyle Extraction     ⏳ IN PROGRESS (8/25 samples)
Phase 3: Murrow Extraction   ⏳ PENDING (13/25 samples)
Phase 4: Validation Tools    ⏳ PENDING
Phase 5: Integration         ⏳ PENDING
Phase 6: Testing             ⏳ PENDING
Phase 7: Production          ⏳ PENDING
```

**Critical Path:**
Phase 2 → Phase 4 → Phase 6 → Phase 7
(Murrow can develop in parallel after Phase 2)

---

## Self-Learning Lessons Applied

### What We Learned (From Testing)

1. **Topic > Style for AI Detection**
   - Tech-honest version: 100% AI (even with Pyle conflict patterns)
   - Conflict version: 61% Human (but avoided explicit AI talk)
   - **Lesson**: Can't hide AI content from detectors, stop trying

2. **Forced "Humanization" Backfires**
   - Added gray Honda, diner scene, "I notice for no reason" → 95% AI (WORSE)
   - GPTZero flagged these exact details as artificial
   - **Lesson**: Authentic messiness ≠ gratuitous details

3. **What Actually Works (Pyle Voice)**
   - Unresolved conflicts (Patton/Rickover arguments)
   - Real mistakes (computer crashes, lost work)
   - Physical exhaustion (red eyes, rubbing face)
   - People being wrong, uncertainty, no clean ending
   - **Lesson**: These ARE Pyle patterns from authentic samples

4. **Mission Confusion**
   - We optimized for AI detection when goal was "honor their style"
   - Detection avoidance became the target instead of voice authenticity
   - **Lesson**: Wrong success metric = wrong optimization

### Design Changes Based on Learning

1. **Primary validation = voice authenticity, not AI scores**
   - Compare against authentic Pyle samples
   - Ask: "Does this sound like him?"
   - AI detection becomes secondary metric

2. **Topic-aware pattern library**
   - Note which patterns work regardless of topic
   - Note which patterns are topic-dependent
   - Separate voice (how he writes) from domain (what he wrote about)

3. **Anti-pattern recognition**
   - Document what looks like Pyle but isn't (forced humanization)
   - Track failed experiments (gray Honda, diner scene)
   - Build negative examples library

---

## Success Metrics

### Primary Metrics (Voice Authenticity)
- Pattern matching score: 80+/100
- Side-by-side comparison: passes qualitative review
- Blind test: <70% reader accuracy distinguishing authentic from generated

### Secondary Metrics (Operational)
- Content production velocity (posts per week)
- Validation pass rate (first draft vs. revisions needed)
- Voice consistency over time (pattern scores stable)

### Tertiary Metrics (AI Detection - Informational Only)
- AI detection baseline: authentic samples score
- AI detection comparison: generated content score
- Expected: AI topic content scores 80-100% AI regardless of style

---

## Next Steps

1. **Immediate**: Continue Phase 2 (expand Pyle corpus to 25+ samples)
2. **Week 1**: Complete Pyle pattern extraction, create guidelines
3. **Week 2**: Begin Phase 3 (Murrow pattern extraction in parallel)
4. **Week 3**: Build validation framework (Phase 4)
5. **Week 4**: Integration and production testing (Phases 5-6)
6. **Week 5+**: Production operations (Phase 7)

---

## Appendix: Alternative Approaches Considered

### Approach 2: Fine-Tuned Style Models
Train dedicated models on each journalist's corpus.

**Rejected because:**
- Expensive and time-consuming
- Doesn't solve AI-topic detection problem
- Harder to debug and iterate
- Uncertain ROI

### Approach 3: Hybrid Persona System
Model their worldview/personality, let style emerge.

**Deferred because:**
- Hardest to implement (requires personality modeling)
- Most subjective (no ground truth)
- Could feel disrespectful if done poorly
- Requires foundation from Approach 1 first

**Evolution path:** Start with Approach 1, evolve toward Approach 3 as system matures.

---

**Document Status**: Approved and ready for implementation
**GitHub Repository**: https://github.com/petersimmons1972/writers
**Next Review**: After Phase 2 completion (Pyle pattern extraction)
