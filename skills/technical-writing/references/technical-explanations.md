# High-level technical writing

Keep the subject accurate while choosing the depth for the reader. “High level” means explaining the consequential ideas and relationships; it does not mean replacing them with slogans.

## Choose the reader's job

Infer the document's purpose from the request and context, then organize accordingly:

- **Explanation or overview:** Establish the main idea, explain how the important parts relate, and make assumptions and limits visible.
- **Decision brief:** State the decision or recommendation early, followed by the evidence, material trade-offs, and uncertainties that could change it.
- **Tutorial or how-to:** Give the intended outcome, necessary prerequisites, actions in a usable order, and an observable indication of success. Separate optional background from required steps.
- **Project or research update:** Say what changed, what the evidence shows, and what remains unresolved or comes next. Distinguish achieved, planned, and blocked work.
- **Reference:** Make facts easy to find with stable terms, compact entries, and accurate contracts. Avoid burying lookup information in a narrative.

Combine forms when the request needs them, but keep the main reading path clear. Do not turn a short stakeholder brief into a tutorial or a conceptual explanation into an installation guide.

## Control depth without losing the mechanism

Open with a sentence the reader can place: what the system or idea does, why it matters here, or what decision is needed. Give unfamiliar concepts a concrete subject and action before naming their abstractions. Define acronyms only when they recur and help the reader.

Explain the mechanism at the smallest useful scale, often with one well-chosen example, then generalize. If an analogy helps, state its limit before it implies a false technical relationship. Do not equate probabilistic behavior with a guarantee or describe an observed association as a mechanism.

Keep technical terms that preserve important distinctions. Explain “spatial resolution” when needed rather than replacing it with “image quality.” A reader may need to distinguish spatial, temporal, and spectral resolution to understand the claim.

Use supporting detail in an appendix, link, or later paragraph when the audience needs access to it but not during the first read. Do not include implementation trivia just to signal expertise. Do not hide a condition or limitation that would change the reader's decision.

## Make implications concrete

Connect a fact to its consequence: what changes in cost, effort, reliability, capability, or scientific interpretation? Use only supported quantities and examples. Mark projections, illustrative scenarios, and assumptions as such. “Faster” needs a comparison; “easier” should identify whose effort falls and which step changes.

For non-specialists, explain what uncertainty changes about the conclusion. Avoid stripping away qualifiers or burying them in jargon. For specialist readers, omit introductory background they already share and give the consequential distinction sooner.

## Match voice and format

Follow a supplied writing sample and the destination's conventions. Use a professional, direct default; be conversational when the context supports it. Do not add fake anecdotes, opinions, humor, or first-person experience to make factual writing sound human.

Choose connected prose for an explanation, lists for steps or parallel options, and tables for genuine comparisons. Use informative headings in a long document when allowed. Do not add an executive summary, glossary, diagram, or repeated conclusion to every artifact.

## Check the reader's understanding

Read without relying on the surrounding chat. Can the intended reader state the main point, describe the mechanism at the promised depth, and identify the main limitation or action? Explain missing connections. Cut repeated summaries and rhetorical flourishes that add no information.

For instructions, check the full sequence for prerequisites, safe ordering, actual success conditions, and avoidable manual work. Count authentication prompts and context switches when relevant. Reuse existing credentials or sessions through supported mechanisms; never embed a password or token in an example.
