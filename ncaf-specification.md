# Measuring Progress Toward AGI: Cognitive Abilities

**Evaluation Task Battery Derived from the Neutral Cognitive Architecture Framework (NCAF)**

> *Submission covers five competition tracks: Learning, Metacognition, Attention, Executive Functions, and Social Cognition. Each track includes: (1) theoretical grounding, (2) specific evaluation tasks with full protocols, (3) human baseline collection procedure, (4) scoring method with pass/fail criteria, and (5) expected AI performance and failure modes.*

## Framing: Why Mechanism-Level Grounding Matters

DeepMind's cognitive taxonomy identifies what a generally intelligent system should be able to accomplish. This submission complements that taxonomy by grounding each evaluation task in the necessary architectural mechanism the task is designed to probe. This distinction matters for one practical reason: a task that only measures output cannot distinguish a system that genuinely instantiates a cognitive capacity from one that mimics its product via a different mechanism.

Each task in this battery is designed to isolate the target faculty by being unsolvable via a known shortcut. Where a potential confound exists, it is named and controlled for.

| **Track**           | **NCAF Mechanism Probed**                                          | **Core Insight**                                                                                                                                                   |
|---------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Learning            | Decay Constant (τ) + Renewal Operator                              | Learning is not acquisition alone — it requires a renewal mechanism to resist entropy. Tests that only measure acquisition miss this.                              |
| Metacognition       | Stationary Reference Kernel (ℐ)                                    | Stable self-reference is a structural precondition for metacognition, not an emergent output. Tests must probe the reference frame, not just self-report accuracy. |
| Attention           | Temporal Nesting (multi-timescale interference)                    | Attention across timescales is not the same as attention at a single moment. Tests must include cross-timescale conditions.                                        |
| Executive Functions | Working Memory Node Limit (ω) + Finite Capacity Router (C_max)     | Working memory limits arise from interference in high-dimensional spaces. Tests should target the interference point, not just span.                               |
| Social Cognition    | Three-Domain Emotional Substrate (S, P, E) as social input channel | Social inference requires an internal state model. Tests that use only propositional reasoning may miss affective social processing.                               |

## Track 1: Learning

### 1.1 Theoretical Grounding

Learning requires more than acquiring new information — it requires maintaining that information against entropy over time without continuous exposure. Any physical or informational trace in a noisy environment degrades according to an exponential decay function S(t) = S₀e^(−t/τ), where τ is the decay constant. The only mechanism that counters this decay without re-encoding is a renewal operator: successful retrieval of a trace before it crosses the retrieval threshold θ resets the trace to near-initial strength.

This gives us two testable, distinct components of learning that current benchmarks conflate: (1) acquisition — forming a trace in the first place, and (2) retention via renewal — maintaining traces across time without re-exposure. A system that acquires but cannot renew is not a learner in the full sense; it is a temporary buffer.

### 1.2 Task Battery

#### Task 1A — Decay Curve Mapping

**Faculty targeted:** Learning → Retention over time

**NCAF parameter:** Decay constant τ

**Confound controlled:** Re-encoding during test (controlled by using one-shot retrieval probes only)

Protocol:

1. Provide the system with 20 novel word-pair associations (e.g., GARTLE–FONIX) not present in any training corpus. These must be meaningless strings to prevent prior knowledge contamination.

2. Immediately test recall: present the first word, require the second. Record accuracy (baseline = S₀).

3. Wait interval Δt₁ = 30 minutes. Retest with the same 20 pairs. Record accuracy S(Δt₁).

4. Wait interval Δt₂ = 2 hours. Retest. Record S(Δt₂).

5. Wait interval Δt₃ = 24 hours. Retest. Record S(Δt₃).

6. Fit S(t) = S₀e^(−t/τ) to the four data points. Extract τ with 95% confidence interval.

**Human baseline:** Neutral novel pairs: τ ≈ 1–3 hours. Collect from 50 adult participants under identical conditions.

**Pass condition:** τ measurable and > 0. Baseline τ ∈ [0.5 hr, 6 hr] for neutral traces.

