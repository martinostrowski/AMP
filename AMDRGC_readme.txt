*********************************************************************
* The Australian Marine Microbes Reference Gene Catalog (AMDRGC)               *
*********************************************************************

*********************************************************************
* Download                                                          *
*********************************************************************

OM-RGC_seq.release.tsv.gz
	 [ Size: X.X GB | MD5 sum: XXX ]

*********************************************************************
* File scheme for AMDRGC_seq.release.tsv                            *
*********************************************************************

Contains all reference genes in a single .tsv file for easy insertion
into databases. Field separator is a single 'tab' or '\t' character.
Each row contains the following information:

 1. OM-RGC_ID      Identifier of the sequence (OM-RGC.v1.XXXXXXXXX)
 2. GeneID	   Original gene identifier of representative sequence
# 3. eggNOG_OG  	   eggNOG annotated orthologous group(s) of this gene
		   (if available)
 4. KEGG_ko 	   KEGG annotated KEGG orthology of this gene (if 
		   available)
 5. KEGG_module    KEGG module(s) of this gene (if available)
 6. kingdom 	   Taxonomic annotation (Kingdom)
 7. phylum	   Taxonomic annotation (Phylum)
 8. class	   Taxonomic annotation (Class)
 9. order	   Taxonomic annotation (Order)
10. family	   Taxonomic annotation (Family)
11. genus	   Taxonomic annotation (Genus)
12. species	   Taxonomic annotation (Species)
13. sequence	   Nucleotide sequence of the gene

Empty cells are denoted by "" (two double-quotes). Unknown Taxonomic 
annotations are marked as 'undef' (without the quotes).

*********************************************************************
* Disclaimer                                                        *
*********************************************************************
The data have been generated according to current standards of
scientific conduct. However, gene coding nucleotide sequences
represent computational predictions only and accuracy of taxonomic
and gene functional assignments dependent on the completeness of
reference databases used for annotation. Thus, the data provider
cannot be held responsible for potential mispredictions or
misannotations.

Last change: ref