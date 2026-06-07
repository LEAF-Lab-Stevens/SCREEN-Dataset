# SCREEN-Dataset

**SCREEN** (**S**hort-form social media **C**ove**R**age of youth m**E**ntal h**E**alth in **N**ews) is a news-media stance dataset for understanding youth mental-health narratives around video-based social media.

This repository contains the dataset, annotation pipeline, and experiment code for the paper:

> **SCREEN: A News Media Stance Dataset for Understanding Youth Mental Health Narratives Around Video-Based Social Media**
> Jyotiraditya Singh, Havishey Jotaniya, Tiansui Xie, Sang Won Bae, Ping Wang
> Stevens Institute of Technology

## Overview

SCREEN is a ground-truth corpus of **1,492 news articles** covering two structurally divergent platforms — **YouTube** (algorithmic broadcast) and **Snapchat** (ephemeral messaging) — labeled for stance toward each platform's impact on adolescent mental health. The corpus was built with a human-machine collaborative framework that combines automated LLM relevance screening, human expert adjudication of ambiguous cases, and a multi-LLM consensus annotation stage.

Each article is labeled with one of four stance categories:

| Label | Description |
|-----------|-------------|
| Positive | Benefits, support, community, helpful features |
| Negative | Harms, addiction, bullying, lawsuits, decline in well-being |
| Neutral | Factual business news or balanced reporting |
| Mixed | Significant elements of both harm and benefit |

## Dataset statistics

| Platform | Negative | Mixed | Positive | Neutral | Total |
|----------|---------:|------:|---------:|--------:|------:|
| YouTube  | 505 | 191 | 103 | 58 | 857 |
| Snapchat | 492 | 120 | 4 | 19 | 635 |
| **Overall** | **997** | **311** | **107** | **77** | **1,492** |

The corpus exhibits a pronounced negativity bias (66.8% negative), with framing that varies sharply by platform architecture.

## Repository structure

SCREEN-Dataset/
├── Dataset/        # The SCREEN corpus and intermediate annotation files
├── Notebooks/      # Jupyter notebooks for the annotation pipeline and experiments
├── LICENSE         # MIT License
└── README.md

## Annotation pipeline

The dataset was constructed in stages:

1. **Relevance screening** — an ensemble of GPT-4o and GPT-4o-mini screens articles for substantive mental-health focus, separating high-confidence relevant items from ambiguous ones.
2. **Human adjudication** — three domain experts independently review ambiguous articles on Doccano, with majority voting determining inclusion.
3. **Consensus stance annotation** — four LLMs (GPT-4o, GPT-4o-mini, Claude Sonnet 4.6, Claude Opus 4.6) each assign a stance and topic labels; a 3-of-4 supermajority rule finalizes each label, with critical-stance tie-breaking.

## Experiments

The notebooks benchmark three families of models on the dataset:

- **Traditional ML**: Logistic Regression, SVM
- **Fine-tuned transformers**: RoBERTa, Social-RoBERTa, DeBERTa-v3, Longformer
- **Zero-shot LLMs**: GPT-4o, GPT-4o-mini, Claude Sonnet 4.6

across three tasks: multi-class stance prediction, prediction error analysis, and cross-platform profiling.

## Usage

The notebooks in `Notebooks/` require API keys for OpenAI and Anthropic to reproduce the LLM annotation and zero-shot prediction stages. Set your keys in the configuration cell before running. Supervised baselines can be run on the released labeled data without API access.

## License

This project is released under the [MIT License](LICENSE).

## Citation

If you use SCREEN in your work, please cite:

​```bibtex
@inproceedings{singh2026screen,
  title     = {SCREEN: A News Media Stance Dataset for Understanding Youth Mental Health Narratives Around Video-Based Social Media},
  author    = {Singh, Jyotiraditya and Jotaniya, Havishey and Xie, Tiansui and Bae, Sang Won and Wang, Ping},
  booktitle = {Proceedings of the 35th ACM International Conference on Information and Knowledge Management (CIKM '26)},
  year      = {2026}
}
​```

