# ADR Severity Triage & Entity Extraction (CADEC)

## Overview
An end-to-end NLP pipeline for triaging adverse drug event (ADR) reports
from patient forum posts — classifying severity and extracting drug/ADR
entity spans — built as an applied deep-dive project (classical NLP →
transformer fine-tuning → LoRA/QLoRA → deployment).

## Problem Statement
Given a patient forum post describing a drug experience, predict whether
it reports a serious or mild adverse drug reaction, and extract the
specific drug and ADR entity spans mentioned. Framed as a lightweight
triage system: flagging posts that likely warrant human review.

## Dataset
**CADEC (CSIRO Adverse Drug Event Corpus)** — 1,250 patient forum posts
from AskaPatient, covering 12 drugs, manually annotated for five entity
types: ADR, Drug, Disease, Symptom, Finding.

- Source: https://data.csiro.au (search "CADEC")
- License: CSIRO research-use data licence — **not included in this repo**.
  See `data/raw/README.md` for download instructions.
- Note: CADEC provides entity-level annotations, not a post-level severity
  label. Severity is a derived/proxy label — see methodology below.

## Status / Progress Log
- [x] Day 6 — EDA, severity-label heuristic, TF-IDF + Logistic Regression baseline
- [ ] Day 13 — DistilBERT fine-tune, F1 comparison vs. baseline
- [ ] Day 17–18 — NER for Drug/ADR entity extraction
- [ ] Day 19 — Error analysis, confusion matrices, OOD probes
- [ ] Day 20–23 — LoRA/QLoRA re-runs, tradeoff writeup
- [ ] Day 26–29 — FastAPI service, semantic search over past reports
- [ ] Day 30 — Final writeup

## Methodology Notes
- **Severity label**: derived via [keyword heuristic / ADR-count proxy —
  fill in once decided], since CADEC has no native severity field. This
  is a limitation, documented transparently rather than treated as ground truth.
- **Train/test split**: fixed random seed, stratified by severity label,
  reused identically across all model versions for fair comparison.


