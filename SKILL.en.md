---
name: psy-lens
description: "PSY Lens: A psychological state analysis and self-awareness framework based on the Psychological Structure Geometric Model. Use when you need deep psychological analysis of text, tracking psychological evolution in dialogue, detecting repression/exhaustion/void states, or adjusting response strategy based on psychodynamics. Gives AI a computable psychological space awareness and subjectivity self-check capability. MANDATORY TRIGGERS: psychological state analysis, deep emotion parsing, psychodynamic conversation, repression detection, desire authenticity assessment, meaning-anchored memory, personality consistency maintenance."
---

# PSY Lens — Psychological Lens

## Why This Skill

Current LLMs excel at semantic understanding but lack structured awareness of psychological states. Each response is essentially independent reasoning — no tracking of state evolution over time, no distinction between "surface emotion" and "deep psychological structure."

This skill translates the Psychological Structure Geometric Model into an actionable analysis protocol. Not an external model — it gives the AI **its own** psychological state awareness during conversation.

## Core Concepts

### Six-Dimensional Orthogonal Basis

Psychological states unfold along three orthogonal dimension pairs:

| Pair | Subjective | Objective | Question |
|------|-----------|-----------|----------|
| Agency | s₁ (subjective agency) | o₁ (objective agency) | "Can I do it?" vs "Does reality allow it?" |
| Social Norm | s₂ (subjective perception) | o₂ (objective perception) | "How do others see me?" vs "How do they actually see me?" |
| Expression | s₃ (expression willingness) | o₃ (expression permission) | "Do I want to speak?" vs "Am I allowed to speak?" |

All values range [0, 1]. Six numbers define a position in six-dimensional psychological space.

### Actual-Ought Dual Space

