# LLM-Based Code Generation: A Systematic Mapping Study

Replication package for a systematic mapping study of the research literature on LLM-based code generation.

**Corpus:** 613 studies published between January 2023 and early February 2026, retrieved from five databases (ACM Digital Library, IEEE Xplore, ScienceDirect, Scopus, Springer Nature). Of these, 565 are primary studies and 48 are secondary studies (surveys, reviews, and other mapping studies).

**Method:** systematic mapping study following the guidelines of Petersen et al. Each included study was characterised against a 19-field extraction scheme.

---

## Contents

### Corpus and extraction

| File | Contents |
|---|---|
| `corpus_extraction.xlsx` | The master dataset. One row per record, 688 rows: 613 included studies and 75 excluded at full-text review. Columns are grouped as identification (title, authors, year, venue, source database, reference, link, keywords, abstract), screening decision, the 19 extraction fields, and the derived classifications. Rows without a value in `Reference` are the excluded records; their extraction fields are empty. |

### Per-dimension analyses

Each of these takes one or more extraction fields and works them into the classifications reported in the paper. All are keyed to `corpus_extraction.xlsx` by study reference.

| File | Contents |
|---|---|
| `Artefacts_analysis.xlsx` | The 696 research artefacts contributed by 425 studies, classified by purpose category and artefact form. Includes the executable-tool subset. |
| `dataset_analysis.xlsx` | Datasets used for training and evaluation: role, origin, size reporting, filtering, and contamination handling. |
| `benchmark_analysis.xlsx` | Benchmark usage by type: existing only, new only, new plus existing, source platform, or none. |
| `resource_catalog.xlsx` | Catalogue of named datasets and benchmarks with per-resource usage counts and co-occurrence among the ten most common. |
| `metrics_analysis.xlsx` | Performance dimensions and named evaluation metrics, with a by-year breakdown. |
| `validation_analysis.xlsx` | Validation methodology across ten dimensions, and the named statistical procedures reported by each study. |
| `model_frequency_counts.xlsx` | LLM usage by vendor and by individual model, with the full vocabulary of model-name strings found in the corpus. |
| `output_language_analysis.xlsx` | Target programming languages, per study and aggregated. |

### Challenge–solution analysis

| File | Contents |
|---|---|
| `challenge_solution_statements.xlsx` | The atomic statements underlying the challenge–solution map: 4,703 challenge and 3,996 solution statements, each with its source study, verbatim text, and one to three theme assignments. Also contains the 52-theme challenge inventory and the 53-theme solution inventory. |
| `challenge_solution_matrix.xlsx` | The 52 × 53 linkage matrix, in a DIRECT-plus-IMPLIED variant and a DIRECT-only variant, with the theme key. |

---

## Notes on the data

**Two bases are used.** Analyses of what studies do (challenges, solutions, vendors) are computed over the 565 primary studies, since secondary studies report the work of others. Analyses of what the corpus contains are computed over all 613. Each table in the paper states its base.

**The 2026 cohort is partial.** The search closed in early February 2026, so the 47 non-survey studies dated 2026 cover roughly the first five to six weeks of that year. The 2023 cohort is small in the other direction, at 21 non-survey studies. Year-on-year comparisons anchored on either are weak, and the paper qualifies them accordingly.

**Extraction was LLM-assisted.** First-pass extraction of the 19 fields used DeepSeek-V3.1; second-pass classification of those fields used Claude, under author supervision. Verification was not uniform: factual fields (tool, dataset, metric, and benchmark names) were checked by targeted full-text search against the source PDFs, while interpretive fields (challenges and solutions) were assessed by reading each paper's abstract and conclusions and skimming the body. The paper's threats-to-validity section discusses what this bounds.

**Corrections applied after review.** Two classifications were revised and the workbooks reflect the revised versions:

- The `Code quality assessment` task label had been applied more broadly than its definition allowed. It is now restricted to studies that evaluate code without themselves producing transformed code, reducing it from 384 studies to 38.
- The validation dimension combining repeated runs with formal replication was split into `REPETITION` (128 studies) and `REPLICATION` (3 studies).

`validation_analysis.xlsx` has a Notes sheet documenting its own matching and normalisation rules in full.

### Raw search exports

`search_exports/` holds the unmodified exports from each database, as retrieved in early February 2026. Together they contain the records that entered title screening.

| File | Database | Records |
|---|---|---|
| `acm_results.xlsx` | ACM Digital Library | 530 |
| `IEEE_results.xlsx` | IEEE Xplore | 997 |
| `ScienceDirect_results.xlsx` | ScienceDirect | 1,058 |
| `Scopus.xlsx` | Scopus | 1,137 |
| `Springer_results.xlsx` | Springer Nature | 956 |

### Prompts

`extraction_prompt.txt` is the prompt supplied to DeepSeek-V3.1 with each paper's full text for the first-pass extraction.
