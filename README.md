# ChinaCoalIncident-SFT
ChinaCoalIncident-SFT is a bilingual dataset of 541 Chinese coal-mine accidents (2014–2026), providing aligned JSONL records of accident timelines, causal analyses, and preventive recommendations for LLM fine-tuning.

## Prompt files

The plain-text prompts accompanying the dataset manuscript are in [`prompts/`](prompts/):

- [`case_collection_prompt.txt`](prompts/case_collection_prompt.txt): official-source review and case collection, applied separately to each jurisdiction with its own link file;
- [`chinese_sft_conversion_prompt.txt`](prompts/chinese_sft_conversion_prompt.txt): conversion of Chinese case records into three-message instruction records;
- [`english_translation_prompt.txt`](prompts/english_translation_prompt.txt): record-aligned translation into English;
- [`english_sft_evaluation_prompt.txt`](prompts/english_sft_evaluation_prompt.txt): English before/after SFT response evaluation.

These files reproduce the prompt listings documented in the manuscript. Bracketed inputs such as `[Province]` and `[Links file]` are placeholders supplied for each run.
