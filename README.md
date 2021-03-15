# Genomic association of cognitive decline in Parkinson's Disease
Supplementary methods and data 


## Additional Methods

### Participants
Data from the Parkinson’s Progression Markers Initiative (PPMI) de-novo cohort, defined by a diagnosis of PD within two years and unmedicated for motor symptoms at baseline (n=423) were analysed for trajectories of cognitive decline using an education adjusted Montreal Cognitive Assessment (MoCA) as a primary metric for global cognition. Cases were removed that were below a cut-off for severe cognitive impairment at baseline (n = 35) and without a minimum of three longitudinal observations (n = 3). Records were used up to seven years from baseline after which high levels of attrition was observed. Cases had a median of seven follow up observations over a mean of 3 years from baseline. 

### Genotyping and polygenic scores
Whole blood DNA genotyping was performed on the NeuroX array by PPMI investigators following previously published methods. Raw data from 619 individuals covering 267,607 variants was quality assessed following published recommendations. In brief, data was excluded based on the following criteria 1) variants and individuals with missingness >0.1, 2) individuals with discordant reported sex and inferred sex (X chromosome homozygousity F-value >0.8 for males, <0.2 for females), 3) variants with minor allele frequency <0.01 or >0.05, 4) variants deviating from Hardy Weinberg Equilibrium <1e-3, 5) individuals with heterozygousity rate +- 3 standard deviations, 6) individuals with evidence of cryptic relatedness (pi hat >0.2). Following initial QC, autosomal data was extracted, plink files were recoded to vcf format and uploaded to the Michigan Imputation Server. Imputation was conducted using Eagle2 to phase haplotypes and Minimac4 using the 1000 Genomes reference panel (phase 3, version 5). An R2 filter score for imputation quality was set at 0.3. Following imputation, data was downloaded, converted to plink format and quality assessed following the previous criteria. Finally, genetic principal components were generated along with reference data from the 1000 Genomes Project and non-european cases removed based on qualitative assessment of clustering of the first two principle components. 582 cases passed qc (variants n = 2,287,446). 
Polygenic risk scores (PRS) were calculated using summary statistics from recent genome wide association studies for Alzheimer’s Disease (AD)10, Parkinson’s Disease (PD)11, Education Attainment (EA)12, Schizophrenia and Depression. For AD, the effect of the APOE region was excluded by removing the region chr19:45,116,911 – chr19:46,318,605. For PD, the effect of the GBA region was removed by removing . PRSice-2 software was used for polygenic risk score calculation, which automates clumping and p-value thresholding to generate a “best-fit PRS” for a target phenotype of interest. Briefly, clumping was performed to retain the most significant GWAS variants in a LD block (250kb window, r2 threshold = 0.1). The PRS model is tested over an increasing set of p-value threshold (5e-08 to 1), with the optimal threshold set which generates a score explaining the maximum phenotypic variance in the target phenotype of interest. Phenotype was coded as a binary factor of 0 (Control) and 1 (PD) for this analysis, with the first eight genetic principal components as covariates. Summary of PRS models for each GWAS set available in supplementary methods. 

### Methylomic data
Methods for whole blood DNA methylation data generated at baseline has been previously reported. Raw IDAT files were downloaded, quality controlled and normalised following established pipelines using the R package wateRmelon. Briefly, samples with low signal intensities or bisulphite conversion rate, mismatched reported and imputed sex or cryptic relatedness were excluded. P-filtering was applied using the pfilter() function, excluding samples with  >1 % of probes with a detection P value >0.05 and probes with >1 % of samples with detection P value >0.05. 284 de-novo PD cases with latent class annotation passed QC and were carried forward.The minfi package functions read.metharray.exp() and preprocessNoob() were used to generate RGSet objects and blood cell proportions using the estimateCellCounts2() function of the FlowSorted.Blood.EPIC package.Beta values for each probe was quantile normalised using the dasen() function and probes annotated as cross-hybridised or for SNP genotyping removed. Beta values were converted to M values using the beta2M() in the lumi package. Probes annotated to sex chromosomes were removed and sex effect was normalised using the removeBatchEffect() function in the limma package. Median absolute variation for each probe was calculated and the top 100,000 most variable probes were carried forward for analysis. 

### Latent Class Mixed Modelling 
Latent Class Mixed Modelling (LCMM) was conducted using the R package lcmm. MoCA scores showed a skewed distribution with a ceiling effect at the highest cognitive scores and were normalised using the ‘lcmm’ function applying a 5-quant splines model with a quadratic of age of assessment as the time variable. Latent classes were assessed using the ‘hlme’ function with normalised MoCA as the observed variable against a time variable of years from baseline, coded as a quadratic term, based on assessment of residuals of a linear versus quadratic model. Sex and age of assessment were included as fixed effects, along with NUPDRS-III assessed at the ‘off’ medication state, as a measure of underlying motor symptom severity. A quadratic of time as a mixed effect. Models with 1-5 classes were calculated using the ‘hlme’ function and assessed for model fit based on published recommendations9, including lowest Bayes Information Criterion (BIC), high entropy, resulting class size and posterior classification probability. 
