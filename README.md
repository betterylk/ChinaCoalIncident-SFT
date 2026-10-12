# ChinaCoalIncident-SFT

ChinaCoalIncident-SFT is a bilingual instruction dataset derived from official reports on 541 coal-mine accidents across 21 provincial-level jurisdictions in China (2014–2026). The Chinese master records contain 5,952 chronological events. Each incident pairs a timeline with a reference analysis of the accident mechanism, causes, and preventive recommendations, and retains structured metadata and a link to its official source. The aligned Chinese and English corpora represent the **same 541 incidents**, not 1,082 independent accidents.

## Release status

This public repository contains the four JSONL files listed below and the [construction and evaluation prompts](prompts/). The planned Hugging Face and Zenodo mirrors, a release licence, and a persistent citation still need to be confirmed. The repository files should not be assumed to represent a final, unrestricted release until the review items under [Provenance and use](#provenance-and-use) are resolved.

## Dataset files

| Filename | Records | Contents |
| --- | ---: | --- |
| [`Coal_accident_cases_ZH_sft.jsonl`](Coal_accident_cases_ZH_sft.jsonl) | 541 | Chinese master records |
| [`Coal_accident_cases_EN_sft.jsonl`](Coal_accident_cases_EN_sft.jsonl) | 541 | Record-aligned English translations |
| [`Coal_accident_cases_EN_sft_train.jsonl`](Coal_accident_cases_EN_sft_train.jsonl) | 487 | English training split |
| [`Coal_accident_cases_EN_sft_test.jsonl`](Coal_accident_cases_EN_sft_test.jsonl) | 54 | English held-out split |

Each JSONL line is one incident object with four top-level components: `incident_id`, `task`, `messages`, and `metadata`. The three messages are ordered **system → user → assistant**: the system message defines the analysis task, the user message supplies the accident timeline, and the assistant message contains the reference mechanism, cause analysis, and recommendations. The 26 metadata fields cover incident identity, equipment, accident attributes, mine and location, accident scene, affected personnel, and source provenance. `metadata.source.official_report` links to the official source.

The complete Chinese and English files share incident identifiers and record order. The English split files contain a 487/54 incident-level partition (reported random seed 42); Chinese records are not part of that split. **The split files use an earlier identifier assignment.** Match their timeline text to the complete English file when joining records, rather than assuming the split-file `incident_id` is the current canonical ID.

## Prompt files

The four plain-text prompts are available in [`prompts/`](prompts/):

- [`case_collection_prompt.txt`](prompts/case_collection_prompt.txt): official-source review and case collection, applied separately to each jurisdiction with its candidate-link file and province directory;
- [`chinese_sft_conversion_prompt.txt`](prompts/chinese_sft_conversion_prompt.txt): conversion of Chinese cases into three-message instruction records;
- [`english_translation_prompt.txt`](prompts/english_translation_prompt.txt): record-aligned English translation;
- [`english_sft_evaluation_prompt.txt`](prompts/english_sft_evaluation_prompt.txt): seven-criterion evaluation of English responses before and after supervised fine-tuning.

Bracketed inputs in the prompts, such as `[Province]` and `[Links file]`, are supplied for each run. The candidate-link files, processing utilities, translation scripts, and saved model-evaluation materials are not yet part of this public repository.

## Provenance and use

The corpus is a curated collection of **available official-report material**, not a census of all Chinese coal-mine accidents. Source reports vary in format and detail; some required text recovery from scans. Optional metadata can be missing, and a non-empty field does not by itself establish that a translated passage is semantically identical to the Chinese source. Users should retain nulls and empty arrays as missing information, check the linked report when source fidelity matters, and keep language versions of the same incident in the same train–test partition.

The dataset is intended for research on accident-timeline interpretation, information extraction, retrieval, translation assessment, and language-model adaptation. Its reference analyses and model outputs should not be treated as legal findings or operational safety instructions. The released records require final review of residual personal-name forms, translation artefacts, and date/time inconsistencies before unrestricted redistribution.

## Manuscript and contact

The accompanying *Data in Brief* manuscript is authored by Lingkai Yang, Guangfu Wang, Liang Fan, Zhi Chen, Yu Qin, Zhengyifan Song, and Jie Zhu. Correspondence: **Liang Fan** (L.Fan@lboro.ac.uk). Publication and dataset citation details will be added when available.
