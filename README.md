# RNA-seq Data Analysis Script

## Overview
This script performs analyses on bulk RNA-seq data, specifically focusing on merging RNA-seq count files from two separate runs, followed by optional sample renaming and the application of two dimensionality reduction methods: **Principal Component Analysis (PCA)** and **Uniform Manifold Approximation and Projection (UMAP)**. These methods allow for the visualization and interpretation of high-dimensional gene expression data.

The script consists of three main steps:

1. **Data Preparation**: Merging and optional renaming of RNA-seq data files.
2. **Principal Component Analysis (PCA)**: A linear dimensionality reduction method to explore sample variability.
3. **Uniform Manifold Approximation and Projection (UMAP)**: A non-linear dimensionality reduction method that uncovers complex patterns in gene expression data.

## Prerequisites

### Software Requirements
- Python 3.x is required to run this script.

### Conda Environment
Make sure you have created a Conda environment with the required packages. You can set it up using the `environment.yml` file included in the repository.

To create the environment, run:

```bash
conda env create -f environment.yml
```

### Input Files
- **RNA-seq Count Files**: Two Excel files (`run1.xlsx` and `run2.xlsx`) containing RNA-seq counts with gene symbols and sample information.
- **Sample Metadata File**: An Excel file (`Samples_metadata.xlsx`) containing metadata for each sample, such as disease type, differentiation state, and RNA-seq run.

## Script Workflow

### 1. Data Preparation: Merging and Renaming
The script begins by merging two separate RNA-seq count data files (from `run1.xlsx` and `run2.xlsx`) based on their common gene symbols. Missing values are filled with zeros. After merging, the script optionally renames specific sample columns, as defined by a dictionary (`rename_dict`). The final merged and renamed dataset is saved to an Excel file for further analysis.

**Key Functions:**
- Merging of RNA-seq count files using the `pd.merge()` function.
- Optional renaming of sample columns for better clarity.
- Writing the merged and renamed dataset to Excel files (`combined_run1run2.xlsx` and `renamed_combined_run1run2.xlsx`).

### 2. Principal Component Analysis (PCA)
PCA is a linear dimensionality reduction technique used to identify major sources of variation in gene expression data. This step involves:

- Scaling the RNA-seq data using `StandardScaler`.
- Performing PCA to extract the first two principal components (PC1 and PC2).
- Merging PCA results with the sample metadata for visualization.
- Generating a scatter plot of the PCA results, showing how samples cluster based on disease type, differentiation type, and RNA-seq run.

**Key Functions:**
- `PCA()` from `sklearn.decomposition` to compute principal components.
- `sns.scatterplot()` from `seaborn` to visualize PCA results.

### 3. Uniform Manifold Approximation and Projection (UMAP)
UMAP is a non-linear dimensionality reduction method that preserves complex relationships in the data. The script applies UMAP to the RNA-seq data, generating a 2D embedding (UMAP1 and UMAP2), which is then merged with the sample metadata for visualization.

**Key Functions:**
- `umap.UMAP()` to create a UMAP model and transform the RNA-seq data into lower dimensions.
- `sns.scatterplot()` to visualize UMAP results.

### 4. Visualization
Both PCA and UMAP results are visualized as scatter plots, with different colors and markers representing disease types, differentiation states, and RNA-seq runs. Sample labels are added to each point for easier identification.

The resulting plots are saved as JPEG images (`PCA_plot.jpeg` and `UMAP_plot.jpeg`), and displayed within the script.

## Output Files
- **Merged Data**: 
  - `combined_run1run2.xlsx` (before renaming) 
  - `renamed_combined_run1run2.xlsx` (after renaming)
- **Plots**: 
  - `PCA_plot.jpeg` (PCA result) 
  - `UMAP_plot.jpeg` (UMAP result)

## Usage Instructions
1. Ensure the input files (`run1.xlsx`, `run2.xlsx`, and `Samples_metadata.xlsx`) are in the same directory as the script.
2. Run the script in a Python environment using:

```bash
python RNA_seq_analysis_final.py
```

The script will output two Excel files and two visualizations, saved in the current working directory.

## Expected Results
In the test data provided, we expect that samples with **IPS** state will group together, while **NPC** and **NRN** states will group all together.

## Example Output
- **PCA Plot**: Visualizes how samples cluster based on the first two principal components.
- **UMAP Plot**: Visualizes the UMAP embedding, revealing patterns in gene expression across samples.

## Additional Notes
- The sample renaming step is optional and can be customized by modifying the `rename_dict` dictionary.
- PCA and UMAP parameters can be adjusted to optimize the visualization for your specific dataset.

## Additional Information

- This script was developed for the final project of **Python_for_biologists** course (Autumn 2024, Gothenburg University, Sweden), and it can be modified to suit specific requirements.
- If you encounter any problems while using this script, please feel free to reach out to me at <a href="parvanehnikpour@gmail.com" style="text-decoration: underline;">Your Email</a>. I’m happy to assist you with any issues you may face.
