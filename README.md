# Bruno Young de Castro

**Computational genomics · Pharmacogenomics · Machine learning for precision medicine**

I am an MSc candidate in **Genomics, Informatics, Mathematics and AI for Health (GENIOMHE)** at Université Paris-Saclay, with a BSc in Cell and Molecular Biology from the University of South Florida.

I am interested in a simple question: how can genomic and transcriptomic data be turned into useful, testable hypotheses about disease? My projects combine biology, statistics and machine learning, with a particular interest in pharmacogenomics, cancer dependency and precision medicine. Increasingly they also involve building the software a lab actually needs in order to ask those questions at all.

---

## Flagship projects

### [PGX Pipeline — end-to-end pharmacogenomics for WES cohorts](https://github.com/Zyrok12/pgx-showcase)

**▶ Try it live: [MegaVCF Explorer](https://zyrok12.github.io/pgx-showcase/demo/mega_vcf_explorer.html) · [Analytics Dashboard](https://zyrok12.github.io/pgx-showcase/demo/analytics_dashboard_interactive.html)** — real pipeline output on a synthetic cohort, running in your browser.

Pharmacogenomic cohort work has a tooling gap. Getting from raw reads to something a researcher can interpret means chaining alignment, several variant callers, annotation and a dozen separate knowledge bases together, then repeating the database lookups variant by variant across an entire cohort. Copy-number variants are often skipped altogether because calling them reliably from exome data is difficult — an omission that matters in pharmacogenomics, where a CNV in a gene like *CYP2D6* changes metaboliser status outright. During a research internship in clinical pharmacogenomics I needed that whole path to exist, be reproducible and run locally, so I built it.

FASTQ → alignment → SNV/indel and CNV calling → VEP annotation → pharmacogenomic database enrichment → cohort analytics → an interactive variant browser researchers can actually use. Four entry points (FASTQ, BAM/CRAM, raw VCF, filtered VCF), 19 checkpointed stages, resume and retry.

Validation on GIAB HG002, whole-exome:

| Caller | F1 |
|---|---:|
| GATK HaplotypeCaller | 0.902 |
| Strelka2 | 0.909 |
| DeepVariant | 0.911 |
| PGX ensemble (PASS tier only) | 0.907 |
| **PGX ensemble + ML triage** | **0.929** |

Two design decisions did most of the work. First, calls are tiered PASS/REVIEW/FAIL rather than hard-filtered, and a **calibrated gradient-boosted tree** re-scores the REVIEW tier into P(real) — rescuing 1,373 genuine variants and dropping 215 artifacts on HG002, worth +0.022 F1. Hard thresholds preferentially delete true variants in pharmacogenes, which sit beside pseudogenes and therefore always look borderline. Second, CNVs come from a **five-caller consensus** that merges fragmented bins within each caller before voting, deliberately mixing bin-based and target-based callers so their failure modes do not correlate, and reports breakpoint uncertainty rather than implying precision that WES cannot deliver.

On a synthetic cohort with a planted truth set: F1 0.996 for SNVs/indels and 0.978 for CNVs, with **zero false positives in both validations** — the explicit design goal, since clinical research conclusions must never rest on variants that do not exist.

The showcase repository holds full architecture and methods documentation, validation results with an honest limitations section, and two runnable source excerpts: the triage model and the CNV consensus algorithm. The complete pipeline (~40 modules) remains private as an active research platform. Research use only; it is not a diagnostic device and has not undergone clinical validation.

[Live demos and documentation](https://zyrok12.github.io/pgx-showcase/) · [Repository](https://github.com/Zyrok12/pgx-showcase)

---

### [OncoVulnerability — predicting cancer gene dependencies](https://github.com/Zyrok12/OncoVulnerability)

> Can a cancer model's RNA-expression and genomic profile predict which genes it depends on for survival?

OncoVulnerability is an end-to-end machine-learning project built with public DepMap data. It predicts CRISPR gene-effect values from RNA expression, damaging mutations, copy-number variation and cancer lineage, then ranks the genes most likely to be required by each cancer model.

I developed the project in three versions. V1 established reproducible baselines; V2 expanded the comparison to classical ML and deep-learning models; and V3 assigned regression, classification and ranking to the models that performed best on each task. The final workflow uses a residual neural network with target-gene embeddings for gene-effect regression, Elastic Net for strong-dependency classification, and a validation-selected consensus for within-cancer ranking.

| Project scope | Final design |
|---|---|
| Data | 1,066 DepMap cancer cell lines and 2,308 target genes |
| Inputs | RNA expression, damaging mutations, CNV and lineage |
| Outputs | Predicted gene effect, dependency class and ranked genes |
| Biological separation | Common-essential controls vs selective therapeutic hypotheses |
| External check | Independent Sanger CRISPR screen: 31 cell lines and 2,145 genes |

Held-out performance:

| Task | Model | Result |
|---|---|---:|
| Continuous gene-effect regression | Residual target-embedding network | MAE 0.176; median target Spearman 0.245 |
| Strong-dependency classification | Elastic Net | Median target AUPRC 0.439 |
| Per-cancer gene ranking | Residual/Elastic consensus | Precision@10 0.965; NDCG@10 0.970 |
| Selective non-common ranking | Residual/Elastic consensus | Precision@10 0.741 vs 0.494 baseline |
| External Sanger validation | Residual/Elastic consensus | AUPRC 0.490; NDCG@10 0.791 |

The repository includes the complete V1–V3 results, figures, saved artifacts and a command-line prediction workflow. A user with the required molecular profiles can obtain gene-effect predictions, dependency classifications, the top five common-essential genes and the top five possible therapeutic targets in both the terminal and saved CSV files.

**Important interpretation:** a predicted dependency is a preclinical hypothesis, not evidence that a drug will be safe or effective in patients. Normal-tissue essentiality, tractability and experimental validation still need to be considered.

[Read the results](https://github.com/Zyrok12/OncoVulnerability/tree/main/results) · [Try the model](https://github.com/Zyrok12/OncoVulnerability#how-to-try-the-model-with-your-own-data)

---

## Other selected projects

### [Panel Bias Auditor Lite](https://github.com/Zyrok12/Panel-Bias-Auditor)

A dependency-light Python command-line tool for asking whether a genomic panel covers the biology it is meant to measure—and whether nominally covered regions may still be technically difficult to call.

The tool reads BED tracks and optional VCF files to measure critical-region coverage and overlap with risks such as low mappability, GC extremes, repeats, homologous or pseudogene-like regions and reference-bias tracks. It can also derive GC-extreme, homopolymer and low-complexity tracks directly from FASTA sequence.

Beyond reporting coverage, the research workflow tests whether risk regions are enriched among assay failures or low-callability benchmark regions. Results are written as readable Markdown/HTML reports and machine-readable JSON/TSV files. The repository includes demo data, unit tests and commands for comparing multiple panels.

### [TCGA-BRCA RNA-seq analysis](https://github.com/Zyrok12/tcga-brca-differential-expression)

A reproducible R/Bioconductor workflow that follows TCGA breast-cancer RNA-seq data from retrieval to biological interpretation.

The analysis downloads STAR count data from the Genomic Data Commons with TCGAbiolinks and compares primary tumors with solid-tissue normal samples using DESeq2. It then visualizes significant genes with a volcano plot and heatmap, tests ERBB2 expression groups with Kaplan–Meier and Cox survival analyses, and performs Gene Ontology Biological Process enrichment using the complete tested gene set as the background universe.

The project also uses cross-validated LASSO logistic regression to distinguish tumor from normal samples and identify the expression features retained by the model. It is deliberately presented as an exploratory learning project: the repository documents the absence of an external cohort, possible batch effects and the limits of drawing clinical conclusions from this analysis.

### [CardI-HACK clinical genomics challenge](https://github.com/georgyzaouk/Cardi-HACK-data-challenge-group6)

A three-person team project using clinical and genetic variables to predict two cardiovascular outcomes: major adverse cardiovascular events (MACE) and disease severity.

The workflow includes exploratory analysis, missing-data review, encoding and scaling, SNP clustering to reduce redundant genetic features, construction of a polygenic-risk feature for MACE, separate outcome models, local validation and generation of the final challenge submission. I contributed to the exploratory analysis and modeling work, including iterations of the logistic-regression analysis, as well as the final scientific presentation.

Although this project is outside oncology, it gave me experience working with patient-level clinical and genetic variables, preventing data leakage and communicating a team analysis under a data-challenge deadline.

### [Deep-learning framework from scratch](https://github.com/Zyrok12/2526-m1geniomhe-group-7-main)

An educational three-person project implementing the central pieces of a neural network library in Python and NumPy. The framework contains a tensor-based automatic-differentiation engine, computation graphs, trainable parameters, linear layers, module registration, mean-squared-error loss, stochastic gradient descent with optional momentum, data loaders and common preprocessing tools.

Runnable examples train small networks on synthetic data, Iris and MNIST, while TCGA examples retrieve and encode cancer metadata from the GDC API. This is not intended to replace PyTorch; its purpose is to make forward propagation, backpropagation, gradient flow and parameter updates explicit.

---

## Research and publication

- **Co-author publication:** **Young de Castro B.**, Parsons R.F. and van der Vaart A. [Register-Shifted Structures in Uracil:Adenine and Uracil:Guanine Base-Paired DNA](https://doi.org/10.1021/acs.biochem.5c00796), *Biochemistry* (2025).

- **Ongoing research:** second-author manuscript in preparation with the Uddin Genomics Lab on an epigenome-wide association study of glucocorticoid-pathway methylation in post-traumatic stress disorder.

## Currently working on

Extending the PGX platform with star-allele and haplotype calling validated against CDC GeT-RM consensus samples, and a deep-learning model that predicts function and dosing guidance for *novel* pharmacogene variants — the known ones only need a CPIC lookup. Longer term, moving the platform toward multi-omics, starting with transcriptomics.

## Technical toolkit

- **Programming:** Python, R, Bash and C/C++
- **Machine learning:** scikit-learn, PyTorch, regularized regression, tree-based models, neural networks, probability calibration, survival analysis, model evaluation and interpretation
- **Genomics and transcriptomics:** RNA-seq, differential expression, TCGA/GDC, DepMap, VEP, GATK, DeepVariant, CNV ensemble calling, PGx resources (PharmGKB, CPIC, PharmVar, DPWG), EWAS/GWAS and PLINK2
- **Reproducibility:** Linux/WSL, Git, Conda, Docker/Apptainer, HPC workflows, tests, versioned inputs, run manifests and machine-readable outputs

## Contact

- [LinkedIn](https://www.linkedin.com/in/brunoyoungdecastro/)
- [ORCID](https://orcid.org/0009-0001-5757-2056)
- [GitHub](https://github.com/Zyrok12)
- [brunoyc@icloud.com](mailto:brunoyc@icloud.com)