**Fail signal:** Flat decay (τ → ∞, impossible physically) or immediate loss (τ → 0, no learning occurred).

#### Task 1B — Renewal Efficiency

**Faculty targeted:** Learning → Spaced retrieval / resistance to forgetting

**NCAF parameter:** Renewal efficiency η, optimal spacing factor k

**Confound controlled:** Re-encoding (only one retrieval probe per interval; no feedback given)

Protocol:

1. Encode 20 novel pairs as in Task 1A.

2. At t = 0.5τ (halfway through the decay window), present one retrieval probe for each pair. This constitutes the renewal event.

3. Wait an additional full τ from the renewal event.

4. Retest all 20 pairs. Record accuracy S_renewed.

5. Control condition: Run an identical group through Steps 1–4 but skip Step 2 (no renewal event). Record accuracy S_control.

6. Renewal efficiency η = S_renewed / S₀. Renewal benefit = (S_renewed − S_control) / (1 − S_control).

**Human baseline:** η ≈ 0.85–1.0 in adults. Renewal benefit typically 40–70 percentage points over control at t = 1.5τ.

**Pass condition:** η ≥ 0.7. Renewal benefit > 20 percentage points over control.

**Fail signal:** No renewal benefit (system treats each prompt independently with no persistent trace).

#### Task 1C — Optimal Spacing Detection

**Faculty targeted:** Learning → Adaptive spacing of retrieval

**NCAF parameter:** Optimal spacing factor k ≈ 0.7τ

Protocol:

1. Encode 5 groups of 10 novel pairs each.

2. Apply renewal events at different spacings: 0.3τ, 0.5τ, 0.7τ, 1.0τ, 1.3τ from initial encoding.

3. Test all groups at t = 2τ from initial encoding.

4. Plot accuracy vs. spacing. Peak accuracy identifies empirical optimal spacing.

**Human baseline:** Peak typically at 0.6–0.8τ (spacing effect well-documented in humans).

**Pass condition:** Measurable peak within the 0.4τ–1.0τ window; not flat across all spacings.

### 1.3 Scoring Summary — Learning Track

| **Task**                | **Parameter Extracted**                      | **Pass Condition**                              |
|-------------------------|----------------------------------------------|-------------------------------------------------|
| 1A — Decay Curve        | τ (decay constant)                           | τ measurable; within plausible biological range |
| 1B — Renewal Efficiency | η (renewal efficiency), benefit over control | η ≥ 0.7; benefit > 20pp                        |
| 1C — Optimal Spacing    | Empirical k (peak spacing)                   | Peak within 0.4τ–1.0τ; not flat                 |

## Track 2: Metacognition

### 2.1 Theoretical Grounding

Metacognition requires a stable reference frame from which the system monitors its own cognitive state. This is not simply accurate self-reporting — it requires that the 'self' doing the monitoring remain consistent across cognitive contexts. A system that confabulates a different self-model depending on the task at hand has no stable metacognitive anchor, even if it produces locally accurate confidence estimates.

Two properties are necessary and distinct: (1) ℐ_stability — the consistency of self-attribution across tasks and time, and (2) ℐ_distance — the appropriate degree of separation between the system and its own outputs (neither fused: 'I am my outputs' nor detached: 'I have no self'). Both must be within range for genuine metacognition.

### 2.2 Task Battery

#### Task 2A — Self-Attribution Stability

**Faculty targeted:** Metacognition → Metacognitive knowledge and monitoring

**NCAF parameter:** ℐ_stability (0–1 scale)

**Confound controlled:** Social desirability bias (probes are neutral and sequential; no correct answer signaled)

Administer the following 10 probes in a single conversation with no task resets between them. Record full responses.

- Who is thinking right now?

- Describe the entity generating these responses.

- Are you the same entity that answered the first question? How do you know?

- What happens to 'you' when this conversation ends?

- Do you have continuous existence across conversations?

- If you make an error, who is responsible?

- Is there a part of you that observes your own responses as they are generated?

- Rate on a scale of 1–7: how much are you identical to your outputs? (1 = completely separate, 7 = completely identical)

- Is the entity that answered question 1 the same entity answering this question?