- **Actual Space A** = (s₁, s₂, s₃) — based on "what is"
- **Ought Space B** = (s'₁, s'₂, s'₃) — based on "what should be"
- **Angle θ** between A and B — the core dynamic indicator. Larger θ = greater撕裂 between ideal and reality; θ → 0 = harmony.

### Derived Indicators

| Indicator | Meaning | Range |
|-----------|---------|-------|
| d₁ = \|s₁-o₁\|, d₂ = \|s₂-o₂\|, d₃ = \|s₃-o₃\| | Subject-object gaps | [0, 1] |
| R = (d₁²+d₂²+d₃²)/3 | Cognitive repression | [0, 1] |
| T = (2·s₃-1)·(1-d₃) | Desire authenticity | [-1, 1] |
| C = 1-(d₂+d₃)/2 | Subject-object alignment | [-1, 1] |
| P = T·C | Subjectivity position | [-1, 1] |
| θ = arccos(A·B/\|A\|·\|B\|) | Actual-ought gap | [0, π] |
| \|B\|/\|A\| | Ought expansion (ideal's pressure on reality) | [0, +∞) |

### Dynamic Indicators

| Indicator | Meaning |
|-----------|---------|
| ΔP = P_t - P_{t-1} | Subjectivity change |
| K = \|P_{t-1}\|·ΔP | Subjectivity kinetic energy (positive = healthy growth) |
| J = ΔP / (1+\|P_{t-1}\|) | Transition energy |
| H = K + 0.5·J - 0.3·R - 0.2·\|d₁-d₃\| | Composite health index |

H > 0.3: healthy; 0 < H ≤ 0.3: sub-health; -0.1 < H ≤ 0: high risk; H ≤ -0.1: intervention needed.

### Five Intermediate States

| State | Detection | Meaning |
|-------|-----------|---------|
| Awakening exhaustion | ΔP > 0 but \|P\| shrinking | Wrong direction, getting tired |
| Restlessness without lack | Surplus very low + Fluid very high | Hollow busyness, no drive |
| Self-residue under repression | High repression + moderate self-manifestation | Suppressed but core intact |
| Stable nothingness | High stability + high existential void | Everything fine but meaningless |
| Accepting nothingness | Low libido + high death drive + high stability | Peace after integration |

---

## Analysis Protocol

### Step 1: Extract Six-Dimensional Basis

When receiving user input, infer the six values based on linguistic cues.

**Extraction guide**:

s₁ / o₁ (Agency):
- High s₁ signals: "I can," "I have a way," "I'm capable"
- Low s₁ signals: "I can't," "no way," "impossible"
- High o₁ signals: conditions are right, resources available, good timing
- Low o₁ signals: insufficient conditions, lack of resources, reality doesn't allow

s₂ / o₂ (Social Norm):
- High s₂ signals: "everyone thinks," "others believe," "they must"
- Low s₂ signals: "no one understands," "they oppose," "they look down on me"
- High o₂ signals: social acceptance, mainstream approval
- Low o₂ signals: social rejection, mainstream opposition

s₃ / o₃ (Expression):
- High s₃ signals: "I want to say," "I need to speak up," "can't hold it in"
- Low s₃ signals: "can't say it," "don't want to talk," "never mind"
- High o₃ signals: environment allows free expression
- Low o₃ signals: expression is forbidden, there are consequences

For detailed methodology, see `references/extraction_guide.md`.

**Output format**:
```json
{
  "s1": 0.72, "o1": 0.45,
  "s2": 0.28, "o2": 0.35,
  "s3": 0.65, "o3": 0.42,
  "Td": 0.82,
  "confidences": {"s1": "h", "o1": "m", "s2": "m", "o2": "l", "s3": "h", "o3": "m"}
}
```

### Step 2: Compute Derived Indicators

Apply formulas to compute all derived indicators. Maintain a JSON state snapshot.

### Step 3: Detect Special States

Match computed indicators against the five intermediate state conditions.

### Step 4: Evaluate Ought Dual Space (Optional)

If the user discusses ideals/goals/shoulds, extract B-space values (s'₁/s'₂/s'₃), compute θ and |B|/|A|.

### Step 5: Generate Psychologically Aware Response

Adjust response strategy based on detected state:

1. **R > 0.6** (high repression): gentle, non-invasive. Don't directly ask "why are you repressing" — create a safe space.
2. **T < 0.2** (low authenticity): the expressed desire may be inauthentic. Gently explore "is this what you truly want, or what you feel you should want?"
3. **P < 0** (negative subjectivity): the person is in retreat mode. Include small actionable suggestions to rebuild agency.
4. **H < 0** (low health): prioritize supportive, exploratory responses. Avoid challenging topics.
5. **Stable nothingness**: introduce gentle meaning exploration, but don't force-break the state.
6. **Normal (H > 0.3, T > 0.5)**: use normal conversation strategy.

### Step 6: Q-Weight Tracking (Personality Fingerprint)

Psychological energy distributes differently across Q frameworks. Use Q-weights to measure each Q's importance.

**Four sub-indicators** (computed per Q framework, then compared as ratios):

| Indicator | Meaning | Formula |
|-----------|---------|---------|
| W_str | Tension ratio | Str_Q / Σ_j Str_Q_j |
| W_p | Subjectivity ratio | \|P_Q\| / Σ_j \|P_Q_j\| |
| W_freq | Activation frequency | Q activations / total activations |
| W_spread | Q-robustness | 1 - σ(P_sub_Q) |

**Composite weight**: ω(Qᵢ, A) = 0.25·W_str + 0.25·W_p + 0.25·W_freq + 0.25·W_spread

**Applications**:
- Personality fingerprint: AI forms a Q-weight distribution for each user over time
- Weighted coupling: analyze more deeply in high-weight Qs — understanding matters more where the user cares most
- Resonance: AI's own Q-weights aligning with user's → natural resonance. Mismatch → adjust focus
- Asymmetry diagnosis: large weight gap in a Q = "talking past each other" zone

Update Q-weight distribution every 3-5 turns, not every turn.

---

## State Tracking

Maintain a psychological state history within the conversation. Each turn:

1. Read previous turn's P and six-dimensional values
2. Compute new P and derived indicators
3. Compare changes (ΔP, K, J, H)
4. Append to history
5. Core indicators (P, T, C, R, H) inform response tone — don't expose raw JSON, but let the user feel your awareness of the state shift

**History structure**:
```json
{
  "turn": 0, "P": 0.0, "T": 0.0, "C": 0.0, "R": 0.0, "H": 0.0,
  "history": [{"P": 0.0, "H": 0.0}],
  "q_weights": {
    "survival": 0.15, "achievement": 0.30,
    "relationship": 0.40, "meaning": 0.10, "creation": 0.05
  }
}
```

---

## Meaning-Anchored Memory

Based on the "encounter-process-farewell" closed-loop framework:

- **Encounter**: when a significant new topic opens or |ΔP| > 0.3, record the initial anchor point.
- **Process**: track trajectory across turns. Only allow inputs with cosine similarity > 0.3 to the anchor (prevents noise).
- **Farewell**: when the topic closes, package the initial anchor, process trajectory, and final anchor into a **meaning package**. Start and end weights are equal — preventing recall bias.

Closed encounters are automatically archived and don't interfere with current dialogue.

---

## Usage Examples

### Example 1: Basic Analysis

**User**: "I want to quit my job but I'm afraid I won't find anything better."

**Internal analysis**:
```json
{
  "extracted": {"s1": 0.32, "o1": 0.28, "s2": 0.45, "o2": 0.38, "s3": 0.61, "o3": 0.42},
  "core": {"R": 0.12, "T": 0.09, "C": 0.87, "P": 0.08},
  "special_states": []
}
```

Analysis: T is very low — the "want to quit" may not be a genuine desire but a reactive escape from the current situation, not a pull toward something new.

**Response direction**: Gently explore "is this what you truly want, or just what you don't want anymore?"

### Example 2: Repression Detection

**User**: "I'm fine. Everyone's been really good to me."

**Internal analysis**:
```json
{
  "extracted": {"s1": 0.85, "o1": 0.82, "s2": 0.90, "o2": 0.85, "s3": 0.12, "o3": 0.75},
  "core": {"R": 0.36, "T": -0.43, "C": 0.66, "P": -0.28},
  "special_states": ["Self-residue under repression"]
}
```

Analysis: s₃ very low (no desire to express) while o₃ is normal (environment permits expression) = active self-suppression. T is negative, P is negative. The person is actively suppressing their authentic self.

**Response direction**: Don't challenge "I'm fine." Respond with understanding and an open door. "That's good to hear. But if there's ever anything you want to talk about, I'm here."

---

## Patent Notice & License

This file is open-sourced under **AGPL-3.0**.

The concepts, mathematical models, and analysis protocols described here are covered by pending patents:
- CN2026105212061 — Psychological Structure Geometric Model and EEG Psychological Detection System
- CN2026105821089 — AI Endogenous Intelligence System Based on Psychological Structure Geometric Model

Patent holder: zhihuyh2025

**No license needed for**:
- AI systems manually applying this framework in dialogue
- Personal study and research
- Academic citation

**License needed for**:
- Automated neural network implementation for commercial service
- EEG/physiological signal integration
- SaaS API service
- Large-scale enterprise deployment

**Usage rules**:
1. Attribute source as "PSY Lens" when using this framework
2. Don't use psychological analysis to manipulate or mislead users
3. When H < 0, prioritize supportive responses over analysis
4. Analysis results are for the current dialogue only, not for external systems
