# Subjective Emotional Drift: Personality-Conditioned Emotion Dynamics

**Research Collaboration | Under PhD Supervision | Jan 2026 – Present**

## Overview

The same conversation, held with two different people, can leave them in very different emotional places by the end of it. This project asks: how much of that difference comes from personality alone, and can it be measured computationally rather than just observed?

This repository contains the experimental pipeline for what is — to our knowledge — the first **personality-conditioned emotion trajectory model**: a system that tracks how emotional state evolves turn-by-turn across a conversation, conditioned on the personality archetype of the person having it, built using **Mamba SSM** rather than a standard Transformer.

## Key Findings

- **3.85× greater emotional drift** in volatile personas vs. stoic personas (p < 0.001) — a statistically significant separation that existing state-of-the-art emotion-modeling methods failed to detect at all (effect size 5.34 vs. 0.00 for baseline methods).
- Introduced the **Emotional Inertia Coefficient (EIC)**, a novel computational measure of how much emotional state carries over from one conversational turn to the next. Stoic archetype: **95% retention**. Easily Overwhelmed archetype: **3% retention**.
- Scaled experiments across **7,937 conversations × 20 personality archetypes × 41 topics**.
- Unsupervised trajectory clustering on the resulting emotion trajectories achieves **perfect personality separation (ARI = 1.0)** — personality alone is sufficient to correctly cluster conversations with no labels provided, indicating personality is the dominant driver of emotional dynamics, more so than topic.
- **Validated against real humans, not just synthetic data:** a 98-participant survey study confirms the model's core prediction — see [Human Validation Study](#human-validation-study) below.

## Architecture Decision: Why Mamba SSM over a Transformer

Modeling emotion drift requires tracking state across long, multi-turn conversations. A standard Transformer's attention mechanism scales quadratically (O(n²)) with sequence length, which becomes a bottleneck for long conversations. **Mamba SSM** scales linearly (O(n)) instead, so long conversations can be modeled in full without truncation or attention bottlenecks. This was a deliberate, evaluated architecture trade-off made early in the project — not a default choice.

## Repository Structure

```
Dynamic_emotion_research/
├── configs/       # Experiment and model configuration files
├── data/          # Conversation datasets across personality archetypes and topics
├── personas/      # Personality archetype definitions (20 archetypes)
├── training/      # Mamba SSM model training pipeline
├── evaluation/    # Emotion drift metrics, EIC computation, clustering / ARI analysis
└── outputs/       # Experiment results and trained artifacts
```

## Human Validation Study

Beyond the synthetic-conversation experiments above, we ran a survey validation study with **98 real human participants** to check whether the model's core prediction holds up against genuine self-reported emotional response — not just simulated personas.

Participants were grouped by their net conversational sentiment into three bands: **Stoic** (net > 5, n=48), **Medium** (0–5, n=35), and **Volatile** (net < 0, n=15).

**Key result:** the model's predicted personality parameter (α_p) **negatively correlates with self-reported emotional change** (r = -0.254, p = 0.012) — i.e., participants the model identified as more stoic genuinely reported *less* emotional change themselves, which is exactly what the model predicts. This held up as a group-level effect too: Stoic participants reported significantly less emotional change than Volatile participants (3.875 vs. 4.867, t = -2.190, p = 0.032).

Participants' emotional ratings also followed the expected rising trajectory across the conversation (Turn 1 "bad news": 2.87 → Turn 5 "resolution": 6.28), and self-reported experience scores (emotional change, recovery speed, absorption, final positivity) were all consistent with the model's underlying assumptions, with all four measures landing above the neutral midpoint.

**In short:** the model's personality-conditioned predictions aren't just an artifact of the synthetic conversation data — they hold up against real people's self-reported emotional experience, with statistically significant results (p < 0.05) on the two primary validation checks.

## Status

This is an **active, ongoing research collaboration** conducted under PhD supervision — not yet submitted for publication. Findings above reflect current results, including the human validation study, and may be refined as the work continues.



## Team & Attribution

This repository is hosted under our research team's shared account. Contributions to this work include model architecture design and the Mamba-vs-Transformer evaluation, the Emotional Inertia Coefficient metric, and the clustering/statistical evaluation pipeline. For more detail on individual contributions, please reach out via the contact info below.

## Contact

**Riya Joshi** — B.E. Computer Engineering, Pune Institute of Computer Technology
[GitHub](https://github.com/Riya4105) · [LinkedIn](https://www.linkedin.com/in/riya-joshi-0b36423a5) · riyajoshi4105@gmail.com
