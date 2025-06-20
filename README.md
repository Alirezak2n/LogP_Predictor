# MollogP Predictor (No-SMILES Model)

This repository provides a predictive model for estimating molecular logP values in the iDeepLC retention time prediction workflow, specifically designed for use in cases where SMILES annotations are not available.

## Background

iDeepLC is a deep learning-based tool for predicting peptide retention times in liquid chromatography–mass spectrometry (LC-MS) experiments. It leverages molecular properties, such as logP, of post-translational modifications (PTMs) to improve accuracy. When SMILES representations of modifications are available, logP values are directly computed from the molecular structure. However, in certain scenarios—such as novel, poorly annotated, or synthetic modifications—SMILES may be missing.

This model provides a fallback mechanism by predicting logP values based on descriptive features when molecular structure is unavailable.

## Recommended Workflow for Obtaining LogP Values

Before using this predictive model, I strongly encourage to follow the prioritized protocol below for sourcing SMILES:

1. **Check the CompOmics SMILES Repository**  
   First, verify whether the modification is already listed in the CompOmics SMILES database or available as output in the CSV files generated by iDeepLC tools.

2. **Search External Resources**  
   If not found, consult authoritative databases such as [PubChem](https://pubchem.ncbi.nlm.nih.gov), [ChEBI](https://www.ebi.ac.uk/chebi/), or search scientific literature and supplementary materials from relevant manuscripts.

3. **Contact the Maintainers**  
   If SMILES are still unavailable after a comprehensive search, users are invited to open an issue on this repository or contact the authors directly. We will make every effort to resolve missing annotations.

4. **Use This Model as a Fallback**  
   Only when all aforementioned methods are exhausted should this model be used to estimate logP. The model achieves a Pearson correlation of **0.85** with the reference logP values and is suitable for use as a fallback option in pipeline continuity.

## Features


This repository includes multiple components and methodological strategies to facilitate accurate logP prediction in the absence of molecular structures:

- **Skip-gram-based Amino Acid Embeddings**  
  Utilizes skip-gram models to generate distributed representations (embeddings) of amino acids for capturing contextual biochemical similarity.

- **Plain Sequence Tokenization**  
  Converts raw peptide or modification sequences into tokenized forms suitable for embedding and downstream modeling.

- **Molecular LogP Regression Model**  
  Core predictive model for estimating logP values using alternative representations when SMILES strings are unavailable.

- **Embedding-based LogP Prediction**  
  Applies learned amino acid embeddings to construct vector representations of modifications for input into regression models.

- **Multi-Layer Perceptron (MLP) with Cross-Validation**  
  Trains and evaluates MLP architectures for logP prediction using k-fold cross-validation to assess generalization.

- **MLP with One-Hot Encoding**  
  Alternative modeling approach using one-hot encoded representations of sequences as input to the MLP, providing a baseline for comparison with embeddings.

- **Principal Component Analysis (PCA) on Embeddings**  
  Includes dimensionality reduction of amino acid embeddings via PCA to visualize and assess variance structure in the learned representations.

