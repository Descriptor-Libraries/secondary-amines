# Library Details

<div class="centered-container">
     <img src="/secondary-amines/content/secondary-amines-workflow.png" alt="Secondary Amines Workflow" class="responsive-image">
</div>

## Molecule Identification

### Reaxys
Using the Reaxys database, a list of secondary alkyl amines was identified via substructure searching and subsequent filtering of results (exported on October 21st, 2021). Complete results of the substructure search were first limited to those listed as “product for purchase” that also appeared in the Sigma-Aldrich database, in order to maintain a reasonable number of commercially available compounds. The results from this substructure search were further filtered to limit the results to compounds for which the MW < 504 g/mol (to avoid large peptides) and the number of fragments = 1 (to eliminate salts). Incompatible functional groups (carboxylic acids, amino acids, carboxylates, hydoxamic acids, carbamic acids, primary amines, quaternary ammonium derivatives, α-amino acids, hydroxylamines, hemiaminals, thiohemiaminals, thiols, aryl thiols, alcohols, boronic acids, sulfonic acids, phosphonic acids, and di-amines) were explicitly excluded. This left a list of over 88,000 results which were further limited to those that were “present as a reactant” and appeared in > 10 references; the results of the search were exported as a list of SMILES strings and numbered as SecN1–SecN4256. Isotopically labeled amines (containing e.g., <sup>2</sup>H, <sup>13</sup>C, or <sup>15</sup>N) were removed. In cases where the library contained racemic and enantiopure forms of the same amine, a single example was retained in the library.

### Broad Institute’s Drug Repurposing Hub
The Broad Institute’s Drug Repurposing Hub of FDA-approved, clinical trial, and pre-clinical trial drugs was queried for amide containing drugs. The SMARTS string “CC(NC)=O” was used to identify drugs containing secondary and tertiary amides to obtain a list of 1988 compounds, 1744 of which could be handled by RDKit. SMARTS filtering was used to eliminate drugs containing functional groups incompatible with an amide coupling reaction as described above. Additionally, drugs containing multiple amides or amides that would fragment to give aryl or heteroaryl amines were excluded. RDKit was used to generate SMILES strings for the amine and amine fragments for each remaining amide. Duplicate amines were not added to the library.

### Enamine Building Blocks
Enamine’s top 50 secondary amine building blocks list was downloaded (August 25th, 2023). SMARTS filtering was used to eliminate compounds containing functional groups incompatible with an amide coupling reaction as described above. Duplicate amines were not added to the library.

## Conformational Searching & Conformer Selection

To capture the conformational flexibility of the substrates at a reasonable a computational cost, each secondary alkyl amine was subject to a gas phase molecular mechanics conformational search using Schrödinger MacroModel and the OPLS4 force field.  An ensemble of conformers within 21 kJ/mol (5.02 kcal/mol) of the minimum were collected, excluding mirror-image conformers. 

If the ensemble consisted of greater than 20 conformers, the number of conformers was reduced by atomic root mean square deviation (RMSD)-clustering to the minimum Kelley penalty value and taking the centroids of the resultant clusters. The Kelley index facilitates selection of the optimal number of clusters and ensures the selected conformers structurally diverse.

## DFT Computations

All DFT geometry optimizations and sequent frequency calculations (Gaussian 16, rev C.01) were performed at the B3LYP-D3(BJ)/6-31G(d,p)-LANL2DZ(I, Sn, Se) level of theory. The corresponding geometries were used for a series of single-point energy calculations at the M06-2X/def2-TZVP-SDD(I, Sn, Se) level of theory. 

From the DFT calculations, global, atomic, and bond-level properties were collected for each conformer using a [jupyter notebook.](https://github.com/nsf-c-cas/AcidAmine_Descriptor_Predict/tree/main/get_properties_examples/get_secondary_amine_properties_example) The dynamic range of properties across the conformational ensemble of a single amine was summarized by using five condensed measures for each of the properties.

| Descriptor              | Definition                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------|
| Boltz                   | Boltzmann-weighted average of a property from all the conformers in an ensemble (T = 298.15 K)  |
| max                     | highest value of a property given by any conformer in an ensemble                               |
| min                     | lowest value of a property given by any conformer in an ensemble                                |
| low_E                   | value of a property from the lowest energy conformer in the ensemble                            |
| Boltz_stdev             | Boltzmann-weighted (weighted by mole fraction) standard deviation of a property based on all the conformers in an ensemble (T = 298.15 K) |

An extended explanation of the computational workflow used to build the secondary alkyl amine library, as well as details on the collected and predicted descriptors can be found in the original publication supporting information.

## Citation
Haas, B. C., Hardy, M. A. Sowndarya S. V., S.; Adams, K.; Coley, C. W.; Paton, R. S.; Sigman, M. S. Rapid Prediction of Conformationally-Dependent DFT-Level Descriptors using Graph Neural Networks for Carboxylic Acids and Alkyl Amines. *ChemRxiv* **2024**. DOI: [10.26434/chemrxiv-2024-m5bpn](https://doi.org/10.26434/chemrxiv-2024-m5bpn)
