# A Generative-Informed Neuro-Symbolic Framework for Syntactic Ambiguity Resolution

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Hugging Face Transformers](https://img.shields.io/badge/%F0%9F%A4%97-Transformers-blue)](https://huggingface.org/)

Official repository for the paper: **"A Generative-Informed Neuro-Symbolic Framework for Syntactic Ambiguity Resolution in Arabic DPs and Construct States"**.

---

## 📌 Overview

This repository implements a neuro-symbolic framework for resolving structural syntactic ambiguity in Arabic Determiner Phrases (DPs), including Construct States (*Iḍāfa*), non-Construct States, and coordinated DPs. 

By integrating formal generative primitives (**Merge**, **Agree**, and restricted **Search Space**) with pre-trained Transformer contextual attention mechanisms (**AraBERT**), the framework conditions language models using pre-formulated structural candidates:

$$\text{Input} = S \mathbin{[\text{SEP}]} \text{N1}: c_{\text{N1}} \mathbin{[\text{SEP}]} \text{N2}: c_{\text{N2}}$$

where:
* $S$ is the complete preprocessed sentence context.
* $c_{\text{N1}}$ represents Candidate 1 (High / VP Attachment).
* $c_{\text{N2}}$ represents Candidate 2 (Low / NP / Embedded Attachment).

---

## 📊 Dataset Specifications

The dataset was curated and filtered through a multi-stage verification pipeline from an initial pool of **44,637** raw sentence instances down to a verified human-ground-truth corpus of **6,696** instances:

| Split / Partition | High/VP Attachment ($c_{\text{N1}}$) | Low/NP Attachment ($c_{\text{N2}}$) | Total Instances |
| :--- | :---: | :---: | :---: |
| **Human Gold Corpus** | 4,881 (72.89%) | 1,815 (27.11%) | **6,696** |

* Preprocessing applies Farasa-based morphological segmentation via `ArabertPreprocessor`.
* Maximum input sequence length is set to $128$ tokens.

---

## 🛠️ Repository Layout

```text
A-generative-informed-neuro-symbolic-framework-for-syntactic-ambiguity-resolution/
├── README.md                   # Repository documentation
├── requirements.txt            # Environment dependencies
├── code_stage_3.py             # Full end-to-end PyTorch / AraBERT pipeline script
├── data/
│   ├── training_dataset.xlsx   # Stratified training split
│   ├── valid_dataset.xlsx      # Model selection / early stopping split
│   └── eval_dataset.xlsx       # Unseen held-out evaluation split
└── models/                     # Checkpoints directory (or HF Hub links)
