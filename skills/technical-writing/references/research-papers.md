# Research papers

Use for empirical STEM papers, computational methods papers, abstracts, related work, thesis sections, and responses to reviewers. Match the actual article type and venue. A theoretical paper, dataset paper, or review need not follow an empirical IMRAD outline.

## Build an argument from the research record

Identify the research question, the specific contribution, the evidence for it, and its limits. Let each section advance that argument. Distinguish what the work demonstrates from what it proposes or motivates. Claims of novelty, generality, causation, or superiority need evidence beyond polished wording.

For substantial drafting, keep a working link between important claims and the supplied experiment outputs, tables, figures, or passages that support them. An informal outline or compact claim/source table is enough when traceability is simple. Do not impose manifests, evidence IDs, external services, or human sign-off on every sentence.

When the research record is incomplete, draft only what it supports. Put unresolved information in a short author note or an unmistakable placeholder if the user wants a working draft. Never make up a sample size, model setting, result, citation, funding statement, approval, or availability declaration. A missing report of an experiment does not establish that it was never performed.

## Give each section a job

- **Title and abstract:** Describe the actual task and scope. A useful abstract moves from the problem and gap to the approach, principal supported result, and bounded implication. Include quantitative findings when available and meaningful. Match the completed paper; do not invent numbers to satisfy an abstract pattern.
- **Introduction:** Establish the concrete problem, the relevant limitation in existing work, why it matters, and how this study addresses it. Avoid a history-of-the-field opening or a claim that no prior work exists without a defensible search. State contributions at the specificity the evidence permits.
- **Related work:** Organize by research question, method, assumption, or unresolved disagreement. Compare approaches on common criteria. Explain how the current work relates to them without caricaturing prior work. Avoid an author-by-author inventory.
- **Methods:** Describe what was actually done closely enough to reproduce the relevant result. Name data selection, preprocessing, independent units, splits, models or derivations, evaluation, uncertainty estimates, and consequential implementation choices. Separate planned work from completed work. Put extensive details in a supplement when the venue allows, with clear pointers.
- **Results:** Answer the research questions in an understandable order. Give estimates, units, denominators, uncertainty, and comparison conditions where available. Explain the finding a display supports without repeating every cell. Keep interpretation distinct from observation unless the venue combines results and discussion.
- **Discussion:** Interpret results in relation to the question and verified literature. Explain plausible mechanisms as interpretations unless tested. Address counterevidence, failures, generalization limits, and practical consequences.
- **Conclusion:** State what was learned within the study's actual scope. Do not introduce a new result or repeat the abstract at length.

Use explicit transitions between question, method, finding, and implication. Prefer informative topic sentences to repeated announcements such as “this section presents.” Keep paragraph flow suitable for reading an argument, rather than turning the manuscript into a checklist.

## Interpret quantitative evidence faithfully

Preserve metric definitions, baseline conditions, independent sample units, and the meaning of error bars. Distinguish standard deviation, standard error, and confidence or credible intervals. Do not add a test, interval, correction, or statistical claim that was not performed or supplied.

An increase from 0.70 to 0.77 is 7 percentage points or 10% relative, if the metric is a proportion; name the comparison correctly. “Significant” should identify statistical or practical meaning. A non-significant test does not establish equivalence, and correlation does not establish causation. Pixels, repeated measurements, or model runs may not be independent samples.

Make limitations specific: name the affected conclusion, the source of uncertainty, and the setting in which the conclusion may fail. “More research is needed” does not explain a limitation. Check [geospatial and ML reporting](geospatial-and-ml.md) when relevant.

## Sources and literature synthesis

Verify both source identity and claim support. Prefer the paper, dataset documentation, software documentation, or authoritative record itself. A resolving DOI verifies neither that the citation identifies the intended paper nor that it supports the sentence. Search snippets and another paper's bibliography are discovery aids.

Use the correct version for the claim; distinguish preprints from peer-reviewed work and note material corrections or retractions when known. Preserve verified author names, titles, dates, identifiers, quotations, and locators. If access is unavailable, label verification as incomplete; never supply a plausible DOI or quotation from memory.

Use sources appropriate to CS and Earth science, such as ACM, IEEE, ACL Anthology, relevant publishers, arXiv, Earth-observation data providers, OpenAlex, or Semantic Scholar, as available. Do not route these subjects through biomedical databases by default. Respect dataset and benchmark citations required by the actual research context.

For a narrative related-work section, bound the coverage honestly. If asked for a systematic or scoping review, record databases, queries, search dates, eligibility criteria, screening, exclusions, and synthesis choices at the level needed to reproduce it. Do not call a few search results exhaustive or systematic. Reuse available authenticated access rather than requiring another service or login merely to write.

## Displays, review, and submission

Make captions interpretable without hunting through the paper: identify what is plotted, units, aggregation, sample unit, and uncertainty when applicable. Reconcile labels and numbers with the text. Do not generate illustrative data and present it as a study result.

For reviewer responses, track each substantive concern, the response or reasoned disagreement, the actual change, and its location. Separate edits already made from proposed experiments. Do not promise a rerun that has not happened.

When submission preparation is requested, check the venue's current template, reporting expectations, authorship and AI-disclosure rules, and required declarations. Use factual declarations supplied or verified for this study; do not import medical reporting checklists into unrelated STEM work. Writing a submission draft does not itself authorize submitting it or uploading unpublished material to a new service.
