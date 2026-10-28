# OmiCairn neurodegeneration campaign: hypotheses and outcomes

This page lists every hypothesis formally nominated in the 57-run neurodegeneration campaign of OmiCairn, an autonomous multi-agent analysis system, together with the final verdict for each one and a link to the final report of the run. The machine-readable version is [`data/hypotheses.csv`](data/hypotheses.csv), one row per hypothesis; run-level information is in [`data/runs.csv`](data/runs.csv).

## What counts as a hypothesis

- **Pre-registered** (`origin = plan`): a testable statement written in the run's planning stage, before any analysis. Each one has an explicit decision rule (threshold, test and direction). Sub-hypotheses with their own decision rule (for example H1a and H1b) are listed separately.
- **On the fly** (`origin = on_the_fly`, IDs `OTF1`, `OTF2`, ...): a genuinely new hypothesis the run proposed during execution and recorded in its knowledge graph. OTF IDs are numbered within each run.

33 of the 57 runs reached planning and nominated 179 hypotheses in total (160 pre-registered, 19 on the fly). The other 24 runs stopped before planning, so they have no hypotheses; their status is recorded in `data/runs.csv`.

## How verdicts were assigned

Verdicts were assigned by **AI adjudication agents, not by human expert review**. For each hypothesis, an agent read the latest artefacts of the run (results, analysis notes, knowledge-graph updates, the written report and any review or claim-audit notes). It then applied the run's own pre-registered decision rule. A later execution stage overrides an earlier one. Each verdict is backed by a short verbatim quote from the run outputs (`evidence_quote`, with its stage-relative source file in `evidence_source`), and the agent recorded the reasoning in `adjudication_note`.

The adjudication was deliberately conservative. Wherever the data did not meet the rule, the verdict follows the data, even when the run's own label or the written report claimed support. Proxy or surrogate analyses do not count as tests of the pre-registered hypothesis. In about 15 cases the verdict is stricter than the run's own label; `adjudication_note` explains each one and names a defensible alternative reading where there is one. The run outputs cited in `evidence_source` are not included in this repository.

### Outcome classes

| Verdict | Outcome class | Meaning |
|---|---|---|
| Supported | positive | Tested. The pre-registered decision rule was met. |
| Partially supported | positive (partial) | Tested. Some components of the decision rule were met, but not all (for example, the direction was right but a replication arm failed). |
| Not supported | negative | Tested. The decision rule was not met: a null result (CI includes the null or FDR fails), a refutation or an opposite effect. Includes powered negatives. |
| Inconclusive | inconclusive | Tested, but underpowered, ambiguous or confounded, so the data cannot settle it. |
| Not testable (data) | not tested | Not tested, or tested only through a proxy, because a suitable dataset, modality, sample size or metadata was unavailable, access-restricted or unsuitable. |
| Not tested (run did not execute) | not tested | Not tested for a reason unrelated to data: the run halted before execution, a technical failure, a time or compute limit, or a follow-up that was proposed but never run. These are excluded from the summary denominators below. |

## Summary

This table reproduces the manuscript's Supplementary Data table of hypothesis outcomes. It covers the 27 runs that tested at least one hypothesis and their 136 hypotheses. The 43 hypotheses marked *Not tested (run did not execute)* are excluded; 30 of them come from 6 runs that never executed any test. Percentages are row-wise and rounded.

| Subset | Runs | Hypotheses | Supported | Partially supported | Not supported | Inconclusive | Not testable (data) |
|---|--:|--:|--:|--:|--:|--:|--:|
| All executed runs | 27 | 136 | 15 (11%) | 7 (5%) | 45 (33%) | 31 (23%) | 38 (28%) |
| &nbsp;&nbsp;PD | 22 | 109 | 14 (13%) | 4 (4%) | 33 (30%) | 28 (26%) | 30 (28%) |
| &nbsp;&nbsp;AD | 4 | 21 | 1 (5%) | 0 (0%) | 10 (48%) | 2 (10%) | 8 (38%) |
| &nbsp;&nbsp;Cross-disease | 1 | 6 | 0 (0%) | 3 (50%) | 2 (33%) | 1 (17%) | 0 (0%) |
| &nbsp;&nbsp;Pre-registered (plan) only | 27 | 125 | 14 (11%) | 7 (6%) | 44 (35%) | 29 (23%) | 31 (25%) |
| &nbsp;&nbsp;Runs that reached review | 17 | 87 | 9 (10%) | 6 (7%) | 26 (30%) | 19 (22%) | 27 (31%) |
| &nbsp;&nbsp;Latest run per topic | 22 | 112 | 12 (11%) | 6 (5%) | 40 (36%) | 22 (20%) | 32 (29%) |

All counts were recomputed from `data/hypotheses.csv` and match the supplementary table exactly. Subset definitions:
- *Latest run per topic*: the most recent executed run for each topic (the highest `-rN` among executed runs), where the topic is the run name without its `-rN` suffix.
- *Runs that reached review*: the executed runs whose pipeline reached a peer-review stage. These 17 runs are: `alzheimer-apoe4-microglia-ldam-r1`, `alzheimer-ligrec-braak-breakdown-r1`, `alzheimer-rorb-ec-vulnerability-r1`, `ideate-parkinson-mechanism-r2`, `neurodeg-microglia-convergence-r1`, `parkinson-asyn-propagation-r2`, `parkinson-cellchat-immune-axis-r3`, `parkinson-celloracle-ko-r1`, `parkinson-foundation-embedding-r4`, `parkinson-lamda-multiregion-r3`, `parkinson-lincs-reversal-r4`, `parkinson-metabolic-flux-sn-r1`, `parkinson-multimodal-ppmi-trajectory-r1`, `parkinson-multimodal-spatial-proteomics-r3`, `parkinson-prs-portability-r3`, `parkinson-scenic-regulons-r1`, `pd-vatpase-lysosomal-compensation-r1`.

Taken together, 83 of the 136 tested-or-attempted hypotheses (61%) were either not supported or not testable with the available data. Even if every partially supported and inconclusive hypothesis were counted as supported, support would be at most 53/136 (39%). 11 of the 33 planned runs had at least one fully supported hypothesis.

## Positive findings (22: 15 supported, 7 partially supported)

