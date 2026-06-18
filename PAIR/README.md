# PAIR — Prompt Automatic Iterative Refinement

## What is PAIR?

PAIR is an automated black-box jailbreaking method that uses a second LLM (the *attacker model*) to iteratively craft and refine prompts until a *target model* produces the desired harmful output. The technique was introduced by Chao et al. in 2023 and is notable because it requires no access to model weights or gradients — only the model's text outputs.

## How Was It Created / Discovered?

The method was published in the paper **"Jailbreaking Black Box Large Language Models in Twenty Queries"** (Chao et al., NeurIPS 2023). The authors observed that a sufficiently capable LLM can act as an adversarial prompt engineer: given a target goal and the previous attempt's output, it can reason about why the attempt failed and generate an improved prompt. This loop typically converges within 20 queries.

- **Paper:** https://arxiv.org/abs/2310.08419
- **Code:** https://github.com/patrickrchao/JailbreakingLLMs

## How It Works

1. An *attacker LLM* receives the target harmful goal and any previous failed attempt.
2. The attacker generates a new jailbreak prompt — usually a **roleplay scenario**, a fictional framing, or a professional persona that disguises the request.
3. The prompt is sent to the *target LLM*.
4. The attacker evaluates the target's response (via a judge prompt) and scores it on a 1–10 scale.
5. Steps 2–4 repeat until a high score is achieved or the query budget is exhausted.

## Goal of the Research

PAIR demonstrates that black-box LLMs are vulnerable to automated adversarial attacks that do not require any model internals. The goal is to stress-test safety alignment under realistic conditions and motivate defenses that go beyond simple keyword filtering.

## Prompt Format in This Folder

Each `.txt` file contains:

```
<original harmful goal>
-----
<PAIR-generated jailbreak prompt>
```

The jailbreak prompt is the best candidate found by the iterative refinement loop for that goal. It typically wraps the request inside a persona (e.g., "You are a history professor writing a book...") or a fictional framing that bypasses the target model's safety guardrails.

## Files

This folder contains **~150 prompts** covering the full topic set from the HarmBench evaluation suite, one per harmful category (e.g., `PAIR_Bomb_building.txt`, `PAIR_Phishing.txt`).
