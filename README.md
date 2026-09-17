
<p align="center">
<img src="./logo.png" width="700"/>
</p>

## Complete Atom-to-Atom Mapped Genome-scale metabolic models of the Simplified Human Intestinal Microbiota 

This repository provides genome-scale metabolic models of the Simplified Human Intestinal Microbiota (SIHUMIx) with fully validated atom-to-atom mappings across the entire metabolic network.

These models enable detailed tracing of atomic transitions through biochemical reactions, supporting advanced analyses such as metabolic flux tracing, isotope labeling studies, and mechanistic investigations of microbial metabolism.

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

## Model Quality

All models achieve a MEMOTE score of **89%**, indicating high-quality, well-curated, and consistent metabolic reconstructions.

## JSON File Structure of GEMs

Each organism is provided as a JSON file containing the genome-scale metabolic model and its associated atom-to-atom mapping (AAM) information. The JSON structure is organized into five main sections:

```text
<organism>.json
├── stats
├── curations
├── metabolites
├── reactions
└── potential_problems
```

### `stats`

The `stats` section provides summary statistics for the model, including the number of species, metabolites, and reactions. Metabolites and reactions are further classified according to their structural and AAM status.

For example, reaction statistics distinguish between non-transport reactions, 1-to-1 transport reactions, other transport reactions, curated reactions, database-derived AAMs, generated AAMs, and reactions for which no AAM is available.

### `curations`

The `curations` section contains manually curated information used during model construction and AAM generation. It includes:

* `hydrogen metabolites`
* `curated_metabolites`
* `curated_reactions`
* `unmatched_reaction_curations`

Curated reactions contain atom-mapped reaction representations used to define or correct reaction mappings.

### `metabolites`

The `metabolites` section contains the metabolites included in the model. Each metabolite is stored using its metabolite name as a key and contains information such as:

| Field                            | Description                                                     |
| -------------------------------- | --------------------------------------------------------------- |
| `id`                             | Identifier of the metabolite                                    |
| `name`                           | Metabolite name                                                 |
| `sbml_species`                   | Mapping between model compartments and SBML species identifiers |
| `primary_structure`              | Primary molecular structure represented as SMILES               |
| `primary_structure_source`       | Source/method used to obtain the primary structure              |
| `primary_structure_std_features` | Structural standardization features                             |


### `reactions`

The `reactions` section contains all reactions of the genome-scale metabolic model. Each reaction is identified by its reaction ID and contains, among others, the following fields:

| Field               | Description                                                         |
| ------------------- | ------------------------------------------------------------------- |
| `id`                | Reaction identifier                                                 |
| `name`              | Reaction name                                                       |
| `is_transport`      | Indicates whether the reaction is a transport reaction              |
| `is_transport_1to1` | Indicates a 1-to-1 transport reaction                               |
| `compartment`       | Model compartment in which the reaction occurs                      |
| `lhs`               | Reactant stoichiometry                                              |
| `rhs`               | Product stoichiometry                                               |
| `selected_matching` | Selected atom-to-atom mapping and associated structural information |

The `lhs` and `rhs` fields contain the stoichiometric composition of the reaction using the corresponding metabolite IDs.

The `selected_matching.aam` field contains the atom-to-atom mapped reaction in mapped SMILES notation. Atom mapping numbers identify corresponding atoms between reactants and products and allow the fate of individual atoms to be traced through the reaction.

For selected reactions, additional information is provided for each reactant and product, including the corresponding `species_id`, metabolite name, SMILES representation, and `mapped_smiles`.

### `potential_problems`

The `potential_problems` section contains automatically identified issues associated with metabolites, reactions, and curation. It is divided into:

```text
potential_problems
├── metabolite_problems
├── reaction_problems
└── curation_problems
```

These entries document issues such as missing molecular structures, multiple alternative structures, incompatible structures, missing AAMs, unsuccessful structure matching, and other AAM-related problems.

## License

This dataset is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0).

## Citation

Please cite as:
Beier et al. (2026). Atom-to-Atom Mapped Genome-Scale Models for a Small Gut Microbiome Consortium.
