# clinical-nlp-french

Reproducing **CamemBERT-bio** biomedical named-entity recognition (NER) results on the **QUAERO** French medical corpus.

> **Status: work in progress.** This repository documents an ongoing, self-directed reproduction study. Scores listed below are the *reference targets* reported in the original paper — not results obtained here. Results and their analysis will be added as each phase is completed.

---

## Objective

The goal is to reproduce, from scratch and with a clean evaluation protocol, the entity-level NER performance reported for `camembert-bio-base` compared to the general-domain `camembert-base` on the QUAERO corpus (EMEA and MEDLINE splits).

Beyond obtaining numbers, the aim is methodological: to build a rigorous, reproducible pipeline for French clinical/biomedical NLP, and to document any divergence from the published scores rather than conceal it.

## Reference paper

Touchent, R., Romary, L., & de la Clergerie, É. (2023). *CamemBERT-bio: a Tasty French Language Model Better for your Health.* arXiv:2306.15550. (Later: *CamemBERT-bio: Leveraging Continual Pre-training for Cost-Effective Models on French Biomedical Data*, LREC-COLING 2024.)

- Model: [`almanach/camembert-bio-base`](https://huggingface.co/almanach/camembert-bio-base)
- Baseline: [`camembert-base`](https://huggingface.co/camembert-base)
- Dataset: [`DrBenchmark/QUAERO`](https://huggingface.co/datasets/DrBenchmark/QUAERO) (Hugging Face Hub)

## Task

Named-entity recognition on the QUAERO French Medical Corpus (Névéol et al., 2014):

- **EMEA** — drug leaflets
- **MEDLINE** — scientific article titles

Entities are annotated with 10 UMLS semantic groups. Following the reference protocol, nested entities are reduced to their coarsest granularity, and labels use the IOB2 scheme.

## Models compared

| Model | Role |
| --- | --- |
| `camembert-base` | General-domain baseline |
| `almanach/camembert-bio-base` | Biomedical continual-pretraining model |

## Evaluation

Evaluation uses **seqeval** in **strict mode**, **micro-average**, **IOB2** scheme — i.e. **entity-level** F1, not token-level.

> Note: token-level scoring inflates results (a suspiciously high F1, e.g. ~0.95, is a red flag for token-level evaluation). Entity-level strict matching is the correct protocol and the one used in the reference paper.

## Reference scores to reproduce

Entity-level strict micro-average F1 reported for CamemBERT-bio (targets, **not** results from this repo):

| Split | Target F1 |
| --- | --- |
| EMEA | 76.71 |
| MEDLINE | 68.47 |

Any gap between reproduced and reference scores will be documented and explained.

## Repository structure

```
clinical-nlp-french/
├── notebooks/
│   └── 01_warmup_conll.ipynb     # NER warm-up on CoNLL (pipeline sanity check)
├── docs/
│   └── paper_reading_notes.md    # reading notes on the CamemBERT-bio paper
└── README.md
```


## Environment

- Google Colab (Free Tier, T4 GPU)
- Hugging Face `transformers`, `datasets`
- `seqeval` for entity-level evaluation

## References

- Touchent, R., Romary, L., de la Clergerie, É. (2023). *CamemBERT-bio: a Tasty French Language Model Better for your Health.* arXiv:2306.15550.
- Névéol, A., Grouin, C., Leixa, J., Rosset, S., Zweigenbaum, P. (2014). *The QUAERO French Medical Corpus: A Resource for Medical Entity Recognition and Normalization.*
- Martin, L., et al. (2020). *CamemBERT: a Tasty French Language Model.* ACL.
- Nakayama, H. (2018). *seqeval: A Python framework for sequence labeling evaluation.*

---

*Author: Thilleli ROUAS — [github.com/thiilelli](https://github.com/thiilelli)*
