# AMP
AMP Metagenomic Workflow Description

## Metagenome Processing Products Description and Purpose



### 1. Australian Reference Gene Catalogue (ARGC)

- A. non-redundant catalogue of predicted gene sequences (> 200 nt, clustered at 95% nt) identity[clustered alongside the marRef <https://mmp.sfb.uit.no> Database?]

- B. gene abundance table (c.f. a zOTU table)

- C. The ARGC can be annotated against any source database

- D. contigs assembled for each discrete sample, with Taxonomic assignment

- E. Predicted gene sequences and protein sequences (fasta files)

#### Tools
- Trimmomatic
- Fastqc
- Spades/megahit
- metagenemark
- cd-hit
- basta

see AMRGC_Readme.txt for a starting point.
see metagenome workflow for details on the assembly and read mapping

#### Discussion: The RGC structure mirrors the structure of the zOTU table and can be delivered to functional interfaces in .biom format and potentially utilise the same suite of ecological tools.

The size of the database approaches 56,000,000 rows, but could be cut significantly by omitting singletons or short sequences (e.g. less than 500) if there was an apetite  or need

Ideally the gene abundances would be calculated with the exact same methods as the EBI profiles for inter comparison with global datasets, however I can’t find documentation on the process so cannot comment on the accuracy or applicability to the AMP data.

#### Format: ideally a subsettable .biom file served from the Bioplatforms Portal

Annotation sources include: best hit and LCA taxonomic assignment against nt, COG/NOG, GO-slim, nr, Interproscan. (Searches against Datbases in bold have been done). The others are not implemented.

***

### 2. SUPER-FOCUS functional characterisation -short term functional classification and enumeration against the SEED database

Discussion: can be implemented quickly. Hierarchal organisation of functional classes at 4 levels. Raw or Filtered reads (Fastq or Fasta) can be analysed

Can be used to produce rapid results. A curated RGC with defined read mapping criteria and inter comparison with global datasets is preferred.

- A. a table of results for all levels and all samples. See “output_all_levels_and_functions.xls”

#### Tools

- SUPER-FOCUS

### 3.  Metagenome Assembled Genomes (MAGs)

- A. Regional coassemblies with metadata file (length, LCA, coverage)



- B. Regional Assembled Genome bins with metadata (length, LCA, coverage, method of binning, contamination, completeness)

	i). Bacterial bins
	ii) Archaeal bins
	iii) Viral bins -complete viral genomes
	iv) eukaryote bins

#### Tools

- bowtie2
- samtools 
- MetaBat 
- GroopM
- Basta
- contig assembler (Geneious, CAP3 etc.)
- CheckM

#### Discussion: Some optimisation may be required to maximise the completeness and reduce contamination during the binning process.

#### Format: ideally a bioproject on one of the database sites

***

# Priorities

Test the complete workflow on datasets that are a priority for the community

- YON
- GAB
- EAC - Amaranta MQ
-  Entire dataset - assembled contigs
