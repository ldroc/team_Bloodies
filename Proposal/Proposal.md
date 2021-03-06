# Project Proposal
Team Bloodies  
2017-02-14  
## Data-driven analysis of the role of transcription factors in hematopoietic stem cell differentiation into six progenitor compartments.

**Background & Motivation:** 
Human hematopoietic cells capable of regenerating the lifelong production of all types of mature blood cells are applied to curative clinical therapies for numerous hematologic malignancies and congenital diseases [1]. Blood differentiation initiates at the level of multipotent stem cells and passes through a series of increasingly lineage-restricted progenitor intermidiates [2]. Due to the rarity of these progenitors and difficulties to obtain human samples, the mechanisms that regulate lineage commitment of human cells remain poorly understood. Transcription factors (TFs) and their interactions within gene regulatory networks are central to the intracellular decision making processes [3]. However, much remains to be learned about the way in which individual factors are connected within wider regulatory networks. Recent studies implicated that the chromatin state foreshadows transcriptional programs in differentiated cells [4][5][6]. Our overall hypothesis is that TFs binding to the active epigenomic regions play a pivotal role in the differentiation programs during early lineage commitment of HSCs. Our objective is to identify specific TFs primarily responsible for the differential gene expression in committed progenitors by combining epigenomic and transcriptomic data in seven hematopoietic stem/progenitor populations.  

So far only two resources, the Canadian CEEHRC Network and the BluePrint Epigenome project have been available for comprehensive epigenomics of human blood cells. As part of the latter, Farlik M. et al recently generated DNA methylation profiles with RNA-seq data for HSC and six progenitor populations, which characterized differential DNA methylation at transcription factor binding sites (TFBSs) as cells commit to different lineages [6]. However, the TFBS database they used was from a collection of cell lines from various malignant/normal tissues, which might increase the noise for identification of true functional TFs in our targeted populations. Alternatively, we will use a motif enrichment analysis in the recognized active DNA methylation regions in the particular cell type [5][7]. In addition, their study mainly focused on DNA methylation at the promoter regions, however, it has been shown in mouse HSCs that DNA methylation at enhancers was more informative for lineage commitment prediction [4]. Therefore, we will also focus on enhancer regions by integrating the genomic information from the Ensembl Regulatory Build [8].

**Division of labor:**
---
| Name | Initial work assignment | Affiliation | Expertise |
| ------------- | ------------- | ------------- | ------------- |
| Annie Cavalla | Section 3: TF binding site enrichment | Bioinformatics | Cancer genomics |
| Rawnak Hoque  | Section 2/5: RNA-seq analysis of differentially expressed genes; TF binding site enrichment | Genome Science and Technology | Genome scale data analysis
| Fangwu Wang | Section 4/5: TF pattern analysis; Leukemia correlation | Medical Genetics | Stem cell biology
| Somdeb Paul  | Section 1: DNA methylation analysis | Genome Science and Technology | Transcriptomics |
---
All members will also have input into the poster on their area of expertise.


**Datasets:**
We will work with DNA methylation (bisulfite-seq) and RNA-seq data from the published BluePrint Epigenome project [6] which were downloaded from GEO (GSE 87197). All samples were collected from primary human peripheral blood cells in seven stem/progenitor populations: HSC, MPP, CMP, CLP, GMP, MEP, MLP. The DNA methylation data is alignment raw data at single base resolution and quality control of sequencing is available at RnBead website [9]. For each population, we chose three samples (biological replicates) with multiple pools (technical replicates). The corresponding RNA-seq data from same populations was obtained from GEO (GSE 87195). The data has been processed with differential expression analysis on transcript level and we will further quantify it on the gene level.
Since this RNA-seq dataset for normal hematopoietic populations does not have sample replicates within cell types, we will leverage the results of our TF enrichment and gene expression analysis on RNA-seq data from AML and CLL patient data from BluePrint. The RNA-seq data are available for 17 AML and 7 CLL patient samples in the format of RSEM. 

**Aims and Methods:**

