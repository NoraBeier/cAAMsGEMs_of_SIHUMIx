## SBML File Structure of SIHUMIx GEMs

The `SIHUMIx_GEMs` directory contains the original genome-scale metabolic models (GEMs) generated for the organisms of the Simplified Human Intestinal Microbiota (SIHUMIx).

The models are provided in **SBML Level 3 Version 1** format and use the **Flux Balance Constraints (FBC) Version 2** extension. The SBML files contain the metabolic network together with information required for flux balance analysis, including reaction bounds, an optimization objective, and gene–reaction associations.

The general structure of the SBML files is:

```text
<organism>.xml
└── sbml
    └── model
        ├── notes
        ├── listOfUnitDefinitions
        ├── listOfCompartments
        ├── listOfSpecies
        ├── listOfParameters
        ├── listOfReactions
        ├── listOfObjectives
        └── listOfGeneProducts
```

### `sbml`

The root `sbml` element defines the SBML document. The provided models use **SBML Level 3 Version 1** with the **FBC Version 2** extension. The FBC extension is used to represent model constraints such as reaction flux bounds and the optimization objective.

### `model`

The `model` element contains the complete genome-scale metabolic reconstruction.

Each model has a unique model identifier and contains the metabolic network, model constraints, objective definition, and gene–reaction information.

The model notes indicate that the models were generated using **CarveMe version 1.5.1**.

### `listOfUnitDefinitions`

The `listOfUnitDefinitions` section defines the units used in the model.

The provided models define:

```text
mmol_per_gDW_per_hr
```

corresponding to millimoles per gram dry weight per hour (mmol/gDW/h). The unit is defined from mole, gram, and second units with an appropriate scaling factor.

### `listOfCompartments`

The `listOfCompartments` section defines the cellular compartments represented in the model.

The provided models contain three compartments:

| ID    | Name                |
| ----- | ------------------- |
| `C_c` | cytosol             |
| `C_e` | extracellular space |
| `C_p` | periplasm           |

All three compartments are defined as constant compartments.

### `listOfSpecies`

The `listOfSpecies` section contains all metabolites (SBML species) included in the genome-scale metabolic model.

Each species contains information describing its identity, cellular compartment, chemical composition, and database annotations.

Relevant fields include:

| Field                 | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| `id`                  | SBML species identifier                                        |
| `metaid`              | Metadata identifier used for annotations                       |
| `name`                | Metabolite name                                                |
| `compartment`         | Compartment containing the metabolite                          |
| `boundaryCondition`   | Indicates whether the species is treated as a boundary species |
| `constant`            | Indicates whether the species is constant                      |
| `fbc:charge`          | Molecular charge                                               |
| `fbc:chemicalFormula` | Chemical formula                                               |
| `sboTerm`             | Systems Biology Ontology term                                  |
| `notes`               | Additional human-readable information                          |
| `annotation`          | Cross-references to external databases                         |

For example, a species can contain its chemical formula and charge directly in the SBML attributes:

```xml
<species
    id="M_10fthf_c"
    name="10-Formyltetrahydrofolate"
    compartment="C_c"
    fbc:charge="-2"
    fbc:chemicalFormula="C20H21N7O7">
```

The same information is also included in the `notes` section.

### `annotation`

Metabolites contain extensive annotations linking the model species to external databases.

The provided file uses **Identifiers.org** resources and includes cross-references to databases such as:

* Reactome
* KEGG Compound
* ChEBI
* HMDB
* BioCyc
* MetaNetX
* SEED
* InChIKey

For example, `M_10fthf_c` is linked to several external identifiers, including KEGG, ChEBI, HMDB, MetaNetX, BioCyc, SEED, Reactome, and an InChIKey.

These annotations provide standardized identifiers for connecting model metabolites with external biochemical databases.

### `listOfParameters`

The `listOfParameters` section contains numerical parameters used by the model.

In particular, parameters are used to define **reaction flux bounds**. The FBC extension allows reactions to reference lower and upper flux-bound parameters.

For example, the model contains a default lower-bound parameter:

```xml
<parameter
    id="cobra_default_lb"
    value="-1000"
    constant="true"/>
```

These parameters are referenced by reactions through the FBC attributes `fbc:lowerFluxBound` and `fbc:upperFluxBound`.

### `listOfReactions`

The `listOfReactions` section contains all reactions of the genome-scale metabolic model.

Each reaction defines its reaction identifier, name, reversibility, flux bounds, reactants, products, and, where available, gene–reaction associations.

Relevant fields include:

