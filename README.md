# polysolver Modern

`polysolvermod` is the original [polysolver](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4747795/) HLA typing algorithm re-engineered
in modern style. It offers almost all aspects of the original algorithm, adds
new features, runs faster, and is friendly to pipeline integration.

## Features

* Supports both class I and [II](https://github.com/svm-zhang/polysolverMod?tab=readme-ov-file#class-ii-hla-typing) typing with good accuracy
* Generates analysis-ready HLA alignments for HLALOH detection
* Re-engineered in modern style with
  * Modular design
  * Faster runtime with internal optimization
  * Minimum I/O operations
  * Minimum hard-coded code
  * Easy integration to pipeline with packaging and better CLI


## Installation

Please refer to [INSATLL](INSTALL.md) for details.

## Quick Start

`polysolvermod` requires
* Sorted genomic alignment in BAM format with index
* HLA reference sequence in Fasta and Nix (novoalign index)
* BED file with region of each HLA allele
* HLA kmer tags
* HLA 4-digit supertype frequency table

Let us type class 1 alleles for `NA12046` sample provided by the 1000
genome project:

```
polysolvermod --bam NA12046.so.bam \
  --hla_ref abc_complete.fasta \
  --bed class1.bed \
  --tag abc_v14.uniq \
  --freq HLA_FREQ.txt \
  --outdir "$PWD/NA12046_class1 \
  --sample NA12046
```

The command above generates HLA typing results in the designated output
directory specified by `--outdir` option. A quick peek into the result
folder looks like:

```
-- NA12046_class1
   -- finalizer
   -- fisher
   -- realigner
   -- typer
```

## Explain Output

The `finalizer` folder provides the sample-level HLA reference sequence that
can be directly used as reference for realigning tumor data in a paired tumor 
and normal setting. There is also an alignment result in BAM against this
sample-level reference with suffix `hla.realn.ready.bam`. In context of oncology
or immuno-oncology research, the BAM file can be directly ported to program to
detect HLA loss of heterozygosity.

The typing result can be found within the `typer` folder, with suffix
`hlatyping.res.tsv`. The result table should look like the following:

```
allele  gene    tot_scores      sample
hla_a_01_01_29  hla_a   2452923.4298    NA12046
hla_a_02_05_01  hla_a   1766396.924     NA12046
hla_b_50_01_01  hla_b   1332194.9171    NA12046
hla_b_57_01_08  hla_b   1134814.4428    NA12046
hla_c_06_02_01_01       hla_c   3020505.4303    NA12046
hla_c_06_02_01_02       hla_c   1519636.0349    NA12046
```

## Step by Step

## Class II HLA typing


## Disclaimer

## Citation

Please cite the original [polysolver](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4747795/) paper

If you use `polysolvermod`, please cite this github repo as well.