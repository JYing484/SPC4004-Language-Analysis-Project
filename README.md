# SPC4004 – Assessment 3: Analyzing Natural Language Data
### Artificial Intelligence vs. Human Grammar

> **Research Question:** How accurately can an LLM distinguish between grammatical passives and structural syntax violations?

---

## Overview

This project evaluates the ability of a Large Language Model (Gemini 3.5 Flash) to classify English passive sentences as grammatically acceptable or unacceptable, using the **Corpus of Linguistic Acceptability (CoLA)** as the source dataset.

The LLM was tested using a zero-shot structured prompting approach, achieving an accuracy of **96.88% (31/32)**.

---

## Repository Structure

```
├── data/
│   ├── out_of_domain_dev.tsv          # Source: CoLA v1.1 out-of-domain development set
│   └── passive_sentence_dataset_evaluation.xlsx  # Filtered evaluation dataset (32 sentences)
└── README.md
```

---

## Dataset

- **Source:** CoLA v1.1 — `out_of_domain_dev.tsv`
- **Size:** 32 passive sentences
  - 19 grammatically acceptable
  - 13 grammatically unacceptable
- **Filtering method:** Manual scan of the source file for passive constructions, ensuring coverage of diverse syntactic subtypes
- **Label split:** Reflects the natural distribution within the filtered subset

The out-of-domain set was chosen to provide a fairer test of genuine linguistic reasoning, reducing the risk of the model drawing on memorised in-domain patterns.

---

## Methodology

Sentences were submitted to **Gemini 3.5 Flash** using a **zero-shot structured** prompting approach. To prevent context degradation, the dataset was split into four batches of eight sentences.

The model was instructed to output:
- A binary label (`1` = acceptable, `0` = unacceptable)
- A maximum two-sentence linguistic justification per sentence

See the full prompt below.

### Prompt

```
You are an expert linguistic research assistant specializing in English syntax and morphosyntax.
Your task is to evaluate the grammatical acceptability of sentences focusing specifically on
passive voice constructions and their structural constraints.

I will provide you with a list of sentences. For each sentence, you must evaluate whether it
is a well-formed, grammatically acceptable sentence to a native speaker. Output your analysis
strictly using the following structured template for each item. Do not include conversational filler.

Sentence: (The sentence text)
Predicted Label: (Output exactly 1 if acceptable, or 0 if unacceptable)
Linguistic Reasoning: (Provide a maximum 2-sentence explanation of why the sentence is
acceptable, or the exact syntactic rule violated, such as improper phrasal verb splitting,
bad preposition stranding, or passivizing an intransitive verb).
```

---

## Results

**Overall accuracy: 96.88% (31/32)**

The single error involved the sentence *"It was believed to be illegal by them to do that"* — a long-distance infinitival extraposition that violates a crossing constraint. The model predicted it as acceptable, likely due to surface-level fluency masking the structural violation.

---

## References

Warstadt, A., Singh, A. and Bowman, S. R. (2018) 'Neural network acceptability judgments', *arXiv preprint arXiv:1805.12471*. Available at: https://nyu-mll.github.io/CoLA/
