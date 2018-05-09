# BIOC3301

This repository contains all the files used in the analysis of the soil microbiome of Gordon Square Park. The aims of this project were to (i) to confirm the presence of the “rhizosphere effect”, by measuring the difference in microbial richness between bulk soil and rhizosphere samples, as well as investigating the effect of tree species in microbiome composition, (ii) to investigate the phylogeny of the rhizosphere microbial community to confirm the preferential selection of beneficial bacterial species and (iii) to assess whether edaphic factors, such as pH and nutrient concentration, could significantly determine microbial abundance.
All bioinformatic analysis was carried out in the Cirrus supercomputer. All files in this repository are in the Portable Batch System (PBS) format. All jobs were run in 32 cores and completed under 1h wall time.

Raw data processing:
1. Join paired end reads with Seqprep method (1_joined_paired_ends_seqprep.pbs)
2. Demultiplex and quality filtering at q=25 (2_split_libraries.pbs)
3. Identify chimeras using usearch against the SILVA database, v132 (3_identify_chimeric_seqs.pbs)
4. Filter chimeras (4_filter_fasta_chimeras.pbs)
5. Pick closed reference OTUs against SILVA database (5_pick_otus_after_chimera_filtering.pbs)
6. Filter OTU map to create two new mapping files, one containing "bulk soil" and "rhizosphere" samples (i.e. sample types) (6_filter_otus_by_sample.pbs) 
7. Make new OTU tables for comparing sample types ("bulk soil" and rhizosphere") and sample species ("Prunus cerasus" and "Platanus x acerifolia") (7_make_otu_table.pbs)
8. Removing singletons from OTU table (8_filter_singletons.pbs)

Alpha diversity analysis:
9. Rarefy OTU tables (9_rarified_OTU_table_2.pbs)
10. Compute alpha diversity at each rarefaction level (10_parallel_alpha_diversity.pbs)
11. Collate alpha diversity tables (11_collate_alpha.pbs)
12. Make Rarefraction plots (12_make_rarefraction_plots.pbs)
13. Compare Alpha diversity (13_compare_alpha_diversity.pbs)

Beta diversity analysis:
14. Compute jackkniffed beta diversity (14_jackknifed_beta_diversity.pbs)
15. Make 2D PCoA plots (make_2d_plots.pbs)

Taxonomic composition:
16. Summarize taxa through plots (16_summarize_taxa_through_plots.pbs)

Statistical analyses:
17. Measuring the strength and statistical significance of sample groupings (17_compare_categories.pbs)
18. Comparing OTU frequencies across sample groupings (18_group_significance.pbs)
19. Calculating correlations between diversity and different sample groupings (19_observation_metadata_correlation.pbs)