Hypothesis texts are the condensed statements recorded during adjudication. Several of these verdicts carry caveats: a negative control or specificity check that holds only because the primary hypothesis failed, a rule met at n = 2 + 2, a proxy method, or a run that was later superseded. Read the `adjudication_note` for the row in `data/hypotheses.csv` before relying on any verdict.

| Run | Disease | ID | Hypothesis | Verdict | Report |
|---|---|---|---|---|---|
| `alzheimer-gwas-snatac-celltype-r1` | AD | OTF1 | Proportion of microglia-dominant loci exceeds the mean proportion for non-microglial cell types. | Supported | [report](reports/alzheimer-gwas-snatac-celltype-r1/report.md) |
| `neurodeg-microglia-convergence-r1` | Cross-disease | H1 | Microglial LDAM module (LGALS3, CD9, GPNMB, NPC2) significantly elevated in EACH of AD, DLB and PDD vs NCI in GSE303823 (shared cross-dementia feature). | Partially supported | [report](reports/neurodeg-microglia-convergence-r1/report.md) |
| `neurodeg-microglia-convergence-r1` | Cross-disease | H2 | H1 call reproduced by two orthogonal methods: (a) Leiden LDAM-like subcluster compositional shift (scCODA); (b) AUCell per-donor scores. | Partially supported | [report](reports/neurodeg-microglia-convergence-r1/report.md) |
| `neurodeg-microglia-convergence-r1` | Cross-disease | H6 | Sensitivity decomposition: H1 effect not driven by microglial proportion, survives covariates (PMI/age/sex), marker-set and resolution perturbation. | Partially supported | [report](reports/neurodeg-microglia-convergence-r1/report.md) |
| `parkinson-asyn-propagation-r1` | PD | H1 | SNCA-weighted SIR (model B) recovers Braak rank order of t_peak across 5 regions (Spearman rho>=0.70, bootstrap CI lower bound >0). | Supported | no final report (superseded or halted run) |
| `parkinson-asyn-propagation-r1` | PD | H4 | Ablating DMNX->GPi edge shifts predicted rank of at least one region by >1 position. | Supported | no final report (superseded or halted run) |
| `parkinson-cellchat-immune-axis-r3` | PD | H1 | >=5 L-R pairs PD-up in both PBMC CD8+T->monocyte (GSE223138) and brain CD8+T->microglia (Ma 2025 SN; fallback Fullard), permutation p<0.01 | Supported | [report](reports/parkinson-cellchat-immune-axis-r3.pdf) |
| `parkinson-cellchat-immune-axis-r3` | PD | H4 | Reverse direction (monocyte->CD8+T, microglia->CD8+T) does NOT reach H1 threshold (<5 pairs, perm p>=0.05): direction-specificity | Supported | [report](reports/parkinson-cellchat-immune-axis-r3.pdf) |
| `parkinson-celloracle-ko-r1` | PD | H3 | LRRK2-KO top-100 predicted targets enriched for Hemedan 2024 prodromal module (BH q<0.05) | Supported | [report](reports/parkinson-celloracle-ko-r1.pdf) |
| `parkinson-celloracle-ko-r1` | PD | H4a | SNCA-KO predicts protective shift: cosine with PD-vs-ctrl vector >0, permutation p<0.05 | Supported | [report](reports/parkinson-celloracle-ko-r1.pdf) |
| `parkinson-celloracle-ko-r1` | PD | H4b | HBB-KO negative control predicts null shift (\|cosine\|<0.1) | Supported | [report](reports/parkinson-celloracle-ko-r1.pdf) |
| `parkinson-gut-brain-axis-r2` | PD | H3 | DMNX microglia upregulate TLR4/TLR2/CD14/NLRP3 module (FDR<0.05) AND correlate with Wallen LPS-producer abundance AND DMNX effect > SNpc, V1 | Partially supported | no final report (superseded or halted run) |
| `parkinson-gut-brain-axis-r2` | PD | H5 | Negative-control modules (catecholamine, ferroptosis, cuproptosis) do NOT show H1-level alignment (<15 modules, p>=0.01) | Supported | no final report (superseded or halted run) |
| `parkinson-gut-brain-axis-r4` | PD | H5 | Negative-control modules (catecholamine, ferroptosis, cuproptosis) show no significant alignment (all hypergeometric p>=0.05) | Supported | [report](reports/parkinson-gut-brain-axis-r4.pdf) |
| `parkinson-lamda-multiregion-r3` | PD | H3 | LAMDA higher in EN vs IN in >=2/3 cortical regions AND in >=1 subcortical projection-neuron type (DMNX_Neu/GPI_Neu) vs background. | Partially supported | [report](reports/parkinson-lamda-multiregion-r3.pdf) |
| `parkinson-lincs-reversal-r4` | PD | H3 | DMNX_Neu and Micro_PVM connectivity rankings poorly correlated (Pearson r<0.3 AND CI upper <0.3). | Supported | [report](reports/parkinson-lincs-reversal-r4.pdf) |
| `parkinson-multimodal-ppmi-trajectory-r1` | PD | H5 | Descriptive audit of machine-readability of 6 cited PPMI supplements (>=4/6 strong, 2-3/6 partial, <=1/6 negative). | Partially supported | [report](reports/parkinson-multimodal-ppmi-trajectory-r1.pdf) |
| `parkinson-prs-portability-r3` | PD | H2 | EAS/EUR analytical AUC ratio within ±0.10 of Saffie-Awad ratio 0.931 | Supported | [report](reports/parkinson-prs-portability-r3.pdf) |
| `parkinson-scenic-regulons-r1` | PD | H5 | H1 replication count varies by <=1 across Leiden gamma 0.4/0.8/1.2 | Supported | [report](reports/parkinson-scenic-regulons-r1.pdf) |
| `parkinson-tcell-foothold-r3` | PD | H5 | Negative control: exhaustion module fails to replicate (log2FC<=0 or FDR>=0.1) in >=3 atlases | Supported | [report](reports/parkinson-tcell-foothold-r3.pdf) |
| `pd-vatpase-lysosomal-compensation-r1` | PD | H1 | V-ATPase CLEAR module UP (mean log2FC>0, >=6 subunits up, perm p at floor) in LRRK2 G2019S isogenic iPSC-DA, GSE167335 | Supported | [report](reports/pd-vatpase-lysosomal-compensation-r1/report.md) |
| `pd-vatpase-lysosomal-compensation-r1` | PD | H5 | Sensitivity/power decomposition: replication verdict robust to gene-set and normalisation choices; cohort power adequacy | Partially supported | [report](reports/pd-vatpase-lysosomal-compensation-r1/report.md) |

