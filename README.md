# Bruno Young de Castro

**Cancer genomics · Machine learning · Translational bioinformatics**

I am an MSc candidate in **Genomics, Informatics, Mathematics and AI for Health (GENIOMHE)** at Université Paris-Saclay, with a BSc in Cell and Molecular Biology from the University of South Florida.

I am interested in a simple question: how can genomic and transcriptomic data be turned into useful, testable hypotheses about disease? My projects combine biology, statistics and machine learning, with a particular interest in cancer dependency, RNA expression and precision medicine.

I am currently looking for a **six-month internship in computational oncology, genomics or precision medicine**.

[LinkedIn](https://www.linkedin.com/in/brunoyoungdecastro/) · [ORCID](https://orcid.org/0009-0001-5757-2056) · [Email](mailto:brunoyc@icloud.com)

## Flagship project

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

## Other selected projects

### [Panel Bias Auditor Lite](https://github.com/Zyrok12/Panel-Bias-Auditor)

A dependency-light Python command-line tool for asking whether a genomic panel covers the biology it is meant to measure—and whether nominally covered regions may still be technically difficult to call.

The tool reads BED tracks and optional VCF files to measure critical-region coverage and overlap with risks such as low mappability, GC extremes, repeats, homologous or pseudogene-like regions and reference-bias tracks. It can also derive GC-extreme, homopolymer and low-complexity tracks directly from FASTA sequence.

Beyond reporting coverage, the research workflow tests whether risk regions are enriched among assay failures or low-callability benchmark regions. Results are written as readable Markdown/HTML reports and machine-readable JSON/TSV files. The repository includes demo data, unit tests and commands for comparing multiple panels.

**What this project demonstrates:** practical genomics file handling, assay design reasoning, statistical enrichment, command-line software design and reproducible reporting.

### [TCGA-BRCA RNA-seq analysis](https://github.com/Zyrok12/tcga-brca-differential-expression)

A reproducible R/Bioconductor workflow that follows TCGA breast-cancer RNA-seq data from retrieval to biological interpretation.

The analysis downloads STAR count data from the Genomic Data Commons with TCGAbiolinks and compares primary tumors with solid-tissue normal samples using DESeq2. It then visualizes significant genes with a volcano plot and heatmap, tests ERBB2 expression groups with Kaplan–Meier and Cox survival analyses, and performs Gene Ontology Biological Process enrichment using the complete tested gene set as the background universe.

The project also uses cross-validated LASSO logistic regression to distinguish tumor from normal samples and identify the expression features retained by the model. It is deliberately presented as an exploratory learning project: the repository documents the absence of an external cohort, possible batch effects and the limits of drawing clinical conclusions from this analysis.

**What this project demonstrates:** RNA-seq quantification workflows, differential expression, cancer biology, survival analysis, regularized classification and pathway enrichment.

### [CardI-HACK clinical genomics challenge](https://github.com/georgyzaouk/Cardi-HACK-data-challenge-group6)

A three-person team project using clinical and genetic variables to predict two cardiovascular outcomes: major adverse cardiovascular events (MACE) and disease severity.

The workflow includes exploratory analysis, missing-data review, encoding and scaling, SNP clustering to reduce redundant genetic features, construction of a polygenic-risk feature for MACE, separate outcome models, local validation and generation of the final challenge submission. I contributed to the exploratory analysis and modeling work, including iterations of the logistic-regression analysis, as well as the final scientific presentation.

Although this project is outside oncology, it gave me experience working with patient-level clinical and genetic variables, preventing data leakage and communicating a team analysis under a data-challenge deadline.

**What this project demonstrates:** multimodal clinical-genetic modeling, polygenic-risk features, classification, team collaboration and scientific communication.

### [Deep-learning framework from scratch](https://github.com/Zyrok12/2526-m1geniomhe-group-7-main)

An educational three-person project implementing the central pieces of a neural network library in Python and NumPy. The framework contains a tensor-based automatic-differentiation engine, computation graphs, trainable parameters, linear layers, module registration, mean-squared-error loss, stochastic gradient descent with optional momentum, data loaders and common preprocessing tools.

Runnable examples train small networks on synthetic data, Iris and MNIST, while TCGA examples retrieve and encode cancer metadata from the GDC API. This is not intended to replace PyTorch; its purpose is to make forward propagation, backpropagation, gradient flow and parameter updates explicit.

**What this project demonstrates:** understanding of neural-network internals, object-oriented Python, numerical programming and training-loop design.

## Current private research software

### PGX Pipeline — WES pharmacogenomics platform

I am also developing a private, research-use workflow that accepts FASTQ, BAM/CRAM or VCF inputs and produces annotated variant, CNV, pharmacogenomic and cohort-analysis outputs. The platform combines VEP annotation with resources including PharmGKB, CPIC, PharmVar, DPWG, ClinVar and gnomAD; adds star-allele, diplotype and phenotype interpretation layers; and records versioned manifests for reproducibility.

Current validation work uses GIAB HG002, CDC GeT-RM pharmacogenomic consensus samples and planted-truth synthetic cohorts. The repository remains private because it is an active research platform. It is not a diagnostic device.

## Research and publication

- **First-author publication:** **Young de Castro B.**, Parsons R.F. and van der Vaart A. [Register-Shifted Structures in Uracil:Adenine and Uracil:Guanine Base-Paired DNA](https://doi.org/10.1021/acs.biochem.5c00796), *Biochemistry* (2025).

- **Ongoing research:** second-author manuscript in preparation with the Uddin Genomics Lab on an epigenome-wide association study of glucocorticoid-pathway methylation in post-traumatic stress disorder.

## Technical toolkit

- **Programming:** Python, R, Bash and C/C++
- **Machine learning:** scikit-learn, PyTorch, regularized regression, tree-based models, neural networks, survival analysis, model evaluation and interpretation
- **Genomics and transcriptomics:** RNA-seq, differential expression, TCGA/GDC, DepMap, VEP, GATK, CNV analysis, PGx resources, EWAS/GWAS and PLINK2
- **Reproducibility:** Linux/WSL, Git, Conda, Docker/Apptainer, HPC workflows, tests, versioned inputs and machine-readable outputs

## How I approach research software

- Start with a clear biological question and simple baselines.
- Use held-out and external data when they are available.
- Separate technical confidence from biological or clinical interpretation.
- Report limitations alongside positive results.
- Keep analyses reproducible enough that another researcher can inspect and run them.

## Contact

I am happy to discuss internships, computational biology projects or research collaborations.

- [LinkedIn](https://www.linkedin.com/in/brunoyoungdecastro/)
- [ORCID](https://orcid.org/0009-0001-5757-2056)
- [GitHub](https://github.com/Zyrok12)
- [brunoyc@icloud.com](mailto:brunoyc@icloud.com)
