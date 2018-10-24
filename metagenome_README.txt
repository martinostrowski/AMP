
### preliminary version -do not use: 2016

Here is a full set of processes used to prep the metagenome data. version 11 October 2016

## merge lanes and rename to contextually relevant IDs e.g. [full list appended]
cat 21734_1_PE_700bp_MM_UNSW_HM7K2BCXX_ATGCGCAG-GCGTAAGA_L001_R1.fastq.gz 21734_1_PE_700bp_MM_UNSW_HM7K2BCXX_ATGCGCAG-GCGTAAGA_L002_R1.fastq.gz > ss2010_v09.064.0m_206.R1m.fq.gz;

## use TRimmomatic defaults to trim and check for adapters while preserving paired reads
## nb: 4 output files

java -jar ~/Trimmomatic-0-2.36/trimmomatic-0.36.jar PE MAI20130807d0.R1.fq.gz MAI20130807d0.R2.fq.gz MAI20130807d0.fp.fq.gz MAI20130807d0.fu.fq.gz MAI20130807d0.rp.fq.gz MAI20130807d0.ru.fq.gz ILLUMINACLIP:/Users/mostrowski/Downloads/Trimmomatic-0-2.36/adapters/NexteraPE-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36;

##add a name prefix to all sequences, e.g. Maybe doesn't need to be done at this step but it would be easier to parse results from the mapping against the reference set of genes, and it can be used for the miTAG approach of TARA oceans.

cat IN2015_v03.022.cmaxm.ip.fq | awk 'NR % 4 == 1 {sub(/^@/,"@IN2015_v03.022.cmaxm;")} {print}' | gzip -c > IN2015_v03.022.cmaxm.ipr.fq.gz;
cat IN2015_v03.022.cmaxm.fu.fq | awk 'NR % 4 == 1 {sub(/^@/,"@IN2015_v03.022.cmaxm;")} {print}' | gzip -c > IN2015_v03.022.cmaxm.fur.fq.gz;
cat IN2015_v03.022.cmaxm.ru.fq | awk 'NR % 4 == 1 {sub(/^@/,"@IN2015_v03.022.cmaxm;")} {print}' | gzip -c > IN2015_v03.022.cmaxm.rur.fq.gz;

## interleave paired ends, anticipating making it easier for some assemblers. (##not needed for megahit)

## python ~/bin/interleave_fastq.py ss2010_v09.031.0m_101.fpr.fq ss2010_v09.031.0m_101.rpr.fq > ss2010_v09.031.0m_101.ipr.fq; 

## run megahit assembler on each sample, ask for min contig length of 500

~/megahit/megahit --min-contig-len 500 --12 ss2010_v09.064.32m_207.ipr.fq -r ss2010_v09.064.32m_207.fur.fq,ss2010_v09.064.32m_207.rur.fq -o ss2010_v09.064.32m_207

## predict genes on > 500 bp contigs using Metagenemrak

~/MetaGeneMark_linux_64/mgm/gmhmmp -a -d -f G -m ~/MetaGeneMark_linux_64/mgm/MetaGeneMark_v1.mod ss2010_v09.031.0m_101/final.contigs.fa.500.fasta -o ss2010_v09.031.0m_101/ss2010_v09.031.0m_101.gff -D ss2010_v09.031.0m_101/ss2010_v09.031.0m_101.orfs.nt;

## cluster all predicted orfs to generate a reference set of genes sequences (RGC) at 95% nucleotide identity

cd-hit-est -c 0.95 -T 12 -M 0 -G 0 -aS 0.9 -g 1 -r 1 -d 0 -i ss2010.v09.orfs.nt -o ss2010.v09.orfs_


## perl script to rename seqs so they are all unique. (Would be nice to keep gene length information)
 
perl -ane 'if(/^\>gene_\d+/){$a++;print ">PHB.NSI.2017_$a\n"}else{print;}' test.fa

## check gene names are unique

cat ss201X_orfs_2017_v2 | grep '>' | cut -f 1 -d '|' | sort | uniq -c

~/bin/fasta-splitter.pl --n-parts 100 indigo.final.contigs.500.orfs_2016.fna

##mapped back with blastn 

see qsub script below

annotate RGC against TARA OMRGC, translate clustered RGC genes and use Diamond to annotate against nr. Other options include eggNOG classifier (eggNOG), uniprot, TransAAP. 

### blast hits are filtered. matches are at least 60 nt, 60% alignment length. annotations go to file XXXXXX

### process 2 column hits to a gene by site abundance atable using handy python script 2c2tabt.py


analyse counts  using favourite package




