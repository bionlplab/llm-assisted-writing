# Data Submission

This directory contains the essential data files needed to replicate the LLM-assisted writing analyses. Large CSV files are gzip-compressed. One embedding file is split into parts to stay below GitHub's per-file size limit.

## Directory Layout

- `cohorts/`: validated PubMed pre-LLM and post-LLM Health Informatics cohorts, plus excluded rows and validation summary.
- `detector_training/`: leakage-safe train/validation/test splits used for the abstract LLM detector.
- `llm_labels/`: post-era paper-level LLM probabilities and threshold labels, plus the threshold manifest.
- `mesh_openalex/`: frozen MeSH heading tables and OpenAlex topic/citation metadata used by downstream analyses.
- `ontology/`: ontology subtopic definitions and LLM-reviewed mappings from OpenAlex/MeSH/papers to ontology subtopics.
- `embeddings/`: SPECTER embedding tables for post-era B/C papers and pre-era A papers.
- `country_collaboration/`: country, language-environment, development-status, and collaboration feature tables.
- `impact_metrics/`: paper-level impact metrics without duplicate abstract text.
- `citation_windows/`: exact citation acquisition, cumulative citation cutoff, and monthly citation trend tables.

## Compressed Files

Most tables can be read directly with tools that support gzip, for example:

```python
import pandas as pd

df = pd.read_csv("submission/data/cohorts/post_dataset_validated.csv.gz")
```

## Split Embedding File

The pre-era embedding table is stored as split gzip parts:

```text
submission/data/embeddings/pre_a_embeddings.csv.gz.part-aa
submission/data/embeddings/pre_a_embeddings.csv.gz.part-ab
submission/data/embeddings/pre_a_embeddings.csv.gz.part-ac
```

Recombine before reading:

```bash
cat submission/data/embeddings/pre_a_embeddings.csv.gz.part-* > pre_a_embeddings.csv.gz
```

Then read `pre_a_embeddings.csv.gz` as a normal gzip-compressed CSV.

## Checksums

`MANIFEST.sha256` contains SHA-256 checksums for every submitted data file.
