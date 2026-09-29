# Pathways

The `Pathways` dataset provides atom-to-atom mappings (AAMs) for metabolic reactions grouped by pathway. The reactions are derived from the *Escherichia coli* K-12 MG1655 genome-scale model, while the assignment of reactions to metabolic pathways is based on pathway annotations from EcoCyc.

Each CSV file corresponds to one metabolic pathway and contains the reactions associated with that pathway. The files are named according to the corresponding pathway.

## File structure

Each pathway file contains the following columns:

| Column           | Description                                                                                                                                          |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Reaction_index` | EcoCyc reaction identifier for the reaction.                                                                                                         |
| `Substrate`      | EcoCyc metabolite identifiers of the reaction substrates. Multiple metabolites are comma-separated.                                                  |
| `Product`        | EcoCyc metabolite identifiers of the reaction products. Multiple metabolites are comma-separated.                                                    |
| `Bigg_IDs`       | BiGG reaction identifier(s) corresponding to the reaction in the *E. coli* K-12 MG1655 genome-scale model.                                           |
| `AAMs`           | Atom-to-atom mapping of the reaction. Atoms are represented using atom-map numbers to indicate their correspondence between substrates and products. |