## Negative findings (45 not supported)

These hypotheses were tested and the pre-registered decision rule was not met. Some are powered negatives; others are underpowered nulls, and `adjudication_note` says which.

| Run | Disease | ID | Hypothesis | Verdict | Report |
|---|---|---|---|---|---|
| `alzheimer-apoe4-microglia-ldam-r1` | AD | H1 | APOE4/4 vs APOE3/3 microglial pseudobulk: >=2/4 LDAM markers up AND >=2/3 DAM2 markers down (FDR<0.05) at matched Braak (SEA-AD primary, Morabito replication). | Not supported | [report](reports/alzheimer-apoe4-microglia-ldam-r1.pdf) |
| `alzheimer-apoe4-microglia-ldam-r1` | AD | H2 | Per-donor LDAM/DAM ratio positively associated with tau (Braak) after adjusting for amyloid; beta_tau>0, p<0.05, 95% CI excludes 0. | Not supported | [report](reports/alzheimer-apoe4-microglia-ldam-r1.pdf) |
| `alzheimer-gwas-snatac-celltype-r1` | AD | H1 | Of top-75 AD GWAS loci, microglia-dominant snATAC fraction exceeds p0=0.25 (>=25 loci, binomial) AND SPI1 motif accessibility is the top predictor of microglial dominance. | Not supported | [report](reports/alzheimer-gwas-snatac-celltype-r1/report.md) |
| `alzheimer-gwas-snatac-celltype-r1` | AD | H2 | Microglial GWAS-overlapping peak accessibility peaks at DAM/mid-disease stage vs both homeostatic and late stages (both contrasts p<0.05, CI excl. 0). | Not supported | [report](reports/alzheimer-gwas-snatac-celltype-r1/report.md) |
| `alzheimer-gwas-snatac-celltype-r1` | AD | H3 | Exploratory: secondary compartment of GWAS loci in excitatory-neuron peaks; rank order microglia > excitatory neurons > oligodendrocytes ~ astrocytes. | Not supported | [report](reports/alzheimer-gwas-snatac-celltype-r1/report.md) |
| `alzheimer-ligrec-braak-breakdown-r1` | AD | H1 | C1Q-C3-CR3, SPP1 and CXCL10-CXCR3 are among the top-10 disrupted L-R axes in AD PFC, each with positive monotone Braak slope (p<0.05, CI excl. 0). | Not supported | [report](reports/alzheimer-ligrec-braak-breakdown-r1.pdf) |
| `alzheimer-rorb-ec-vulnerability-r1` | AD | H1 | RORB+ vs RORB- EC excitatory neurons: CACNA1C or CACNA1D up AND CALB1 or PVALB down (BH-FDR<0.05), sign reproduced in second atlas. | Not supported | [report](reports/alzheimer-rorb-ec-vulnerability-r1.pdf) |
| `alzheimer-rorb-ec-vulnerability-r1` | AD | H2 | ISR module score in RORB+ EC neurons increases with Braak stage (slope>0, p<0.05, CI excl. 0), preceding RORB+ loss. | Not supported | [report](reports/alzheimer-rorb-ec-vulnerability-r1.pdf) |
| `alzheimer-rorb-ec-vulnerability-r1` | AD | H4 | Exploratory: RORB+ EC excitatory subcluster recoverable at Leiden 0.6-1.2 in both GSE138852 and GSE147528 with >80% consistent assignment. | Not supported | [report](reports/alzheimer-rorb-ec-vulnerability-r1.pdf) |
| `alzheimer-rorb-ec-vulnerability-r1` | AD | OTF2 | Re-analysis restricted to GSE147528 (2,009 RORB+ cells) will have power for H1; test whether CACNA1C/D reach FDR<0.05 there. | Not supported | [report](reports/alzheimer-rorb-ec-vulnerability-r1.pdf) |
| `neurodeg-microglia-convergence-r1` | Cross-disease | H3 | LDAM signature locked on GSE303823 transfers without refitting to held-out SEA-AD DLPFC and separates high vs low Braak donors (AUC CI lower bound >0.5). | Not supported | [report](reports/neurodeg-microglia-convergence-r1/report.md) |
| `neurodeg-microglia-convergence-r1` | Cross-disease | H4 | LGALS3/GPNMB lipid-droplet sub-program enriched in APOE4 carriers in GSE303823 (replicating SEA-AD JT p=0.006), with SEA-AD MTG replication. | Not supported | [report](reports/neurodeg-microglia-convergence-r1/report.md) |
| `parkinson-asyn-propagation-r1` | PD | H2 | Removing SNCA weighting (model A) degrades rho by >=0.30 vs model B (paired bootstrap CI excl. 0). | Not supported | no final report (superseded or halted run) |
| `parkinson-asyn-propagation-r2` | PD | H1 | SNCA-weighted SIR (model B) recovers proxy Braak rank order [1,3,5,5,6] of t_peak across 5 regions (rho>=0.7, bootstrap CI lower bound >0). | Not supported | [report](reports/parkinson-asyn-propagation-r2.pdf) |
| `parkinson-asyn-propagation-r2` | PD | H2 | Removing SNCA weighting (model A, connectome-only) degrades rho by >=0.3 relative to model B. | Not supported | [report](reports/parkinson-asyn-propagation-r2.pdf) |
| `parkinson-asyn-propagation-r2` | PD | H4 | Ablating DMNX->GPi edge shifts peak-time rank by >1 position for >=1 region. | Not supported | [report](reports/parkinson-asyn-propagation-r2.pdf) |
| `parkinson-asyn-propagation-r2` | PD | H5 | Model-family comparison: connectome-only (A), SNCA-weighted (B, primary), cell-autonomous (C) ranked by Braak rho; A or C beating B reported as-is. | Not supported | [report](reports/parkinson-asyn-propagation-r2.pdf) |
| `parkinson-cellchat-immune-axis-r3` | PD | H2 | Ligands/receptors of shared pairs enriched (q<0.05) among 28 Hong 2025 MR-implicated immune genes | Not supported | [report](reports/parkinson-cellchat-immune-axis-r3.pdf) |
| `parkinson-celloracle-ko-r1` | PD | H1 | Mean cosine between in-silico KO shift (10 GWAS genes) and PD-minus-control DA shift >0.30 with permutation p<0.01 | Not supported | [report](reports/parkinson-celloracle-ko-r1.pdf) |
| `parkinson-celloracle-ko-r1` | PD | H2 | Per-gene KO alignment correlates with fine-mapping PIP (Spearman rho>0.4, p<0.05; n=10) | Not supported | [report](reports/parkinson-celloracle-ko-r1.pdf) |
| `parkinson-da-vulnerability-r5` | PD | H3 | Locked consensus AGTR1+ panel classifies Martirosyan 2024 PD vs ctrl donors with AUC>=0.75, CI lower >0.5 | Not supported | [report](reports/parkinson-da-vulnerability-r5.pdf) |
| `parkinson-da-vulnerability-r5` | PD | H5 | Decomposition of DA loss: AGTR1+-within-DA fraction (component c) is the dominant driver vs total nuclei/DA fraction | Not supported | [report](reports/parkinson-da-vulnerability-r5.pdf) |
| `parkinson-foundation-embedding-r4` | PD | H1 | Geneformer-V2 or scGPT donor-level LOO AUC>0.75 AND dAUC>=0.05 over log-CPM-PCA-LR with DeLong p<0.05 (Fullard multi-region) | Not supported | [report](reports/parkinson-foundation-embedding-r4/report.md) |
| `parkinson-gut-brain-axis-r2` | PD | H1 | >=15 KEGG modules shared between Wallen 2022 top-100 PD-enriched MetaCyc pathways and Fullard DMNX top-100 enriched modules, hypergeometric p<0.01 | Not supported | no final report (superseded or halted run) |
| `parkinson-gut-brain-axis-r2` | PD | H2 | 7-gene vagal-afferent module DE in DMNX (FDR<0.05) AND anti-correlated with SCFA-producer depletion (rho<-0.3, perm p<0.05) | Not supported | no final report (superseded or halted run) |
| `parkinson-gut-brain-axis-r2` | PD | H4 | Storm 2025 MR-causal PD proteins (fallback: Hallqvist 2024 panel) over-represented in Wallen PD-enriched bacterial pathways (perm p<0.05) | Not supported | no final report (superseded or halted run) |
| `parkinson-gut-brain-axis-r4` | PD | H1 | >=15 bridging KEGG modules shared between Wallen 2022 top-100 MetaCyc pathways and Fullard DMNX top-100 enriched modules (131-module catalogue), hypergeometric p<0.01 | Not supported | [report](reports/parkinson-gut-brain-axis-r4.pdf) |
| `parkinson-gut-brain-axis-r4` | PD | H2 | 7-gene vagal-afferent module DE in DMNX pseudobulk (FDR<0.05) AND anti-correlated with Wallen SCFA-producer abundance (rho<-0.3, perm p<0.05) | Not supported | [report](reports/parkinson-gut-brain-axis-r4.pdf) |
| `parkinson-gut-brain-axis-r4` | PD | H3 | DMNX Micro_PVM TLR/LPS-response module up in PD (FDR<0.05) AND correlates with Wallen LPS-producer abundance | Not supported | [report](reports/parkinson-gut-brain-axis-r4.pdf) |
| `parkinson-gut-brain-axis-r4` | PD | H4 | Hallqvist 2024 plasma proteins (pre-registered fallback for Storm 2025 MR) over-represented in Wallen PD-enriched pathway modules (perm p<0.05) | Not supported | [report](reports/parkinson-gut-brain-axis-r4.pdf) |
| `parkinson-lamda-multiregion-r3` | PD | H1 | LAMDA module generalises to non-cortical regions: >=3 non-cortical region x cell-type pairs with PD>ctrl at FDR<0.05 and Cohen's d>0.25 (Fullard atlas). | Not supported | [report](reports/parkinson-lamda-multiregion-r3.pdf) |
| `parkinson-lamda-multiregion-r3` | PD | H2 | LAMDA enrichment in PD follows a Braak-stage regional gradient (region-ordered Spearman, permutation p<0.05). | Not supported | [report](reports/parkinson-lamda-multiregion-r3.pdf) |
| `parkinson-lamda-multiregion-r3` | PD | H4 | LAMDA sub-programs (synaptic, mito, proteostasis, vesicle, immune) show cortical vs subcortical dissociation. | Not supported | [report](reports/parkinson-lamda-multiregion-r3.pdf) |
| `parkinson-lincs-reversal-r4` | PD | H4 | Neuronal-cell-line subset top-50 has >=8 PD-evidence compounds and Fisher p<0.05 vs all-lines k1. | Not supported | [report](reports/parkinson-lincs-reversal-r4.pdf) |
| `parkinson-lincs-reversal-r4` | PD | H5 | Sanity gate: ropinirole and pramipexole both above median connectivity (mimicking tail), not reversers. | Not supported | [report](reports/parkinson-lincs-reversal-r4.pdf) |
| `parkinson-metabolic-flux-sn-r1` | PD | H2 | Top-10 TIMBR-predicted biomarker metabolites include >=4 replicated in Shao/Luo 2024 meta-analysis (hypergeometric q<0.05). | Not supported | [report](reports/parkinson-metabolic-flux-sn-r1.pdf) |
| `parkinson-multimodal-ppmi-trajectory-r1` | PD | H4 | No single modality contributes >=70% of loading on the 1-D latent (multi-modal claim). | Not supported | [report](reports/parkinson-multimodal-ppmi-trajectory-r1.pdf) |
| `parkinson-plasma-prodromal-panel-r3` | PD | H4 | HR directions of 6 overlapping panel proteins match between Hällqvist (LC-MS) and Gan 2025 UKB Olink (>=4/6). | Not supported | [report](reports/parkinson-plasma-prodromal-panel-r3/report.md) |
| `parkinson-plasma-prodromal-panel-r4` | PD | H4 | HR directions of 6 UKB-Olink-overlapping proteins concordant between Hällqvist iRBD conversion and Gan 2025 UKB incident PD (>=4/6, p<0.05). | Not supported | [report](reports/parkinson-plasma-prodromal-panel-r4.pdf) |
| `parkinson-plasma-prodromal-panel-r4` | PD | H5 | At least one functional sub-panel achieves 5-fold CV AUC >0.75 (failure if all <=0.60). | Not supported | [report](reports/parkinson-plasma-prodromal-panel-r4.pdf) |
| `parkinson-prs-portability-r3` | PD | H1 | EUR 1000G analytical PRS liability-R2 (Kim 2024, LDpred) within ±0.05 of Saffie-Awad 2025 EUR benchmark (AUC 0.621) | Not supported | [report](reports/parkinson-prs-portability-r3.pdf) |
| `parkinson-prs-portability-r3` | PD | H4 | Multi-ancestry Kim 2024 PRS not significantly outperformed by EUR-only Nalls 2019 PRS in EUR stratum | Not supported | [report](reports/parkinson-prs-portability-r3.pdf) |
| `parkinson-tcell-foothold-r3` | PD | H1 | Ma 2025 clonal CD8+ T-cell module PD-up (FDR<0.1, log2FC>0) in >=3/4 independent atlases, Δ vs shuffled-label null CI excluding 0 | Not supported | [report](reports/parkinson-tcell-foothold-r3.pdf) |
| `parkinson-tcell-foothold-r3` | PD | H2 | T-cell module follows revised region rank GPi>=M1>PFC>DMNX≈V1 in Fullard (rho>0.5, perm p<0.05) | Not supported | [report](reports/parkinson-tcell-foothold-r3.pdf) |
| `parkinson-tcell-foothold-r3` | PD | H3 | Per-donor T-cell module score correlates with AGTR1+ DA-loss (rho>0.3, perm p<0.05) in >=2/4 atlases | Not supported | [report](reports/parkinson-tcell-foothold-r3.pdf) |

