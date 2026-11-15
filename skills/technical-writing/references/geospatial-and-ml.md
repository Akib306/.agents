# Reporting geospatial and ML research

Use the parts relevant to the actual study. These are reporting questions, not permission to invent experimental details or run an unrequested analysis. Flag an absent detail only when it affects reproducibility or a conclusion the document makes.

## Geospatial science and remote sensing

Describe the study region, time interval, sampling or mapping unit, and intended generalization. A large pixel count does not establish broad geographic or temporal coverage.

- **Data identity:** Identify satellite or sensor, platform, product or collection, processing level and version, acquisition dates, and provenance. Distinguish surface reflectance, top-of-atmosphere measurements, radiance, and derived products when relevant. Preserve actual dataset citations and access conditions.
- **Resolution and support:** Report spatial resolution and relevant temporal or spectral resolution. Identify the resolution and geographic support at which results are evaluated or aggregated. Resampling to smaller pixels does not create finer measured detail.
- **Coordinates and alignment:** Report horizontal and, when consequential, vertical reference systems, units, datum, grid, reprojection, and resampling choices. Matching array shapes do not establish spatial alignment. Degree coordinates are not distance or area units; a projected CRS does not automatically preserve area.
- **Preprocessing and missingness:** State cloud, shadow, quality, saturation, and nodata treatment; scale factors and offsets; compositing or mosaicking; and selection exclusions. Distinguish missing or masked observations from measured zeros. Describe relevant SAR calibration, speckle treatment, and terrain correction for radar studies without importing optical assumptions.
- **Reference data:** Identify label origin, timing, coverage, class definitions, annotation process, and uncertainty. Explain temporal or spatial mismatch between labels and imagery when it affects interpretation.
- **Evaluation:** Name the independent unit and how sites, fields, scenes, or regions are partitioned. Adjacent pixels and overlapping patches can leak information. A random pixel split may support interpolation within observed scenes while leaving claims about unseen regions or dates unsupported.
- **Map accuracy:** Name the sampling design and whether the reported accuracy is sample-based, spatially held out, or area-adjusted. Do not infer unbiased area estimates or map-wide accuracy from a convenient test sample. Define producer's/user's accuracy or other class metrics if used, and preserve the class labels and denominators.

Captions for maps should supply the geographic context, legend and units, relevant dates, and scale information the reader needs. Explain uncertainty and missing coverage when they affect the message. Maps need not carry decorative cartographic furniture unrelated to the task.

## Machine learning and AI

Frame results around the actual task and evaluation setting. Name training, adaptation, inference, and evaluation separately.

- **Data and splits:** Report dataset version and scope, sampling unit, exclusions, labels, partition sizes, and split logic. Prevent subject, site, scene, document-family, temporal, or near-duplicate leakage as relevant. Distinguish validation used for model selection from untouched test evaluation.
- **Model and training:** Identify architecture or algorithm, baseline and pretrained checkpoint revisions, initialization, loss, consequential preprocessing, hyperparameter selection, and training budget where available. State fine-tuning or parameter-efficient adaptation rather than implying the full model was trained from scratch.
- **Comparisons:** Keep data access, split, tuning budget, input resolution, preprocessing, and evaluation conditions comparable. Explain departures. An ablation supports a component claim only within the tested changes and interactions.
- **Metrics:** Define metrics, averaging, class balance or prevalence, thresholds, units, and direction. Pair aggregate scores with class or subgroup behavior when the question needs it. Accuracy, F1, AUROC, IoU, and calibration answer different questions.
- **Uncertainty:** Report the supplied number of runs, seeds, intervals, or resampling unit accurately. Variation across random seeds is not the same as uncertainty across populations. Do not invent statistical significance from the size of a score gap.
- **Reproducibility and cost:** Include code or configuration availability, relevant versions, hardware, compute, timing protocol, and memory when the paper makes reproducibility or efficiency claims. Label estimates and targets. A fixed seed alone does not guarantee exact reproducibility.
- **Interpretation:** A feature attribution is not causal proof, a confident model output is not calibrated certainty, and benchmark success alone does not establish deployment reliability or broad intelligence. Report material failure modes and distribution shifts.

For generative AI, identify the model and version, prompts or templates, decoding and retrieval settings, evaluator and rubric, human-rating process if present, and known contamination risks when available and relevant. Distinguish demonstrations from systematic evaluation and model-judged preferences from externally verified correctness.

For geospatial ML, apply both sets of questions. Explain whether the task tests interpolation, new sites, future dates, or another target setting; align the conclusion with the partition actually used.

## Optional implementation companions

The separately installed `geomaster`, `scikit-learn`, and `transformers` skills support actual geospatial and model work. Load them when implementing or diagnosing the corresponding workflow; they are not required to edit a paragraph or write an overview. Do not install scientific packages, download datasets or checkpoints, start training, or request service credentials merely to use this writing guidance.
