---
name: pipeline-hpc-reproducibility
description: >
  Pipeline, HPC, and reproducibility judgment for the lab, plus the recurring genomic-data
  traps. Use when building an analysis pipeline, running jobs on GenomeDK or a SLURM cluster,
  managing environments or containers, making an analysis reproducible, or debugging
  reference-build, contig-prefix, liftover, or VCF-normalization problems. Some cluster details
  are lab-specific fill-ins to confirm.
---

# Pipeline, HPC, and Reproducibility

How we build things that rerun and produce the same answer, and the data traps that break them.
Where a choice is the lab's own it is marked LAB CALL; confirm it with the lab.

## Choosing a workflow manager

- **Snakemake** for a file-graph pipeline in a Python-native lab. Rules, wildcards, and
  dependency tracking; reruns only what changed.
- **Nextflow** when portability or the nf-core ecosystem matters, or the pipeline must run
  across environments and institutions.
- **targets** for an R-centric analysis; it does for R what the above do for shell steps.
- **Plain SLURM scripts** only for genuine one-offs. Anything you will rerun deserves a manager.

LAB CALL: the house default and the threshold at which a script becomes a managed pipeline.

## HPC and SLURM patterns

On GenomeDK or a comparable SLURM cluster:

- Do not run heavy work on login nodes. Submit it. Login nodes are shared and get you throttled.
- Use the module system and a per-project mamba or conda environment together; do not pollute a
  base environment.
- Request memory and time honestly. Overrequesting wastes queue priority; underrequesting kills
  the job at the worst moment. Measure a small run, then scale the request.
- Use array jobs for embarrassingly parallel work rather than a loop that submits thousands of
  jobs.
- Checkpoint long jobs so a timeout or preemption does not cost the whole run. Use scratch for
  heavy intermediate I/O and move final outputs to project or home; know the retention policy on
  scratch before you trust it.

LAB CALL: GenomeDK specifics worth encoding (module names, scratch versus project paths,
partitions, retention, typical resource requests for the lab's common jobs).

## Environments and reproducibility

- One pinned environment per project; commit the lockfile. See python-craft for the
  uv-versus-mamba choice.
- Containerize anything you will rerun or publish. On HPC that means Singularity or Apptainer,
  not Docker. A container pins the whole stack, not just the Python packages. LAB CALL: the
  lab's container standard and where images live.
- Record tool and reference versions in the outputs, not just the code. A result you cannot tie
  to the versions that made it is not reproducible.
- Version-control the pipeline itself, seed RNGs, and aim for byte-reproducible reruns where the
  tools allow it.

## The genomic-data traps

The recurring ones, with commands and symptoms, are in
[references/genomics-data-traps.md](references/genomics-data-traps.md). The classes to watch:

- **Reference build mismatch.** GRCh37/hg19 versus GRCh38/hg38. Coordinates from one build are
  meaningless against the other. Confirm the build of every file before combining files.
- **Contig-prefix mismatch.** `chr1` versus `1`. Tools silently find no overlap when contig
  naming differs between a VCF and its reference or annotation. This is a frequent cause of a
  pipeline step that runs cleanly and returns nothing.
- **Liftover artifacts.** Lifting coordinates between builds drops unmapped variants, can
  multi-map, and can flip strands. Liftover is lossy; check what fell out and never treat a
  lifted file as equivalent to a natively-called one.
- **VCF normalization.** Left-align indels and split multiallelic sites (`bcftools norm`) before
  comparing or annotating, or the same variant represented two ways will look like two variants.
- **Sample and header mismatch.** Sample-ID and contig-order mismatches between files break
  merges and annotation. Reconcile headers before combining.

These are exactly the problems that surface when running a VCF through a genotyping or
annotation pipeline, including PGx callers. Fix the data prep first; most downstream "tool bugs"
are upstream build, contig, or normalization problems. LAB CALL: the build and contig
conventions the lab standardizes on for genomic data.
