# Genomic-data traps

The recurring build, contig, and normalization problems, with how they show up and how to fix
them. Commands assume bcftools and standard liftover tooling; adjust to the lab's stack.

## Reference build mismatch (hg19/GRCh37 vs hg38/GRCh38)
Symptom: variants land in the wrong genes, annotations make no sense, positions are off by
build-specific offsets.
Check: confirm the build of every input (VCF header `##reference`, the reference FASTA, the
annotation source) before combining anything.
Fix: bring everything to one build. If you must lift, see below and treat it as lossy.

## Contig-prefix mismatch (`chr1` vs `1`)
Symptom: an intersection or annotation step runs without error and returns nothing, or far
fewer records than expected.
Check: `bcftools view -h file.vcf.gz | grep contig` against the reference and annotation contig
names.
Fix: rename consistently, for example with `bcftools annotate --rename-chrs map.txt`, where
`map.txt` maps `1` to `chr1` and so on. Make the whole pipeline use one convention.

## Liftover artifacts
Symptom: fewer variants after lifting, duplicated positions, or strand-flipped alleles.
Check: count input versus output and inspect the unmapped file the tool emits.
Fix: keep and review the unmapped set, drop multi-mapped variants deliberately, and reconcile
strand. Never assume a lifted file equals a natively-called one on the target build.

## VCF normalization
Symptom: the same variant appears twice, or a comparison between two callsets shows spurious
differences.
Fix: `bcftools norm -f ref.fa -m -both in.vcf.gz -Oz -o norm.vcf.gz` to left-align and split
multiallelics. Normalize both sides before any comparison or annotation.

## Sample and header mismatch
Symptom: merges fail, samples misalign, or annotation attaches to the wrong records.
Check: `bcftools query -l` for sample names, and compare contig order in the headers.
Fix: reconcile sample IDs and header contig order before merging. Do not rely on positional
assumptions.

## General rule
When a genotyping, annotation, or PGx step behaves strangely, suspect the data prep before the
tool. Build, contig naming, and normalization account for most of it.
