# Sources and local selection

Created on 2026-11-15 for STEM research, software design, and high-level technical writing. This is a local adaptation, not an official ASD or upstream skill release. Source instructions were reviewed as material to curate; they do not override the user's task.

## Primary sources

- [danyuchn/asd-ste100-skill](https://github.com/danyuchn/asd-ste100-skill/tree/9c351694439ea1171f36c65b91ba661e7a0499c8), revision `9c351694439ea1171f36c65b91ba661e7a0499c8`: `SKILL.md` and `references/writing-rules.md`. Adapted ambiguity control, stable terminology, and preservation of modality. Omitted the strict style caps and linter because this collection serves multiple prose genres. The official ASD-STE100 dictionary is not included; [ASD's official download page](https://www.asd-ste100.org/STE_downloads.html) is the source for the actual standard.
- [blader/humanizer](https://github.com/blader/humanizer/tree/b48c832f0f809c1b5658edbb838c2521b72f2413), revision `b48c832f0f809c1b5658edbb838c2521b72f2413`: `SKILL.md`. Adapted the structural editing patterns and fidelity checks into a short optional reference. Omitted the long pattern catalog, intermediate-output requirements, and authorship-detection claims. Naturalness is judged by usefulness to the reader, not by a list of supposed AI tells.
- [k-dense-ai/scientific-agent-skills](https://github.com/k-dense-ai/scientific-agent-skills/tree/2d2065fb4520fa3f3f2bcf61cff26ec8b7eba4b5), revision `2d2065fb4520fa3f3f2bcf61cff26ec8b7eba4b5`: reviewed `scientific-writing`, `literature-review`, `citation-management`, and `scientific-critical-thinking`, with related candidate skills inspected for fit. Adapted evidence fidelity, claim/source checks, research argument, and synthesis guidance. Omitted biomedical routing, mandatory per-claim human-verification workflows, manifests, unrelated tool dependencies, and automatic citations to the skill library. Important claim verification remains part of writing; routine drafting does not require an administrative pipeline.

The three upstream MIT notices are retained in [source-licenses.txt](source-licenses.txt). They apply to the upstream material, not to the separately controlled ASD standard.

## Selective K-Dense installation

Only these implementation skills accompany the writing skill:

- `geomaster`: GIS, raster and vector workflows, remote sensing, spatial evaluation, and Earth-observation ML. Its GeoPandas coverage avoids installing a second overlapping GIS skill.
- `scikit-learn`: classical ML, preprocessing pipelines, model selection, and evaluation.
- `transformers`: Hugging Face model loading, tokenization, inference, and fine-tuning for text, vision, and multimodal work.

Their supporting references remain local and load only when needed. Local provenance records identify source revisions and adaptations. No Python environment, library dependency, model weight, dataset, service account, or plugin was installed as part of this collection. Medical and biomedical skills were excluded. Other CS libraries were left out unless needed for a specific task; domain relevance alone is not a reason to install every package skill.

## Codex compatibility and recovery validation

On 2026-11-15, the interrupted installation was recovered rather than repeated. Before local compatibility edits, all 36 files in the three domain companions matched Git blob hashes in K-Dense's complete tree at the pinned revision above. The upstream package-version and execution reports are retained upstream assertions, not tests rerun locally during this recovery.

Local adaptations move the domain skills' unsupported top-level `compatibility` key into `metadata`, retain their runtime requirements and source URLs, remove Claude-named tool allowlists, and add optional Codex `agents/openai.yaml` interface metadata. Automatic invocation remains enabled by default. The Transformers authentication guidance presents login methods as alternatives and reuses existing access; public-model work does not require a new login by default. GeoMaster explicitly attributes its test history to upstream. Original per-skill license declarations are preserved; the K-Dense repository's MIT notice is included in [source-licenses.txt](source-licenses.txt).

The [official Codex skills documentation](https://developers.openai.com/codex/skills/) was checked for the `~/.agents/skills` user discovery path, progressive disclosure, and optional interface metadata. Validation uses the installed `skill-creator` checker plus local reference and YAML checks. These checks establish skill packaging, not that every scientific example or external service works with the user's installed libraries.

An independent forward test exercised a research abstract, draft software RFC, high-level remote-sensing explanation, and prose cleanup with only supplied evidence. It checked unsupported claims, uncertainty, decision status, and full-sequence authentication counts. No writing-guidance change was justified by that limited test; it is not a guarantee about every future invocation.

## Additional skill discovery

The [skills.sh directory](https://skills.sh/) and its technical-writing search were checked on 2026-11-15. [Anthropic's doc-coauthoring](https://github.com/anthropics/skills/tree/main/skills/doc-coauthoring) was also read. The directory reported approximately 102,000 installations at inspection; this is a popularity signal, not a quality guarantee. Its audience framing and reader-testing idea are useful, but installing another broad writing workflow would duplicate this skill and add frequent interviews and confirmation steps. It was not installed.

The existing local `documentation-and-adrs` skill already supports repository documentation and ADR conventions. It was inspected for overlap and left unchanged. The new writing skill supplies research and audience-specific prose guidance without replacing those project conventions.