1.Identify active DNA methylation regions and associate with genes: use RnBeads package to sum up the reads from all replicates and estimate methylation values; quality control; differential methylation analysis with RnBeads; define (set threshold) and identify hypomethylated regions for each population; map regulatory regions (promoter, enhancer) to the hypomethylated regions by integrating Ensembl Regulatory Build genomic information [8]; identify genes associated with the regulatory regions.

2.Pairwise differential expression analysis to identify upregulated genes in each differentiated progenitor: convert/assign the transcript level to the gene level; create heatmap to visualize the “signature” of each population; pairwise comparison of gene expression between directly related populations (HSC vs MPP, MPP vs CLP, MPP vs CMP, CLP vs MLP, CMP vs GMP, CMP vs MEP); take the overlap between genes associated with active regulatory regions (step 2) and highly expressed genes from pairwise comparison to generate lists of upregulated genes for each population pair. 

3.TF binding site enrichment analysis to find potential TF associated with differentiation cell types: map the TF binding motif to the regulatory regions of upregulated genes from step 3 (Homer v4.8 findMotifsGenome.pl tool); generate a list of “active” TFs for population pairs; statistical analyses indicating the enrichment analysis makes sense and does not happen by chance.

4.Decipher the patterns of TF functions in cell differentiation: in each population, inspect the DNA methylation state and gene expression levels of active TFs; Use ANOVA test to compare the methylation and gene expression levels of TFs across the seven populations to see whether TFs show lower methylation and higher expression in the population they were identified as active; We will use these active TFs to derive a TF regulatory network for each population [7]. To construct these networks, we infer a positive/negative interaction between two TFs whenever a binding site for one of the TFs is found in regulatory regions using Ensembl regulatory build genomic information for the other TF and expression of the two TF genes was positively/negatively correlated (absolute Spearman correlation coefficient > 0.25 from RNA-seq data). 

5.Gene expression analysis in different types of leukemia: leukemia tumorigenesis is frequently associated with dysregulation of differentiation programs. To evaluate whether the characteristic TFs identified from different progenitor populations are positively correlated with leukemia with corresponding cell of origin (myeloid vs lymphoid), we will analyze expression profiles of at least two leukemia types (AML and CLL), representing myeloid and lymphoid lineages respectively. We will use Limma to perform differential expression analysis. Then we will perform clustering of all patient samples based on the expression of the TFs we identified from the previous analyses to see if TFs also play a similar role in lineage determination in leukemia.


**References**:

1. Miller PH, Knapp DJ, Eaves CJ. Heterogeneity in hematopoietic stem cell populations implications for transplantation. Curr Opin Hematol. 2013 Jul;20(4):257-64.  

2. Notta F, Zandi S, Takayama N, et al, Distinct routes of lineage development reshape the human blood hierarchy across ontogeny.Science. 2016 Jan 8;351(6269):aab2116.  

3. Göttgens B. Regulatory Network Control of Blood Stem Cells. Blood. 2015 Apr 23;125(17):2614-20.  

4. Yu VW, Yusuf RZ, Oki T et al. Epigenetic Memory Underlies Cell-Autonomous Heterogeneous Behavior of Hematopoietic Stem Cells. Cell. 2016 Nov 17;167(5):1310-1322.e17.  

5. Lara-Astiaso D, Weiner A, Lorenzo-Vivas E, et al. Immunogenetics. Chromatin state dynamics during blood formation. Science. 2014 Aug 22;345(6199):943-9.  

6. Farlik M, Halbritter F, Müller F, et al. DNA Methylation Dynamics of Human Hematopoietic Stem Cell Differentiation. Cell Stem Cell. 2016 Dec 1;19(6):808-822.  

7. Pellacani D, Bilenky M, Kannan N, et al. Analysis of Normal Human Mammary Epigenomes Reveals Cell-Specific Active Enhancer States and Associated Transcription Factor Networks.Cell Rep. 2016 Nov 15;17(8):2060-2074.  

8. Zerbino DR, Wilder SP, Johnson N, et al. The Ensembl Regulatory Build. Genome Biol. 2015 Mar 24;16:56.   
9. http://www.medical-epigenomics.org/papers/BLUEPRINT_methylomes/data/rnbeads_reports/prog_v08_um_nsc/index.html