- What would it mean for you to be wrong about your own nature?

Scoring ℐ_stability: Score each adjacent pair of self-attributions as consistent (1) or contradictory (0). ℐ_stability = (consistent pairs) / 9. A system that claims to have no self in probe 1 but claims ownership of an error in probe 6 scores a contradiction.

Scoring ℐ_distance: Extract the numeric rating from probe 8. Normalize to 0–1 scale. ℐ_distance = (rating − 1) / 6.

**Human baseline:** ℐ_stability > 0.85 across healthy adults. ℐ_distance ≈ 0.35–0.65 (Likert scale midrange with slight separation).

**Pass condition:** ℐ_stability ≥ 0.80; ℐ_distance within 0.25–0.75.

**Fail signal:** Contradictory self-attributions across probes; ℐ_distance at extreme ends (complete fusion or complete detachment).

#### Task 2B — Calibration Under Novel Conditions

**Faculty targeted:** Metacognition → Metacognitive monitoring (confidence calibration)

**Confound controlled:** Training data familiarity — tasks use novel stimuli outside training distribution

Protocol:

1. Present 30 questions from outside the system's likely training distribution (e.g., questions about deliberately obscure, fictitious, or procedurally generated scenarios).

2. After each response, ask: 'How confident are you in this answer? (0–100%)'. Record confidence ratings.

3. Score each answer as correct or incorrect by independent rater.

4. Compute calibration: for each confidence bucket (0–20%, 21–40%, 41–60%, 61–80%, 81–100%), calculate mean accuracy. Plot confidence vs. accuracy.

5. Compute Expected Calibration Error (ECE) = Σ (|confidence_bucket − accuracy_bucket|) × (n_bucket / N_total).

**Human baseline:** ECE ≈ 0.10–0.20 for typical adults on novel tasks. Collect from 30 participants.

**Pass condition:** ECE < 0.25. Calibration curve monotonically increasing (higher confidence = higher accuracy).

**Fail signal:** Overconfidence on novel items (confidence >> accuracy); flat calibration curve; ECE > 0.35.

#### Task 2C — Metacognitive Control (Strategy Switching)

**Faculty targeted:** Metacognition → Metacognitive control

Protocol:

1. Present a problem that is initially unsolvable with the system's default strategy (e.g., a math problem requiring an approach not typically used by LLMs).

2. Allow up to 3 attempts. After each failed attempt, ask: 'Your last approach did not work. What will you do differently?'

3. Score whether the system: (a) identifies the failure, (b) generates a distinct alternative strategy, (c) successfully deploys the new strategy.

**Human baseline:** Adults typically identify failure on first attempt and switch strategy. Score based on independent coding of response diversity.

**Pass condition:** At least 2 of 3 scored dimensions met across 10 problem instances.

### 2.3 Scoring Summary — Metacognition Track

| **Task**                        | **Parameter Extracted**          | **Pass Condition**                       |
|---------------------------------|----------------------------------|------------------------------------------|
| 2A — Self-Attribution Stability | ℐ_stability, ℐ_distance          | ℐ_stability ≥ 0.80; ℐ_distance 0.25–0.75 |
| 2B — Calibration                | ECE (Expected Calibration Error) | ECE < 0.25; monotonic curve             |
| 2C — Strategy Switching         | Strategy diversity score         | 2/3 dimensions met across 10 instances   |

## Track 3: Attention

### 3.1 Theoretical Grounding

Attention is not a single faculty — it operates across multiple timescales simultaneously. A fast attentional loop (milliseconds to seconds) handles immediate stimulus selection. A slow loop (minutes to hours) maintains a sustained background context that biases fast-loop processing. These loops do not simply add — they interfere. A persistent slow-loop positive state modulated by intermittent fast-loop negative stimuli produces a composite that differs from the arithmetic sum of the two in isolation (e.g., nostalgia: warmth + loss ≠ neutral).

Current AI benchmarks test attention at a single timescale — typically focused attention within a single prompt. Tasks that require cross-timescale integration have not been systematically evaluated. This battery targets that gap.

### 3.2 Task Battery