ss201x conditions

	voyage	depth	voyage	region
ss2012_t07.001.25m	ss2012cmax	cmax	ss2012	ASTS
ss2012_t07.001.5m	ss2012surf	surf	ss2012	ASTS
ss2012_t07.004.25m	ss2012cmax	cmax	ss2012	ASTS
ss2012_t07.004.5m	ss2012surf	surf	ss2012	ASTS
ss2012_t07.006.25m	ss2012cmax	cmax	ss2012	ASTS
ss2012_t07.011.45m	ss2012cmax	cmax	ss2012	CS
ss2012_t07.011.5m	ss2012surf	surf	ss2012	CS
ss2012_t07.012.5m	ss2012surf	surf	ss2012	CS
ss2012_t07.012.75m	ss2012cmax	cmax	ss2012	CS
ss2012_t07.014.120m	ss2012cmax	cmax	ss2012	CS
ss2012_t07.014.5m	ss2012surf	surf	ss2012	CS
ss2012_t07.017.5m	ss2012surf	surf	ss2012	CS
ss2012_t07.017.75m	ss2012cmax	cmax	ss2012	CS
ss2013_t03.009.5m	ss2013surf	surf	ss2013	ASTS
ss2013_t03.012.5m	ss2013surf	surf	ss2013	ASTS
ss2013_t03.013.15m	ss2013cmax	cmax	ss2013	ASTS
ss2013_t03.013.5m	ss2013surf	surf	ss2013	ASTS
ss2013_t03.014.35m	ss2013cmax	cmax	ss2013	ASTS
ss2013_t03.015.5m	ss2013surf	surf	ss2013	ASTS
ss2013_t03.016.80m	ss2013cmax	cmax	ss2013	ASTS
ss2013_t03.017.5m	ss2013surf	surf	ss2013	ASTS
ss2013_t03.018.70m	ss2013cmax	cmax	ss2013	CS
ss2013_t03.019.5m	ss2013surf	surf	ss2013	CS
ss2013_t03.020.30m	ss2013cmax	cmax	ss2013	CS
ss2013_t03.022.5m	ss2013surf	surf	ss2013	CS
ss2013_t03.022.cmaxm	ss2013cmax	cmax	ss2013	CS


### forward reads are mapped against the RGC using blastn+
### forward reads are composed of all joined (filtered+ trimmed forward and reverse reads joined with flash) concatenated with all unjoined forward reads

flash --max-overlap=220 --interleaved-input NSI20150731d50.ipr.fq.gz -o NSI20150731d50.j -d joined;

#### qsub script for RGC mapping
#!/bin/bash
#PBS -N MAI.RGC.2 array
#PBS -S /bin/bash
#PBS -t 1-3600
#PBS -l nodes=1:ppn=12:slave
#PBS -l mem=40000m
#PBS -l walltime=1000:00:00
#PBS -M martin.ostrowski@mq.edu.au
#PBS -m bae
#PBS -d /disks/sheldon/data/martin/
#PBS -e /home/martino/${PBS_JOBID}.err
#PBS -o /home/martino/${PBS_JOBID}.out


cd ${PBS_O_WORKDIR}
echo "Job ID is ${PBS_JOBID}"
echo "Job Array ID is ${PBS_ARRAYID}"
echo "Timestamp is $(date +%F_%T)"
echo "Directory is $(pwd)"
echo "Running on host $(hostname)"
echo "Working directory is ${PBS_O_WORKDIR}"
echo "Job has the following nodes/cores:"
cat ${PBS_NODEFILE}

PARAMETERS=$(awk -v line=${PBS_ARRAYID} '{if (NR == line) { print $0; };}' ${PBS_O_WORKDIR}/mai2.conf)

date +%F_%T
echo "file working on is $PARAMETERS"
/usr/local/bin/blastn -db /home/martino/MAI.PHB.NSI.2017_orfs.rename.nt -outfmt='6 qseqid sseqid pident length mismatch gapopen qlen qstart qend sstart send evalue bitscore' -max_target_seqs  1 -best_hit_overhang 0.1 -ungapped -dust no  -num_threa$
date +%F_%T

#### 2c2tabt.py

from collections import Counter
with open("ss201X.rgc.genes.u.60.2c.hitlist") as f:
    next(f)  # do this to skip the first row of the file
    c = Counter(tuple(row.split()) for row in f if not row.isspace())

sites = sorted(set(x[0] for x in c))
genes = sorted(set(x[1] for x in c))

print 'genes\t', '\t'.join(sites)
for gen in genes:
    print gen,'\t', '\t'.join(str(c[site, gen]) for site in sites
)






