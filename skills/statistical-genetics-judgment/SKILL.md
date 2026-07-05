---
name: statistical-genetics-judgment
description: >
  Statistical and psychiatric genetics judgment for the lab. Use for GWAS interpretation,
  polygenic score work, heritability or genetic correlation, Mendelian randomization, ancestry
  and population-structure handling, or psychiatric-genetics analysis. Some calls are
  lab-specific fill-ins to confirm.
---

# Statistical Genetics Judgment

Decisions, not derivations. Where a choice is the lab's own it is marked LAB CALL; confirm it
with the lab. State uncertainty rather than smoothing it over.

## Ancestry and structure

- Match ancestry between the discovery GWAS and the target sample. A score trained in one
  ancestry underperforms in another, sometimes badly. This portability problem is a property of
  the method and the LD structure, not a bug to tune away.
- The LD reference panel must match the ancestry of the data. A mismatched panel corrupts
  clumping, LD-based score methods, and fine-mapping.
- Control for population structure with principal components or a mixed model. Residual
  stratification inflates associations and can manufacture a signal.

## Polygenic score method choice

- Clumping and thresholding is simple and transparent, and often a fair baseline.
- LDpred2, PRS-CS, lassosum, and SBayesR use genome-wide models and usually do better when the
  discovery GWAS is large and well matched. They are more sensitive to LD-panel choice.
- The discovery GWAS dominates. Its sample size and the trait's heritability set the ceiling on
  any score. No method rescues an underpowered or poorly matched base.

LAB CALL: the default PGS method and LD reference, and when to deviate.

## Winner's curse and overfitting

- Do not evaluate a score in the sample it was tuned in. Effect sizes at discovery are inflated
  (winner's curse); evaluate in an independent target.
- Report calibration, not only discrimination. AUC or variance explained is not clinical
  utility, and a well-discriminating score can be badly calibrated.

## GWAS interpretation

- Genome-wide significance is a multiple-testing threshold, not a truth threshold. Replication
  matters more than crossing the line.
- The lead SNP is rarely the causal variant. It tags an LD block. Fine-mapping and
  colocalization, not the top hit, point toward mechanism.
- Association is not mechanism, and it is not causation. Say which you have shown.

## Psychiatric genetics specifics

- Phenotype heterogeneity is the central problem. MDD is not one thing; early versus late
  onset and clinical subtypes differ genetically. Define the phenotype precisely and expect the
  definition to move the result. LAB CALL: how the lab defines and splits its psychiatric
  phenotypes (for example MDD subtypes).
- Cross-disorder genetic overlap is large. Shared signal across psychiatric diagnoses is the
  norm, not a surprise.
- Ascertainment shapes everything. A register-based sample, a clinical sample, and a
  self-report sample give different phenotypes with different noise, and the differences are
  not nuisance, they are structural.

## Mendelian randomization

Treat MR conclusions cautiously. The three assumptions (instrument relevance, independence, and
the exclusion restriction) are mostly untestable. Report sensitivity analyses (Egger, weighted
median, and others), check for pleiotropy, consider reverse causation, and watch for weak-
instrument bias. A single MR estimate without sensitivity analyses is not evidence. LAB CALL:
the lab's standing sensitivity-analysis expectations for MR and PGS work.

## Cohorts

iPSYCH, DBDS, and UK Biobank each carry their own ascertainment and consent structure. UK
Biobank has a well-documented healthy-volunteer bias that affects generalization. Register-based
cohorts inherit the register's ascertainment.

LAB CALL: the specific quirks and access constraints of the cohorts the lab uses, and how they
change an analysis.
