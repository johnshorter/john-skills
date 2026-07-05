# Star-allele callers

A working comparison. Verify current capabilities against each tool's docs before committing;
these move.

| Caller | Input | CYP2D6 structure | Phasing | Notes |
|---|---|---|---|---|
| PharmCAT | VCF (aligned, normalized) | Limited on its own | Uses called genotypes | Broad gene coverage and a built-in guideline annotator; pairs calling with CPIC reporting. Expects a properly prepared VCF. |
| pypgx | BAM or VCF | Handles CNV and structure | Can use phased or unphased | Strong on the structurally hard genes; per-gene models. |
| Stargazer | VCF plus read depth | CNV-aware | Statistical phasing | CNV detection from depth; older, check maintenance. |
| Aldy | BAM | CNV and fusion aware | Own resolution | Good on complex loci including fusions; independent method for a concordance check. |

## How to choose
- Start from the input you have. BAM-based tools can see structure that a genotype-only VCF
  cannot.
- For CYP2D6 or any gene with copy-number and hybrid alleles, use a structure-aware caller.
- Run a second, methodologically different caller on a subset as a concordance check. Agreement
  raises confidence; systematic disagreement localizes the problem.
- Prepare the VCF properly for VCF-based tools: correct reference build, normalized and
  left-aligned, multiallelics split, contig naming consistent. See the
  pipeline-hpc-reproducibility skill for the data-prep traps.
