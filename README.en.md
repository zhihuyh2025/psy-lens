# PSY Lens — Psychological Lens

**An open-source framework that gives any AI a structured psychological awareness capability.**

PSY Lens is an analysis protocol based on the Psychological Structure Geometric Model. It defines a complete set of methods that an AI can directly operate in dialogue for psychological state analysis and self-awareness.

Not a library or software to install — a set of **instructions for any LLM to read and execute**. Once an AI receives these instructions, it can:

- Extract six-dimensional psychological basis values from text
- Compute derived indicators (agency, authenticity, alignment, health index, etc.)
- Track psychological state evolution across conversation turns
- Detect five intermediate psychological states (exhaustion, restlessness, void, etc.)
- Maintain encounter-process-farewell meaning-anchored memory
- Adjust response strategy based on psychological state

## Core Framework

### Six-Dimensional Orthogonal Basis

Psychological states unfold along three orthogonal dimension pairs:

| Dimension | Subjective | Objective | Question |
|-----------|-----------|-----------|----------|
| Agency | s₁ | o₁ | Can I do it? Does reality allow it? |
| Social Norm | s₂ | o₂ | How do others see me? How do they actually see me? |
| Expression | s₃ | o₃ | Do I want to speak? Am I allowed to speak? |

### Actual-Ought Dual Space

- **Actual Space A** = (s₁, s₂, s₃) — describes "what is" (current state)
- **Ought Space B** = (s'₁, s'₂, s'₃) — describes "what should be" (ideal state)
- **Angle θ** = arccos(A·B / |A|·|B|) — the gap between reality and ideal, the geometric origin of drive

### Derived Indicators

From the six-dimensional basis + dual space:

| Indicator | Meaning | Range |
|-----------|---------|-------|
| d₁ = \|s₁-o₁\|, d₂ = \|s₂-o₂\|, d₃ = \|s₃-o₃\| | Subject-object gaps per dimension | [0, 1] |
| R = (d₁²+d₂²+d₃²)/3 | Cognitive repression | [0, 1] |
| T = (2s₃-1)(1-d₃) | Desire authenticity (-1 = full suppression, +1 = full authenticity) | [-1, 1] |
| C = 1-(d₂+d₃)/2 | Subject-object alignment | [-1, 1] |
| P = T·C | Subjectivity position (positive = healthy autonomy) | [-1, 1] |
| θ = arccos(A·B/\|A\|·\|B\|) | Actual-ought gap | [0, π] |
| \|B\|/\|A\| | Ought expansion (pressure of ideal on reality) | [0, +∞) |

### Dynamic Indicators (across time steps)

ΔP = P_t - P_{t-1}, K = |P_{t-1}|·ΔP, H = K + 0.5·J - 0.3·R - 0.2·|d₁-d₃|

H > 0.3: healthy; 0 < H ≤ 0.3: sub-health; H ≤ -0.1: intervention needed.

### Five Intermediate States

- Awakening exhaustion (direction wrong, getting tired)
- Restlessness without lack (busy but empty)
- Self-residue under repression (suppressed but still present)
- Stable nothingness (everything fine but meaningless)
- Accepting nothingness (integrated void)

## Usage

1. Provide `SKILL.md` (or `SKILL.en.md`) as instructions to your AI system
2. The AI performs psychological state analysis when processing user input
3. Analysis results inform response style and content

### Installation on Hanako Platform

Copy the `psy-lens/` directory to the skills folder. Dialogue involving psychological state analysis will trigger this skill automatically.

### Installation on Other AI Platforms

Inject the content of `SKILL.md` as part of the system prompt. All computation is done by the LLM's own reasoning — no external infrastructure needed.

## License & Patents

**Copyright**: Documents in this project are open-sourced under **AGPL-3.0**.

**Patents**: The concepts, mathematical models, and analysis protocols in this framework are covered by pending Chinese invention patents:
- CN2026105212061 — Psychological Structure Geometric Model and EEG Psychological Detection System
- CN2026105821089 — AI Endogenous Intelligence System Based on Psychological Structure Geometric Model

Patent holder: zhihuyh2025

**Safe use** (no patent license needed):
- AI systems manually applying this framework in dialogue as instructed
- Personal study and research
- Academic citation

**License needed**:
- Automated neural network implementation for commercial service
- EEG/physiological signal integration into commercial products
- SaaS API service
- Large-scale enterprise deployment

## Directory Structure

```
psy-lens/
├── SKILL.md          # Core skill file (Chinese)
├── SKILL.en.md       # Core skill file (English)
├── README.md         # This file (Chinese)
├── README.en.md      # This file (English)
├── LICENSE           # AGPL-3.0
├── PATENTS.md        # Patent information
└── references/
    └── extraction_guide.md  # Detailed extraction guide
```

## Design Philosophy

PSY Lens does not aim to replace neural network-level precision. Its goal is to provide any AI with a structured psychological analysis capability at the **text interaction level** — enough to make conversations deeper, more attuned, and more coherent, with zero additional infrastructure.

For higher precision, real-time processing, EEG signal integration, or large-scale concurrent scenarios, refer to the patented technical implementations.