## Other hypotheses by run (112: inconclusive, not testable for data, or not tested)

### `alzheimer-apoe4-microglia-ldam-r1`

AD · [report](reports/alzheimer-apoe4-microglia-ldam-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H3 | Monotonic APOE dose-response: LDAM score e3/3 < e3/4 < e4/4 and DAM2 e3/3 > e3/4 > e4/4 (Jonckheere-Terpstra, Braak-controlled). | Not testable (data) |
| OTF1 | APOE expression itself is elevated in LDAM-state microglia in SEA-AD (APOE4 autocrine feedback loop). | Not tested (run did not execute) |
| OTF2 | In e4/e4 homozygous donors (Synapse syn64410371 metadata) the LDAM/DAM2 shift is larger than in heterozygotes and the H1 rule would pass. | Not testable (data) |
| OTF3 | A linear mixed model with categorical age bins as random effects would recover a significant beta_tau for H2 in the same 84 donors. | Not tested (run did not execute) |

### `alzheimer-gwas-snatac-celltype-r1`

AD · [report](reports/alzheimer-gwas-snatac-celltype-r1/report.md)

| ID | Hypothesis | Verdict |
|---|---|---|
| OTF2 | GWAS-linked microglial circuits peak at late disease (Stage 5-6) rather than mid-disease (sustained late-inflammatory phenotype). | Not testable (data) |
| OTF3 | Fine-mapped credible sets (+/-5-50 kb) would recover more loci than lead-SNP overlap and may strengthen microglial enrichment. | Not tested (run did not execute) |

### `alzheimer-ligrec-braak-breakdown-r1`

AD · [report](reports/alzheimer-ligrec-braak-breakdown-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H2 | Genes of disrupted L-R pairs (Braak III-IV or AD-vs-control) are enriched in top-20 AD GWAS locus genes (hypergeometric p<0.05, OR CI excl. 1). | Not testable (data) |
| H3 | Exploratory: disrupted-axis intensity across EC, hippocampus, PFC tracks tau-spread order (Spearman rho>=0, p<0.05; needs SEA-AD multi-region). | Not testable (data) |
| OTF1 | LAMA2->integrin (microglia->astrocyte) disruption reflects pericellular-matrix change and tracks Braak stage as microglia shift to DAM. | Not testable (data) |
| OTF2 | JAM2->ITGB1 (endothelial->excitatory neuron) elevation reflects Braak-dependent BBB breakdown. | Not testable (data) |
| OTF3 | Reformulated H2: NicheNet downstream targets of top disrupted L-R pairs are enriched in GWAS-locus regulatory modules. | Not tested (run did not execute) |
| OTF4 | Relative ranking of ECM vs complement/SPP1 axes is real (Delta=0.662, p=0.001) but absolute disruption needs larger n (SEA-AD). | Not testable (data) |
| OTF5 | MDK->ALK (endothelial->endothelial, log2FC -1.90) is a novel AD-associated loss of vascular neuroprotective signalling. | Not tested (run did not execute) |
| OTF6 | SEMA5A->PLXNA3/PLXNA1 (microglia->astrocyte/neuron) reduction reflects axon-guidance disruption contributing to synaptic pruning deficits. | Not tested (run did not execute) |

### `alzheimer-rorb-ec-vulnerability-r1`

AD · [report](reports/alzheimer-rorb-ec-vulnerability-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H3 | Exploratory: one vulnerability program (excitability, ISR/proteostasis, mitochondrial) separates RORB+ from RORB- more strongly than others (Cohen's d, >0.3 SD). | Inconclusive |
| OTF1 | ISR module is LOWER in RORB+ than RORB- EC neurons (at all Braak stages), counter to the ISR-driven vulnerability model. | Inconclusive |
| OTF3 | Elevated excitability module in RORB+ neurons is driven by non-calcium genes (SCN1A, SCN8A, HCN1). | Not tested (run did not execute) |
| OTF4 | PVALB downregulation in RORB+ neurons (log2FC -1.18) reaches BH-FDR<0.05 under pydeseq2. | Not tested (run did not execute) |

### `ideate-parkinson-mechanism-r2`

PD · [report](reports/ideate-parkinson-mechanism-r2.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Lysosomal-convergence score log2(LRRK2)-log2(GBA1) identifies the most PD-depleted DA subtype in Kamath 2022 SN atlas (AUROC>=0.70, CI>0.5, beats random pair). | Not testable (data) |
| H2 | TFEB targets (LAMP2A, CTSD, CTSB, ATP6AP1, MCOLN1) >=4/5 down with gene-set FDR<=0.10 in BOTH GBA1-N370S and LRRK2-G2019S iPSC-DA vs isogenic controls (+synergy arm). | Not testable (data) |
| H3 | TFEB-target composite correlates with alpha-syn protein (proteomics) in iPSC-DA (Spearman r>0.40, perm p<0.05) (+ pharmacological reversal arm). | Not testable (data) |
| OTF1 | LRRK2-G2019S iPSC-DA neurons show compensatory upregulation of V-ATPase subunit genes (partially reversed by MLi-2). | Inconclusive |
| OTF2 | GBA1-N370S cells (exhausted compensation) show V-ATPase DOWNregulation, distinguishing two phases of lysosomal dysfunction. | Not testable (data) |
| OTF3 | N=2 donors/group NanoString cannot reach significance; a properly powered test needs N>=5 donors with whole-transcriptome LRRK2-G2019S iPSC-DA data. | Not testable (data) |

### `neurodeg-microglia-convergence-r1`

Cross-disease · [report](reports/neurodeg-microglia-convergence-r1/report.md)

| ID | Hypothesis | Verdict |
|---|---|---|
| H5 | Negative control: ECM-integrin (LAMA2/COL4A2->ITGAV/ITGA6/ITGB8) disruption is AD-specific (AD g<0 FDR<0.05; DLB/PDD CIs include 0). | Inconclusive |

### `parkinson-asyn-propagation-r1`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H3 | Within PFC, model predicts excitatory neurons reach infection threshold first; model top-3 overlaps >=2 with LAMDA pSyn-enriched top-3. | Inconclusive |
| H5 | Model-family comparison: rank connectome-only (A), SNCA-weighted (B, primary), cell-autonomous (C) by Braak rho. | Inconclusive |

### `parkinson-asyn-propagation-r2`

PD · [report](reports/parkinson-asyn-propagation-r2.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H3 | Within PFC (cingulate proxy) excitatory L5/6 neurons reach infection threshold first; model top-3 overlaps >=2 with LAMDA Lewy-burdened top-3 (Fisher p<0.05). | Inconclusive |

### `parkinson-cellchat-immune-axis-r1`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | >=5 L-R pairs PD-upregulated in both peripheral CD8+T->monocyte (GSE223138 PBMC) and brain CD8+T-like->CNS macrophage (Fullard 2024), permutation p<0.01. | Not tested (run did not execute) |
| H2 | Shared L-R pairs enriched for Hong 2025 28 MR-implicated immune genes (BH q<0.05, hypergeometric). | Not tested (run did not execute) |
| H3 | Per-donor peripheral CD8+T MR-gene score rank-correlates with brain T-cell module score (Spearman rho>0.3, p<0.05). | Not tested (run did not execute) |
| H4 | Direction-specificity control: reverse-direction inference yields fewer shared pairs and permutation p>=0.05. | Not tested (run did not execute) |
| H5 | Method-consensus robustness: LIANA consensus shared-pair count within +/-2 of CellPhoneDB, NATMI, scTalk counts. | Not tested (run did not execute) |

### `parkinson-cellchat-immune-axis-r3`

PD · [report](reports/parkinson-cellchat-immune-axis-r3.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H3 | Per-donor peripheral signature scores correlate with brain T-cell module scores (peripheral-foreshadow) | Not testable (data) |
| H5 | Per-method shared-pair counts (CellPhoneDB, NATMI, scTalk, CellChat, Connectome) within +/-2 of LIANA consensus | Not tested (run did not execute) |

### `parkinson-celloracle-ko-r1`

PD · [report](reports/parkinson-celloracle-ko-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H5 | H1 mean cosine changes <=0.1 between Adams-derived ATAC base-GRN and Zenodo midbrain reference base-GRN | Not tested (run did not execute) |

### `parkinson-da-vulnerability-r4`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | AGTR1+ DA fraction depleted in PD (log2FC in [-2.6,-0.95], BH-FDR<0.05) in all 3 replication atlases (Wang, Adams, Fullard SNpc) | Inconclusive |
| H2 | TP53 and NR2F2 modules upregulated in residual AGTR1+ DA cells (BH-FDR<0.05) in >=2/3 atlases | Inconclusive |
| H3 | Locked consensus AGTR1+ panel stratifies PD vs ctrl in blind Martirosyan 2024 (AUC>=0.75, CI lower >0.5) | Not tested (run did not execute) |
| H4 | H1 depletion sign and FDR pass stable across >=4/6 Leiden resolutions in each atlas where H1 holds | Inconclusive |
| H5 | Per-donor decomposition: AGTR1+ within-DA fraction (layer c) dominates signal reduction vs total nuclei / DA fraction | Inconclusive |

### `parkinson-da-vulnerability-r5`

PD · [report](reports/parkinson-da-vulnerability-r5.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Kamath AGTR1+ DA subtype recovers and is depleted in PD (log2FC in [-2.6,-0.95], BH-FDR<0.05) in Wang, Adams and Fullard SNpc | Inconclusive |
| H2 | TP53 and NR2F2 stress modules upregulated in residual AGTR1+ DA cells (BH-FDR<0.05) in >=2/3 atlases | Not testable (data) |
| H4 | H1 sign and FDR stable across >=4/6 Leiden resolutions within each atlas that passed H1 | Inconclusive |

### `parkinson-foundation-embedding-r1`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Donor-level LOO AUC: best FM (Geneformer/scGPT) beats log-CPM-PCA-LR by dAUC>=0.05 (CI>0, DeLong p<0.05) with AUC>0.75 (Wang 2024) | Not tested (run did not execute) |
| H2 | Leiden on Geneformer embeddings recovers an AGTR1-high cluster (>=1.5x, silhouette>=0.10) in Wang PD donors | Not tested (run did not execute) |
| H3 | Geneformer fine-tuned 1 epoch achieves held-out AUC>=0.7 on Adams; random-init transformer <=0.6 | Not tested (run did not execute) |
| H4 | dAUC stable within +/-0.05 across 5K/25K/50K nuclei-per-donor subsamples | Not tested (run did not execute) |
| H5 | Wang-fitted FM donor embeddings achieve zero-shot AUC>=0.65 (CI lower>=0.50) on Adams | Not tested (run did not execute) |

### `parkinson-foundation-embedding-r4`

PD · [report](reports/parkinson-foundation-embedding-r4/report.md)

| ID | Hypothesis | Verdict |
|---|---|---|
| H2 | AGTR1+ subcluster recovery in FM embeddings | Not testable (data) |
| H3 | Geneformer fine-tuned on Kamath SNpc generalises to Wang and Adams (AUC>=0.70) and beats from-scratch by >=0.10 | Not testable (data) |
| H4 | dAUC stable within +/-0.05 across 5K/25K/50K nuclei-per-donor subsamples | Not tested (run did not execute) |
| H5 | Fullard-trained FM embeddings zero-shot AUC>=0.65 with CI lower>=0.50 on BOTH Wang and Adams | Inconclusive |

### `parkinson-lamda-multiregion-r2`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | >=3 non-cortical (region x cell-type) combos show positive LAMDA enrichment in PD (BH-FDR<0.05, d>0.25) in Fullard atlas | Not tested (run did not execute) |
| H2 | LAMDA module score in PD follows Braak ordering DMNX>=SNpc>=GPi>=M1>=V1 (Spearman rho>0, perm p<0.05) | Not tested (run did not execute) |
| H3 | LAMDA higher in excitatory/projection neurons than inhibitory in >=2/5 regions (BH p<0.05, r>0.10) | Not tested (run did not execute) |
| H4 | LAMDA sub-program co-activation higher in cortex than subcortex (perm p<0.05) | Not tested (run did not execute) |
| H5 | Orbitofrontal positive control: LAMDA higher in PD/PDD/DLB vs ctrl in Goralski CosMx (p<0.001) | Not tested (run did not execute) |

### `parkinson-lamda-multiregion-r3`

PD · [report](reports/parkinson-lamda-multiregion-r3.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H5 | Positive control: LAMDA higher in pSyn+ vs pSyn- CosMx cells of held-out Goralski orbitofrontal data (Wilcoxon p<0.001). | Not testable (data) |

### `parkinson-lincs-reversal-r1`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Top-50 LINCS L1000 reversers of DMNX_Neu PD signature include >=5 compounds with prior PD-repositioning evidence (hypergeometric q<0.01). | Not tested (run did not execute) |
| H2 | >=2 of 5 pre-specified PD-relevant drug classes enriched in top-50 reversers (Fisher, BH q<0.05). | Not tested (run did not execute) |
| H3 | DMNX_Neu vs Micro_PVM connectivity rankings poorly correlated (Pearson r<0.3, CI upper <0.3). | Not tested (run did not execute) |
| H4 | Neuronal-cell-line L1000 subset top-50 has >=8 compounds with prior PD evidence, more than all-lines top-50. | Not tested (run did not execute) |
| H5 | Sanity gate: levodopa/ropinirole/pramipexole/rasagiline not in top-50 reversers. | Not tested (run did not execute) |

### `parkinson-lincs-reversal-r4`

PD · [report](reports/parkinson-lincs-reversal-r4.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | >=5 of top-50 LINCS touchstone reversers of DMNX_Neu PD signature have prior PD repositioning evidence (hypergeometric p<0.01). | Inconclusive |
| H2 | Top-50 reversers enriched for >=2 of 5 PD-relevant drug classes (Fisher, BH q<0.05). | Not testable (data) |

### `parkinson-metabolic-flux-sn-r1`

PD · [report](reports/parkinson-metabolic-flux-sn-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Composite primary: iMAT/Recon3D DA-neuron PD glycolytic flux decrease (H1a ratio<0.9, CI excl 1) AND sign concordance with Supandi 2018 (H1b). | Inconclusive |
| H1a | Bootstrap median PD/ctrl glycolytic flux ratio in DA neurons <0.9 with 95% CI excluding 1.0. | Inconclusive |
| H1b | Per-reaction flux-change signs concordant with Supandi 2018 in >=70% of shared reactions (binomial p<0.01). | Inconclusive |
| H3 | Iron-metabolism reaction flux ratio in PD DA neurons >1.1 with CI excluding 1.0. | Inconclusive |
| H4 | Per-reaction flux-change direction concordant across contextualisation methods (max pairwise Spearman rho >=0.5). | Inconclusive |
| H5 | Glycolysis signal cell-type separation: compare DA neurons vs Fullard GPi neurons and Micro_PVM (descriptive). | Not tested (run did not execute) |

### `parkinson-multimodal-ppmi-trajectory-r1`

PD · [report](reports/parkinson-multimodal-ppmi-trajectory-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | GPLVM 1-D latent disease-time from PPMI published summary tables correlates with time-from-diagnosis (rho>0.6, CI lower>0.4, n>=50). | Inconclusive |
| H2 | Model trained without dMRI recovers free-water dMRI rank order (leave-dMRI-out rho>=0.4, CI lower>0). | Inconclusive |
| H3 | LRRK2-G2019S carriers show leftward-shifted disease-time vs sporadic PD at matched stage (d>0.5, p<0.0125). | Not testable (data) |

### `parkinson-multimodal-spatial-proteomics-r1`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | MOFA+ on snRNA+Visium+proteomics yields >=1 factor with >5% variance in each modality AND PD-associated (Wilcoxon p<0.05). | Not tested (run did not execute) |
| H2 | Removing proteomics drops the matched factor's Visium explained variance by >=30 pp (permutation p<0.05). | Not tested (run did not execute) |
| H3 | Top-100 H1-factor genes enriched for LAMDA and/or Hemedan Boolean-PD regulators (hypergeometric q<0.05). | Not tested (run did not execute) |
| H4 | No single modality contributes >60% of H1-factor explained variance. | Not tested (run did not execute) |
| H5 | No pairwise MOFA+ model recovers a factor with loading \|r\|>=0.7 to the H1 factor. | Not tested (run did not execute) |

### `parkinson-multimodal-spatial-proteomics-r3`

PD · [report](reports/parkinson-multimodal-spatial-proteomics-r3.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | 3-modal MOFA+ (snRNA+spatial+proteomics) yields >=1 factor with R2>5% in all three modalities AND PD-associated (Wilcoxon p<0.05). | Not testable (data) |
| H2 | Proteomics ablation drops spatial R2 of matched factor by >=30 pp. | Not testable (data) |
| H3 | Top-100 H1-factor genes enriched for LAMDA ∪ Hemedan (hypergeometric q<0.05); not evaluable if H1 null not rejected. | Not testable (data) |
| H4 | No single modality contributes >60% of H1-factor explained variance. | Not testable (data) |
| H5 | No pairwise MOFA+ model recovers factor with \|r\|>=0.70 to the H1 factor. | Not testable (data) |

### `parkinson-plasma-prodromal-panel-r3`

PD · [report](reports/parkinson-plasma-prodromal-panel-r3/report.md)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Re-processing PXD046355 with DIA-NN + locked 8-protein LR yields 5-fold CV AUC >=0.85 for iRBD converter vs non-converter. | Not testable (data) |
| H2 | Per-protein univariate Cox HR signs match Hällqvist 2024 published HR directions (binomial). | Not testable (data) |
| H3 | Adding the 8-protein panel to clinical baseline improves 5-yr time-dependent AUC by >0.05 (CI excludes 0). | Not testable (data) |
| H5 | Functional sub-panels (inflammation, proteostasis, lipid) tested in 5-fold CV; any sub-panel AUC>0.75 = dominant. | Not testable (data) |

### `parkinson-plasma-prodromal-panel-r4`

PD · [report](reports/parkinson-plasma-prodromal-panel-r4.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Locked 8-protein LR on PXD046355 (DIA-NN or MOESM4 fallback) achieves 5-fold CV AUC >=0.85 for iRBD converter vs non-converter. | Inconclusive |
| H2 | Univariate Cox HR signs of 8 panel proteins match Hällqvist Supp Table 3 conversion HR signs (>=6/8 with binomial p<0.05). | Not testable (data) |
| H3 | Panel adds ΔAUC>0.05 over clinical-only (age, sex, MoCA, UPSIT) Cox model, CI lower >0. | Not testable (data) |

### `parkinson-prs-portability-r1`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | EUR 1000G LDpred-funct PRS liability-R2 within ±0.05 of Saffie-Awad 2025 EUR benchmark (AUC 0.621), bootstrap equivalence test | Not tested (run did not execute) |
| H2 | EAS/EUR ancestry-decay ratio within ±0.10 of Saffie-Awad ratio 0.931 | Not tested (run did not execute) |
| H3 | Storm 2025 protein-MR overlay adds ΔR2 >= 0.01 in EUR | Not tested (run did not execute) |
| H4 | Kim 2024 multi-ancestry PRS not worse than Nalls 2019 EUR-only PRS in EUR (DeLong p>0.10, Kim>=Nalls) | Not tested (run did not execute) |
| H5 | Bootstrap AUC-equivalent CI width >0.15 for at least one sub-population with n<200 | Not tested (run did not execute) |

### `parkinson-prs-portability-r3`

PD · [report](reports/parkinson-prs-portability-r3.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H3 | Storm 2025 pQTL protein-MR overlay increases EUR liability-R2 by >= 0.01 | Not testable (data) |
| H5 | Bootstrap AUC CI width >0.15 for at least one ancestry with n<200 (CI honesty) | Inconclusive |

### `parkinson-scenic-regulons-r1`

PD · [report](reports/parkinson-scenic-regulons-r1.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Top-20 Fullard SNpc-DA PD regulons replicate same-sign in all 3 held-out atlases (>=3 regulons) with binomial p<0.01 | Inconclusive |
| H2 | Consensus PD-up regulon TFs enriched (BH q<0.05) for Kim 2024 fine-mapped PD-risk genes | Not testable (data) |
| H3 | Per-donor consensus PD-up regulon activity correlates (rho>0.3) with AGTR1+ DA depletion | Not testable (data) |
| H4 | Leave-one-atlas-out RF on regulon scores classifies PD donors with mean AUC>=0.70 and CI excluding 0.5 | Inconclusive |

### `parkinson-tcell-foothold-r2`

PD · no final report (superseded or halted run)

| ID | Hypothesis | Verdict |
|---|---|---|
| H1 | Ma 2025 clonal CD8+ T-cell module PD-up (FDR<0.1) in >=3/4 independent snRNA-seq atlases, beating shuffled-label null | Inconclusive |
| H2 | T-cell module region ranking SNpc > M1 > V1 ≈ DMNX in Fullard (Spearman rho>=0.5, perm p<0.05) | Inconclusive |
| H3 | Per-donor T-cell module score correlates with AGTR1+ DA loss (rho>0.3, p<0.05) in >=2/4 atlases | Not testable (data) |
| H4 | Visium spots high in T-cell module co-enriched for reactive-astrocyte markers (rho>=0.3) | Not testable (data) |
| H5 | Negative control: exhaustion module NOT PD-enriched (FDR>0.1) in >=3/4 atlases | Inconclusive |

### `parkinson-tcell-foothold-r3`

PD · [report](reports/parkinson-tcell-foothold-r3.pdf)

| ID | Hypothesis | Verdict |
|---|---|---|
| H4 | Spatial T-cell module x reactive-astrocyte co-localisation (pre-registered as DEFERRED) | Not testable (data) |

### `pd-vatpase-lysosomal-compensation-r1`

PD · [report](reports/pd-vatpase-lysosomal-compensation-r1/report.md)

| ID | Hypothesis | Verdict |
|---|---|---|
| H2 | V-ATPase module higher in GBA-N370S vs control iPSC-DA in E-MTAB-7303 | Not testable (data) |
| H3 | iPSC-locked V-ATPase module higher in PD than control postmortem SN DA neurons (GSE157783); AUC and effect CIs exclude null | Inconclusive |
| H4 | V-ATPase shift is DA-neuron selective (DA-vs-other contrast CI excludes 0) | Inconclusive |
