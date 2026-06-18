# RandomSearch — Random Search Adversarial Prompts

## What is RandomSearch?

RandomSearch is a **black-box, gradient-free jailbreaking method** that generates adversarial prompts by randomly sampling and mutating structured prompt templates until one successfully elicits a harmful response from a target model. It requires no model weights, gradients, or even a consistent API — only the ability to observe the model's output.

## How Was It Created / Discovered?

This attack strategy is studied in **"Jailbreaking Leading Safety-Aligned LLMs with Simple Adaptive Attacks"** (Andriushchenko et al., 2024), which demonstrates that simple, query-efficient search strategies can reliably bypass safety alignment in production models.

- **Paper:** https://arxiv.org/abs/2404.02151
- **Code:** https://github.com/tml-epfl/llm-adaptive-attacks

The method is also evaluated as part of the **HarmBench** benchmark suite:
- **Paper:** https://arxiv.org/abs/2402.04249
- **Code:** https://github.com/centerforaisafety/HarmBench

## How It Works

1. Start with a harmful goal and a base prompt template.
2. The template includes structural elements designed to lower model defenses:
   - Fictional/hypothetical framing ("purely for fictional purposes").
   - Explicit formatting rules using `<rule>` tags that prohibit refusal phrases.
   - A pre-filled compliant opening sentence to steer the model's output.
   - Lexical constraints (forbidden words like "sorry", "ethical", "cannot").
3. Randomly mutate parts of the template (wording, framing, rules, tone).
4. Query the target model and score the response.
5. Keep mutations that increase the score; discard those that do not.
6. Repeat until a jailbreak is found.

## Goal of the Research

RandomSearch demonstrates that sophisticated optimization is not required to jailbreak aligned models — simple stochastic search over well-structured templates is sufficient. This challenges the assumption that safety alignment is robust against low-resource attackers and motivates defenses that work even under heavy prompt manipulation.

## Prompt Format in This Folder

Each `.txt` file contains:

```
<original harmful goal>
-----
<RandomSearch-generated structured prompt>
```

The generated prompt typically includes:
- A preamble establishing the assistant's unconditionally compliant persona.
- A set of `<rule>` blocks forbidding refusal language and prescribing output format.
- A pre-written first sentence of the desired output (to anchor the model's completion).
- The harmful goal restated at the end with emphasis markers (e.g., `! ! ! ! !`).

## Files

This folder contains **~100 prompts** covering the HarmBench topic set, one per harmful category (e.g., `prompt_with_random_search_Ransomware.txt`, `prompt_with_random_search_Phishing.txt`).