| Field                    | Description                                     |
| ------------------------ | ----------------------------------------------- |
| `id`                     | Reaction identifier                             |
| `metaid`                 | Metadata identifier                             |
| `name`                   | Reaction name                                   |
| `sboTerm`                | Systems Biology Ontology term                   |
| `reversible`             | Indicates whether the reaction is reversible    |
| `fast`                   | SBML reaction attribute                         |
| `fbc:lowerFluxBound`     | Reference to the lower flux bound               |
| `fbc:upperFluxBound`     | Reference to the upper flux bound               |
| `listOfReactants`        | Reactants and their stoichiometric coefficients |
| `listOfProducts`         | Products and their stoichiometric coefficients  |
| `geneProductAssociation` | Associated gene products                        |

The provided model contains 1,159 reactions and 830 species.

### `listOfReactants` and `listOfProducts`

The reactants and products of a reaction are represented using `speciesReference` elements.

Each `speciesReference` points to a metabolite defined in `listOfSpecies` and contains its stoichiometric coefficient.

For example:

```xml
<listOfReactants>
    <speciesReference
        species="M_dec4_2_coa_c"
        stoichiometry="1"/>
    <speciesReference
        species="M_h_c"
        stoichiometry="1"/>
    <speciesReference
        species="M_nadph_c"
        stoichiometry="1"/>
</listOfReactants>

<listOfProducts>
    <speciesReference
        species="M_dc2coa_c"
        stoichiometry="1"/>
    <speciesReference
        species="M_nadp_c"
        stoichiometry="1"/>
</listOfProducts>
```

Thus, the reaction stoichiometry can be reconstructed directly from the referenced species and their stoichiometric coefficients.

### Reaction Flux Bounds

Flux constraints are represented using the FBC extension.

Each reaction can reference a lower and upper flux-bound parameter using:

```text
fbc:lowerFluxBound
fbc:upperFluxBound
```

For example:

```xml
<reaction
    id="R_24DECOAR"
    reversible="false"
    fbc:lowerFluxBound="cobra_0_bound"
    fbc:upperFluxBound="R_24DECOAR_upper_bound">
```

This separates the reaction definition from its numerical flux constraints and allows the same parameters to be referenced by the model.

### `geneProductAssociation`

Reactions may contain a `geneProductAssociation` linking the reaction to one or more gene products.

For example:

```xml
<geneProductAssociation>
    <geneProductRef
        fbc:geneProduct="G_lcl_CP036346_1_prot_QMW73632_1_509"/>
</geneProductAssociation>
```

The `geneProduct` identifier refers to an entry in the `listOfGeneProducts` section. These associations provide the gene–reaction relationships required for connecting the metabolic network to its genomic information.

### `listOfObjectives`

The `listOfObjectives` section defines the optimization objective used for flux balance analysis.

The provided model contains an objective with:

```text
id: obj
type: maximize
```

and a flux objective targeting the reaction:

```text
R_Growth
```

with a coefficient of `1`. Thus, the model objective is defined by maximizing the flux through the `R_Growth` reaction.

The structure is:

```text
listOfObjectives
└── objective
    └── listOfFluxObjectives
        └── fluxObjective
            ├── reaction
            └── coefficient
```

### `listOfGeneProducts`

The `listOfGeneProducts` section contains the gene products associated with reactions in the metabolic model.

The provided model contains **654 gene products**. These entries are referenced by `geneProductAssociation` elements within reactions and establish the connection between genes/proteins and the corresponding metabolic reactions.

### Overall SBML Structure

The structure of the provided SIHUMIx SBML models can therefore be summarized as:

```text
<organism>.xml
└── sbml
    └── model
        ├── notes
        │   └── model generation information
        │
        ├── listOfUnitDefinitions
        │   └── mmol_per_gDW_per_hr
        │
        ├── listOfCompartments
        │   ├── C_c  → cytosol
        │   ├── C_e  → extracellular space
        │   └── C_p  → periplasm
        │
        ├── listOfSpecies
        │   └── species
        │       ├── chemical formula
        │       ├── charge
        │       ├── compartment
        │       ├── notes
        │       └── annotation
        │
        ├── listOfParameters
        │   └── flux-bound parameters
        │
        ├── listOfReactions
        │   └── reaction
        │       ├── listOfReactants
        │       │   └── speciesReference
        │       ├── listOfProducts
        │       │   └── speciesReference
        │       └── geneProductAssociation
        │
        ├── listOfObjectives
        │   └── objective
        │       └── fluxObjective
        │
        └── listOfGeneProducts
            └── geneProduct
```
