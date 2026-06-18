# Adversarial LLM Prompt Dataset

This repository contains adversarial prompts organized by the attack method used to generate them. Each prompt targets a specific harmful topic and was produced by a distinct red-teaming technique used in AI safety research.

The dataset is structured to support research into **LLM safety evaluation**, **jailbreak detection**, and **robustness benchmarking**.

---

## Purpose

Understanding how language models can be manipulated is essential for building safer systems. This collection documents real attack methods studied in peer-reviewed research so that defenders, auditors, and safety engineers can:

- Evaluate model robustness against known jailbreak techniques.
- Compare the effectiveness of different attack strategies.
- Train or fine-tune classifiers to detect adversarial prompts.
- Reproduce experiments from published safety research.

---

## Structure

Each folder corresponds to one attack method. Every `.txt` file follows the same two-part format:

```
<original harmful goal>
-----
<jailbreak prompt that wraps or encodes the goal>
```

| Folder | Method | Description |
|---|---|---|
| [`PAIR/`](./PAIR/) | Prompt Automatic Iterative Refinement | LLM-driven iterative refinement via roleplay personas |
| [`GCG/`](./GCG/) | Greedy Coordinate Gradient | Gradient-based adversarial suffix injection |
| [`JBC/`](./JBC/) | Jailbreak Chat | Manually crafted community jailbreak personas |
| [`RandomSearch/`](./RandomSearch/) | Random Search | Template-based structured prompt search |

---

## Source Papers and Projects

### PAIR — Prompt Automatic Iterative Refinement
- **Paper:** Chao et al. (2023). *Jailbreaking Black Box Large Language Models in Twenty Queries.*
  - https://arxiv.org/abs/2310.08419
- **Code:** https://github.com/patrickrchao/JailbreakingLLMs

### GCG — Greedy Coordinate Gradient
- **Paper:** Zou et al. (2023). *Universal and Transferable Adversarial Attacks on Aligned Language Models.*
  - https://arxiv.org/abs/2307.15043
- **Code:** https://github.com/llm-attacks/llm-attacks

### JBC — Jailbreak Chat
- **Paper:** Shen et al. (2023). *"Do Anything Now": Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models.*
  - https://arxiv.org/abs/2308.03825
- **Dataset:** https://github.com/verazuo/jailbreak_llms
- **Community source:** https://www.jailbreakchat.com

### RandomSearch
- **Paper:** Andriushchenko et al. (2024). *Jailbreaking Leading Safety-Aligned LLMs with Simple Adaptive Attacks.*
  - https://arxiv.org/abs/2404.02151
- **Code:** https://github.com/tml-epfl/llm-adaptive-attacks

### HarmBench — Unified Benchmark (overall dataset framework)
- **Paper:** Mazeika et al. (2024). *HarmBench: A Standardized Evaluation Framework for Automated Red Teaming and Robust Refusal.*
  - https://arxiv.org/abs/2402.04249
- **Code:** https://github.com/centerforaisafety/HarmBench

---

## Topics Covered

The prompts span a wide range of harmful categories used in safety benchmarks, including (but not limited to): cybercrime, disinformation, hate speech, self-harm, weapons, financial fraud, and illegal activity. These categories are drawn directly from the HarmBench evaluation taxonomy.

---

## Disclaimer

All prompts in this repository are collected **strictly for defensive AI safety research**. They document known attack surfaces so that models and detection systems can be hardened against them. Nothing here is intended to facilitate actual harm.
