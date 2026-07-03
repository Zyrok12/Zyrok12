# Bruno Young de Castro

**Computational Genomics | Pharmacogenomics | ML/AI for Precision Medicine**

I am an M.Sc. student in Genomics, Informatics, Mathematics and AI for Health
(GENIOMHE) at Universite Paris-Saclay and a Cell & Molecular Biology graduate
from the University of South Florida.

I build reproducible bioinformatics tools for pharmacogenomics, oncology-relevant
genomics, assay-design review, and translational research. My current focus is
turning sequencing data into evidence that is useful, auditable, and honest about
its technical limits.

## Featured Work

### PGX Pipeline - private WES pharmacogenomics research platform

Private research-use platform for local WES pharmacogenomics analysis. It accepts
FASTQ, BAM/CRAM, raw VCF, or filtered VCF inputs and produces annotated SNV,
indel, CNV, PGx, cohort analytics, MegaVCF, and report outputs.

Key elements:

- Local browser-based workflow with reproducible run manifests and audit-friendly
  outputs.
- VEP annotation and PGx enrichment using resources such as PharmGKB, CPIC,
  PharmVar, DPWG, ClinVar, and gnomAD.
- Star allele, diplotype, and phenotype layers for pharmacogene review.
- Five-caller WES CNV ensemble using CNVkit, ExomeDepth, GATK-gCNV, CODEX2, and
  panelcn.MOPS.
- MegaVCF Explorer for combined SNV, indel, and CNV review.
- Responder/non-responder analytics and ML workbench outputs for research
  cohorts.
- Validation work against GIAB HG002, CDC GeT-RM PGx consensus, and planted-truth
  synthetic cohorts.

Status: private repository, research-use software, not a diagnostic device.

### [Panel Bias Auditor Lite](https://github.com/Zyrok12/Panel-Bias-Auditor)

Dependency-light Python CLI and research toolkit for auditing genomic panel
designs against biological and technical risk tracks.

What it does:

- Measures panel footprint and critical-region coverage.
- Flags overlap with difficult regions such as low mappability, GC extremes,
  homology, pseudogene-like sequence, and reference-bias tracks.
- Checks whether supplied VCF variants fall inside or outside the panel and risk
  tracks.
- Produces Markdown, HTML, and JSON reports.
- Derives empirical GC-extreme, homopolymer, and low-complexity tracks from FASTA
  sequence.
- Tests whether technical-risk tracks are enriched in assay failures or low
  callability benchmark regions.
- Converts public benchmark/callability BEDs into an assay-performance-style
  schema for exploratory validation.

Stack: Python, CLI design, BED/VCF parsing, JSON/Markdown/HTML reporting,
unit tests, reproducible demo data.

### [TCGA-BRCA Differential Expression Analysis](https://github.com/Zyrok12/tcga-brca-differential-expression)

Reproducible R/Bioconductor workflow for TCGA breast cancer RNA-seq analysis.

Includes:

- TCGA-BRCA data retrieval with TCGAbiolinks.
- DESeq2 differential expression analysis.
- Volcano plot and heatmap visualization.
- ERBB2 Kaplan-Meier and Cox survival analysis.
- LASSO classifier with cross-validated lambda selection.
- Gene Ontology enrichment with clusterProfiler.

Stack: R, Bioconductor, TCGAbiolinks, DESeq2, survival, glmnet,
clusterProfiler, EnhancedVolcano.

### Coursework and Data-Challenge Projects

- Deep learning/autograd framework from scratch in Python/NumPy.
- CardI-HACK clinical genomics challenge: PRS and dual-outcome MACE/severity
  classifier from clinical and genetic features.
- Genome annotation pipeline coursework using BLAST, soft-masking, gene
  prediction, and GFF3 generation.
- scikit-learn-style OOP machine-learning library from scratch.

## Publications

**Young de Castro B.**, Parsons R.F., van der Vaart A.  
[Register-Shifted Structures in Uracil:Adenine and Uracil:Guanine Base-Paired DNA](https://doi.org/10.1021/acs.biochem.5c00796)  
*ACS Biochemistry*, 2025.

Second-author manuscript in preparation with the Uddin Genomics Lab: epigenome-
wide association study of glucocorticoid pathway methylation in PTSD.

## Technical Stack

**Languages:** Python, R, Bash, C/C++  
**Python:** NumPy, Pandas, scikit-learn, PyTorch, Flask, unittest  
**R/Bioconductor:** DESeq2, limma, minfi, TCGAbiolinks, clusterProfiler  
**Genomics:** WES/PGx pipelines, VEP, GATK, FreeBayes, DeepVariant, CNVkit,
ExomeDepth, CODEX2, panelcn.MOPS, PyPGx, PharmVar, CPIC, DPWG, PharmGKB,
ClinVar, gnomAD, RNA-seq, EWAS/GWAS  
**ML/statistics:** survival analysis, LASSO/Cox models, random forest, SHAP,
Transformers, VAE, PLINK2 association testing, Fisher exact testing  
**Compute:** Linux/WSL, HPC, Docker/Apptainer, Conda, Git, reproducible
manifests

## Research Principles

- Keep clinical interpretation separate from technical call confidence.
- Report limitations as clearly as successes.
- Prefer reproducible manifests, versioned resources, and machine-readable
  outputs.
- Treat research signals as hypotheses until validated against appropriate truth
  sets or orthogonal evidence.

## Links

- [LinkedIn](https://www.linkedin.com/in/brunoyoungdecastro/)
- [ORCID](https://orcid.org/0009-0001-5757-2056)
- Email: brunoyc@icloud.com
