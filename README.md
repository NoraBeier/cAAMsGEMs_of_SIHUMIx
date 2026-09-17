# Complete Atom-to-Atom Mapped Genome-scale Metabolic Models of the Simplified Human Intestinal Microbiota

This repository provides genome-scale metabolic models of the **Simplified Human Intestinal Microbiota (SIHUMIx)** together with comprehensive atom-to-atom mapping (AAM) information.

The dataset supports detailed investigations of microbial metabolism, including **atom tracing, isotope-labeling studies, metabolic flux analysis, and mechanistic analyses of biochemical reactions**.

## Included Organisms

The dataset includes the following organisms:

* *Anaerostipes caccae*
* *Bacteroides thetaiotaomicron*
* *Bifidobacterium longum*
* *Blautia producta*
* *Clostridium butyricum*
* *Clostridium ramosum*
* *Escherichia coli* K-12
* *Lactobacillus plantarum*

## Data

The `data` directory contains three different datasets, each serving a distinct purpose:

```text
data/
├── SIHUMIx_GEMs/
├── cAAMsGEMs/
└── Pathways/
```

### `SIHUMIx_GEMs`

The `SIHUMIx_GEMs` directory contains the **originally generated genome-scale metabolic models (GEMs)** of the SIHUMIx organisms.

These models represent the original metabolic reconstructions and provide the baseline model data, including metabolites, reactions, stoichiometry, compartments, and model constraints.

### `cAAMsGEMs`

The `cAAMsGEMs` directory contains **curated, atom-to-atom mapped genome-scale metabolic models**.

These models extend the original GEMs with comprehensive molecular structure information and atom-to-atom mappings across the metabolic network.

In particular, the `cAAMsGEMs` dataset provides:

* curated molecular structures for metabolites
* standardized structural information
* atom-to-atom mappings (AAMs) for metabolic reactions
* mapped reactant and product structures
* information describing the provenance and curation of structures and mappings
* identification of potential structural and mapping problems

The `cAAMsGEMs` therefore provide the main dataset for analyses that require **complete structural information and atom-level tracing through the metabolic network**.

### `Pathways`

The `Pathways` directory contains **atom-to-atom mappings for many different metabolic pathways**.

This dataset is currently **under development**.

Unlike the organism-specific genome-scale models in `cAAMsGEMs`, the `Pathways` dataset focuses on providing AAM information at the **pathway level**. It is intended to make atom-to-atom mappings available for a broad collection of metabolic pathways and reactions, including pathways that are not necessarily restricted to the SIHUMIx genome-scale models.

The pathway dataset is therefore intended as a complementary resource for **pathway-level atom tracing and mechanistic metabolic analyses**.

## Data Overview

The three datasets can be summarized as follows:

| Dataset        | Description                                               | Main purpose                                  |
| -------------- | --------------------------------------------------------- | --------------------------------------------- |
| `SIHUMIx_GEMs` | Original genome-scale metabolic models                    | Original metabolic reconstructions            |
| `cAAMsGEMs`    | Curated GEMs with complete structure information and AAMs | Atom-level tracing within genome-scale models |
| `Pathways`     | AAMs for a broad collection of metabolic pathways         | Pathway-level atom tracing                    |


## Model Quality

The SIHUMIx genome-scale metabolic models achieve a **MEMOTE score of 89%**, indicating high model consistency and quality under the MEMOTE framework.

## License

This dataset is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0).

## Citation

Please cite as:

> Beier et al. (2026). *Atom-to-Atom Mapped Genome-Scale Models for a Small Gut Microbiome Consortium.*