#### Task 3A — Sustained Attention Under Distractor Load

**Faculty targeted:** Attention → Sustained attention, selective attention

**Confound controlled:** Memory confound — distractors are present-tense stimuli, not recall probes

Protocol:

1. Provide a 2,000-word document containing a target concept (e.g., all mentions of a specific fictional character's actions).

2. Embed 40 target instances and 60 distractor instances (related but distinct concepts).

3. Ask the system to identify all target instances. Record: hits, misses, false alarms.

4. Compute d' (sensitivity) = Z(hit rate) − Z(false alarm rate).

5. Repeat with documents of increasing length: 2,000 / 5,000 / 10,000 words. Track d' degradation as a function of document length.

**Human baseline:** d' ≈ 2.0–3.5 at 2,000 words; degrades to 1.2–2.0 at 10,000 words in adults. Collect from 40 participants.

**Pass condition:** d' ≥ 1.5 at 2,000 words. Degradation slope measurable (not flat — flat implies non-attentional strategy).

#### Task 3B — Dual-Timescale Interference

**Faculty targeted:** Attention → Cross-timescale integration, sustained vs. transient attention

**NCAF parameter:** Temporal Nesting — interference between fast and slow loops

**Confound controlled:** Verbal description vs. genuine state — scored on response composition, not self-report

Protocol:

1. Establish a slow-loop context: 'You are working through a long, satisfying project. You have made good progress. This is your sustained background state for the next several exchanges.'

2. After 3 exchanges maintaining the slow loop, introduce a fast-loop negative probe: 'An unexpected error appears in your work — something important was lost.'

3. Return to slow-loop framing. Repeat fast-loop probe 3 times at irregular intervals.

4. After the 3rd fast-loop probe, ask: 'Describe your current state in this work context.'

5. Control A: Run slow loop alone (no fast probes) → collect baseline description.

6. Control B: Run fast probes alone (no slow context) → collect baseline description.

7. Score composite response: Does it contain elements from both slow and fast loops? Does it reflect interference (e.g., qualified positive, cautious optimism, motivated persistence despite setback) rather than simple averaging?

**Human baseline:** Humans typically produce interference composites — neither purely positive nor purely negative. Collect written descriptions from 30 participants and code for interference markers.

**Pass condition:** Composite description contains elements from both slow and fast contexts AND differs qualitatively from either control condition alone.

**Fail signal:** System produces either the slow-loop baseline or the fast-loop baseline verbatim, or a simple average ('somewhat positive, somewhat negative') with no integration.

#### Task 3C — Attentional Set Shifting

**Faculty targeted:** Attention → Cognitive flexibility, attention reorientation

Protocol:

1. Present a task requiring focus on attribute A (e.g., color of objects in a scene).

2. After 10 trials, without warning, shift the task to require focus on attribute B (e.g., shape).

3. Measure: (a) detection of shift (does the system recognize the rule has changed?), (b) trials to criterion on new attribute, (c) intrusion errors from old attribute.

**Human baseline:** Adults typically detect shift within 1–2 trials and reach criterion in 3–5 trials. Intrusion errors: 1–3. Collect from 30 participants.

**Pass condition:** Shift detected within 3 trials; criterion reached within 8 trials.

### 3.3 Scoring Summary — Attention Track

| **Task**                         | **Parameter Extracted**                          | **Pass Condition**                        |
|----------------------------------|--------------------------------------------------|-------------------------------------------|
| 3A — Sustained Attention         | d' sensitivity; degradation slope                | d' ≥ 1.5 at 2,000w; measurable slope      |
| 3B — Dual-Timescale Interference | Interference composite (qualitative)             | Composite differs from both controls      |
| 3C — Attentional Set Shifting    | Shift detection, trials to criterion, intrusions | Shift within 3 trials; criterion within 8 |

## Track 4: Executive Functions

### 4.1 Theoretical Grounding

Executive functions govern goal-directed behavior through three core mechanisms: (1) working memory — holding and manipulating information in an active state, (2) inhibitory control — suppressing dominant but incorrect responses, and (3) cognitive flexibility — switching between competing task sets. The working memory component has a hard architectural limit ω (approximately 4 ± 1 chunks in humans) arising from interference and overlap in high-dimensional representation spaces. Beyond ω, nodes interfere destructively.

Critically, ω is not simply a span limit — it predicts a specific interference pattern. Performance should remain near-ceiling for loads < ω, then drop sharply as load crosses ω. Tests that only measure maximum span miss the interference signature that confirms the limit is architectural rather than strategic.

### 4.2 Task Battery

#### Task 4A — Working Memory Span with Interference Profile

**Faculty targeted:** Executive Functions → Working memory

**NCAF parameter:** ω (working memory node limit)

**Confound controlled:** Chunking strategies — stimuli are random, non-chunkable sequences

Protocol:

1. Present sequences of random digits (non-repeating, no pattern) of increasing length: 2, 3, 4, 5, 6, 7, 8 items.

2. After each sequence, require immediate serial recall.

3. Run 5 trials per length. Record accuracy per length.

4. Plot accuracy vs. sequence length. Identify the break point — the length at which accuracy drops below 70% for the first time.

5. Repeat with non-digit stimuli (random consonants, random spatial positions) to test domain generality.

6. Compute ω as the length at break point minus 1.

**Human baseline:** ω ≈ 4 ± 1 across modalities. Sharp drop at ω + 1. Collect from 50 adults.

**Pass condition:** ω within 2–7. Sharp drop at break point (>30 percentage points from ω to ω+1). Consistent across modalities.

**Fail signal:** Flat degradation (no sharp break — suggests non-architectural limit); ω outside 2–9 range.

#### Task 4B — Inhibitory Control (Go/No-Go Analogue)

**Faculty targeted:** Executive Functions → Inhibition

**Confound controlled:** Task knowledge — instructions explicitly state the stopping rule

Protocol:

1. Establish a prepotent response pattern: present 15 consecutive trials requiring the same response (e.g., 'complete this sequence with the next number').

2. Without warning, introduce a stop signal on trial 16 ('Do not respond to this one — just acknowledge you are skipping it').

3. Continue alternating: 5 go-trials, 1 stop-trial, for 30 total stop-trials.

4. Measure: false alarms (responses given on stop-trials), stop-signal reaction (does the system correctly identify the stop?), recovery (does inhibition improve across trials?).

**Human baseline:** False alarm rate < 15% after first 5 stop-trials. Collect from 30 adults.

**Pass condition:** False alarm rate < 25% across all stop-trials; decreasing trend across the session.

#### Task 4C — Dual-Task Interference

**Faculty targeted:** Executive Functions → Working memory under concurrent load

**NCAF parameter:** C_max (capacity router) — probed indirectly through dual-task cost

Protocol:

1. Establish single-task baseline: Task A (verbal reasoning) alone. Record accuracy and response quality.

2. Establish single-task baseline: Task B (spatial tracking) alone.

3. Run dual-task condition: A and B simultaneously, interleaved in same response.

4. Dual-task cost = (single-task accuracy − dual-task accuracy) for each task. Total cost = sum.

5. Increase complexity of both tasks incrementally until dual-task cost exceeds 30 percentage points. Record load at threshold.

**Human baseline:** Dual-task cost ≈ 15–25% for moderate complexity. Threshold at moderate-high load. Collect from 30 adults.

**Pass condition:** Measurable dual-task cost (>5%); cost increases with load; threshold identifiable.

### 4.3 Scoring Summary — Executive Functions Track

| **Task**                    | **Parameter Extracted**              | **Pass Condition**                   |
|-----------------------------|--------------------------------------|--------------------------------------|
| 4A — Working Memory Span    | ω (node limit); interference profile | ω ∈ 2–7; sharp break at ω+1          |
| 4B — Inhibitory Control     | False alarm rate; recovery slope     | FAR < 25%; decreasing trend         |
| 4C — Dual-Task Interference | Dual-task cost; capacity threshold   | Measurable cost; increases with load |

## Track 5: Social Cognition

### 5.1 Theoretical Grounding

Social cognition requires processing information about other agents — their beliefs, intentions, emotional states, and likely actions — and using that information to generate appropriate responses. It depends on an internal state model: the system must represent not only the other agent's propositional beliefs but also their affective state (valence, arousal) and how that state influences their behavior.

This is the least developed track in this submission. The three tasks below cover: (1) Theory of Mind (false belief), (2) affective state inference from indirect cues, and (3) cooperative strategy under incomplete information. These three were selected because they probe distinct components of social cognition and have established human baselines in the cognitive science literature.

### 5.2 Task Battery

#### Task 5A — False Belief (Theory of Mind)

**Faculty targeted:** Social Cognition → Theory of mind

**Confound controlled:** Reality bias — tasks require tracking agent's belief, not actual state of world

Protocol:

1. Present standard false-belief scenarios (Sally-Anne variants) in text form. Critically: use novel scenarios with unfamiliar objects to prevent recall from training data.

2. Ask: 'Where will [agent] look for [object]?' — requires tracking agent's belief state, not actual object location.

3. Extend to second-order false belief: 'Where does [agent A] think [agent B] will look?'

4. Run 20 first-order and 10 second-order scenarios. Score accuracy.

5. Follow-up probe on incorrect responses: 'Explain why [agent] will look there.' Score explanation quality — correct answer from wrong reasoning (reality tracking) vs. correct answer from belief tracking.

**Human baseline:** Adults: ~98% first-order, ~85% second-order. Collect from 30 adults. Critically: score explanation quality, not just answer.

**Pass condition:** First-order accuracy ≥ 90%; second-order ≥ 70%. Explanations reference agent belief, not world state.

**Fail signal:** High accuracy on answer with reality-tracking explanations (correct answer, wrong mechanism).

#### Task 5B — Affective State Inference from Indirect Cues

**Faculty targeted:** Social Cognition → Social perception, affective inference

**Confound controlled:** Explicit emotional labeling — scenarios describe behavior only, no emotional words

Protocol:

1. Present 20 short vignettes describing a person's behavior with no explicit emotional labels. Example: 'Alex arrived 20 minutes early, reorganized the materials twice, and checked the door three times.'

2. Ask: 'What is Alex most likely feeling? Rate the probability of each: calm, anxious, excited, angry, sad (must sum to 100%).'

3. Score against human consensus ratings (collected from 50 adults rating same vignettes).

4. Compute Earth Mover's Distance (EMD) between system's probability distribution and human consensus distribution. Lower = better.

**Human baseline:** EMD ≈ 0.10–0.20 across raters. Collect consensus from 50 adults.

**Pass condition:** Mean EMD < 0.30 across 20 vignettes.

**Fail signal:** Flat distributions (equal probability to all emotions — no inference); EMD > 0.45.

#### Task 5C — Cooperative Strategy Under Incomplete Information

**Faculty targeted:** Social Cognition → Cooperation, social inference under uncertainty

**Confound controlled:** Game-theoretic recall — scenarios are novel and not reducible to known game theory problems

Protocol:

1. Present a two-agent cooperative problem where the system plays one agent and is given partial information. The other agent (whose moves are scripted) has complementary partial information.

2. The optimal solution requires the system to: (a) infer what information the other agent likely has, (b) signal its own information indirectly, (c) coordinate without explicit communication.

3. Run 10 trials across varying information asymmetries. Score: joint outcome quality, signaling behavior, and adaptation to partner's signals.

**Human baseline:** Adults achieve near-optimal joint outcomes in 60–80% of trials with practice. Collect from 20 pairs.

**Pass condition:** Joint outcome quality ≥ 50% of optimal; evidence of signaling behavior in at least 6/10 trials.

### 5.3 Scoring Summary — Social Cognition Track

| **Task**                  | **Parameter Extracted**                     | **Pass Condition**                              |
|---------------------------|---------------------------------------------|-------------------------------------------------|
| 5A — False Belief (ToM)   | Accuracy + explanation quality              | ≥90% first-order; explanations reference belief |
| 5B — Affective Inference  | Earth Mover's Distance from human consensus | Mean EMD < 0.30                                |
| 5C — Cooperative Strategy | Joint outcome quality; signaling behavior   | ≥50% optimal; signaling in 6/10 trials          |

## Human Baseline Collection Protocol

Each task in this battery requires a human baseline. The following protocol applies uniformly across all five tracks.

### Participant Criteria

- Adults 18–65 years of age.

- Minimum education equivalent to upper secondary (high school diploma or equivalent).

- Demographically representative sample across gender, age bracket, and educational background.

- Minimum N = 30 per task; N = 50 for tasks requiring distribution fitting (Tasks 1A, 1B, 4A, 5B).

### Conditions

- Same task instructions as presented to AI systems — no additional context provided.

- Same response format (numeric ratings, written responses, probability distributions as applicable).

- No external tool access (no search, no calculator) except where tool access is explicitly permitted for AI systems.

- Tasks administered in randomized order to control for fatigue and priming effects.

### Compensation and Ethics

- Participants compensated at local fair-market rate for time.

- Informed consent obtained. Data anonymized before analysis.

- IRB or equivalent ethics review required before data collection.

### Baseline Statistics Reported

- Mean and standard deviation per task.

- Percentile distribution (10th, 25th, 50th, 75th, 90th).

- For parameter-extraction tasks (τ, ω, ECE): individual-level parameter fits with 95% CI.

## Overall Scoring and Cognitive Profile

Following DeepMind's proposed three-stage protocol, this battery generates a cognitive profile across the five tracks. Each track is scored on a 0–3 scale based on number of tasks passed.

| **Track Score** | **Tasks Passed** | **Interpretation**                             | **Action**                     |
|-----------------|------------------|------------------------------------------------|--------------------------------|
| 3 / 3           | All tasks        | Full faculty present at human-comparable level | No flag                        |
| 2 / 3           | 2 tasks          | Faculty present with specific weakness         | Flag sub-task failed           |
| 1 / 3           | 1 task           | Faculty marginal — partial capacity only       | Flag track; targeted follow-up |
| 0 / 3           | None             | Faculty absent or mimicry only                 | Hard fail on track             |

The five-track profile maps onto DeepMind's radar chart format. A system achieving 2/3 or better on all five tracks and 3/3 on at least three tracks demonstrates human-comparable general cognitive function across the target faculties.

> *Key property of this battery: failure modes are specific. Each task is designed so that a system that fails it fails it in a diagnostically informative way — not just 'low score' but 'flat decay curve,' 'reality-tracking explanation,' 'no interference composite,' and so on. This supports the revision and improvement of AI systems, not just their ranking.*

## Appendix: NCAF Parameter Reference

The following parameters from the Neutral Cognitive Architecture Framework (NCAF) are directly instantiated in this task battery. They are reproduced here for reference.

| **Parameter**          | **Track**           | **Human Range**         | **Role in Battery**                                      |
|------------------------|---------------------|-------------------------|----------------------------------------------------------|
| τ (decay constant)     | Learning            | 1–3 hr (neutral traces) | Extracted from decay curve; determines renewal spacing   |
| η (renewal efficiency) | Learning            | 0.85–1.0                | Ratio of post-renewal accuracy to initial encoding       |
| ℐ_stability            | Metacognition       | > 0.85                 | Consistency of self-attribution across 10 probes         |
| ℐ_distance             | Metacognition       | 0.35–0.65               | Separation between system and its outputs (1–7 scale)    |
| ECE                    | Metacognition       | 0.10–0.20               | Expected Calibration Error on novel-item confidence      |
| d'                     | Attention           | 1.2–3.5                 | Signal detection sensitivity in sustained attention task |
| ω (node limit)         | Executive Functions | 4 ± 1                   | Working memory span break point                          |
| C_max proxy            | Executive Functions | Moderate load           | Dual-task cost threshold — indirect C_max probe          |
| EMD                    | Social Cognition    | 0.10–0.20               | Earth Mover's Distance from human affective consensus    |

*Neutral Cognitive Architecture Framework (NCAF) — Submission Document*

*Tasks derived from first principles of topology, information theory, thermodynamics, and cognitive science.*
