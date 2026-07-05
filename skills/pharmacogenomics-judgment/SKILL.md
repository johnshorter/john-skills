---
name: pharmacogenomics-judgment
description: >
  Pharmacogenomic judgment for the lab. Use for star-allele or diplotype calling, CYP
  genotype-to-phenotype translation, PGx panel design, applying CPIC or DPWG guidelines, or PGx
  reporting and implementation. Some calls are lab-specific fill-ins to confirm.
---

# Pharmacogenomics Judgment

This captures decisions, not textbook facts. Where a choice is the lab's own it is marked
LAB CALL; ask the lab and fill it in before relying on this skill. Like the peer-review skill's
stance on evidence: surface what is uncertain, do not paper over it.

## What the assay can call

The genotyping platform sets the ceiling on what is callable, before any software runs.

- **Genotyping arrays** capture the common defining variants but miss rare and structural
  variation. They will not resolve most novel or population-specific alleles.
- **Targeted panels** cover their designed loci well and little else.
- **WGS or WES** can in principle call more, but coverage, phasing, and structural resolution
  still limit the hard genes.

CYP2D6 is the hard case: copy-number variation, gene deletions, duplications, and CYP2D6-CYP2D7
hybrids. A caller that ignores structure will misclassify it. CYP2C19, CYP2C9, and others are
easier but still depend on which defining variants the assay typed.

State the assay before interpreting a call. A confident diplotype from a platform that could
not have seen the relevant variant is a false confidence.

## Choosing a caller

The tool comparison is in [references/star-allele-callers.md](references/star-allele-callers.md):
PharmCAT, pypgx, Stargazer, Aldy, and where each fits. The decision turns on the input data
type, whether the tool handles CYP2D6 structure, and whether it needs phased input.

LAB CALL: which caller is the house default, for which data, and why. If the lab moved between
callers, capture the reason, because that reason is exactly the judgment worth keeping.

## The diplotype and phenotype pitfalls

- **Overlapping defining variants.** Some star alleles are defined by variants that also
  define others (the classic confusion around alleles distinguished only by phase). Without
  phase, the call is ambiguous, and different callers resolve the ambiguity differently.
- **Reference-allele assumptions.** A missing call is not a reference call. Tools differ in how
  they treat no-calls, and treating absence as wild type inflates the wild-type frequency.
- **Sanity checks that catch misclassification.** Compare called allele frequencies against a
  matched population reference; a large deviation signals a calling or reference-build problem.
  Check Hardy-Weinberg on the calls. Run a second caller on a subset and check concordance;
  systematic disagreement points at a structural or phasing issue, not noise.

LAB CALL: the specific misclassification the lab has hit and the check that catches it. Capture
it verbatim; a known trap with a known check is the highest-value thing in this file.

## Genotype to phenotype

- **CPIC and DPWG** are the two guideline bodies. They do not always agree on the
  diplotype-to-phenotype mapping or the resulting recommendation. Pick one framework per project
  and say which. LAB CALL: which framework is the lab's default, and why.
- **Activity scores** translate diplotypes to metabolizer phenotypes, but the intermediate
  metabolizer boundary is where the ambiguity and the disagreements concentrate.
- **Guidelines update.** Pin the guideline and allele-definition version used, and record it in
  the output. A phenotype call is only reproducible against a stated version.

## Panel design

For a targeted PGx panel or passport, gene and allele selection is a judgment call: actionable
gene-drug pairs, alleles common in the target population (Nordic and Danish frequencies differ
from the global reference), and what the assay can actually type.

LAB CALL: the gene and allele content of the lab's panel and the rationale for each inclusion.

## Reporting and implementation

Use standardized diplotype and phenotype nomenclature so a report is portable. If the
interpretation is delivered as software, it is regulated: PGx interpretation software can fall
under IVDR, which changes what you can ship and what evidence you need. Flag this early and get
regulatory and legal sign-off; do not treat a clinical-facing interpreter as just code.
LAB CALL: where the regulatory line sits for the lab's interpretation tooling.
