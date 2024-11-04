Tumor Microenvironment Spatial Analysis with Vectra Data

This repository contains code for spatial analysis in the tumor microenvironment, with a focus on cell phenotypes and their spatial relationships using data from Vectra multiplex immunohistochemistry (mIHC) analysis. Our workflow includes custom neighbor-finding algorithms, Partial Least Squares Discriminant Analysis (PLS-DA), and additional spatial analysis using the R package spatstat.

Project Overview
In this project, we developed a custom neighbor-finding algorithm to analyze biomarker data derived from Vectra mIHC results in tumor biopsy samples. For each cell, neighbors within 30 μm and 200 μm were identified and classified by cell type, creating a "neighborhood profile" for each cell. This profile was appended to the original Vectra-derived data, enriching it with spatial context for downstream analyses.

Analysis Components
1.	PLS-DA and PLS-R Analysis:
We implemented PLS-DA and Partial Least Squares Regression (PLS-R) using Python and the scikit-learn library to examine spatial neighbor features associated with cell phenotypes. This approach enabled us to highlight distinguishing spatial features that correlate with specific cell types. Model performance was thoroughly assessed, including variable importance in projection (VIP) scores for feature ranking.
2.	Spatial Analysis with spatstat in R:
Additional spatial analysis was conducted using spatstat (Baddeley et al.), which provided further validation of VIP-selected cell neighborhood features. This spatial analysis utilized coordinates generated from HALO Vectra analysis to confirm and extend findings from the PLS-DA results.

Files and Notebooks
1. 1-29-23_SpatialAnalysis_Vectra_PreProcessing.ipynb
•	Description: This notebook processes Vectra object data from mIHC tumor biopsies, defining cell types and performing other preprocessing steps.
•	Output: The resulting CSV file serves as input for the neighbor-finding algorithm. Cell types and data format align with those described in Wessel et al., 2024.
2. 3-12-23_SpatialAnalysis_Vectra_Neighborfinding_Algorithms.ipynb
•	Description: This code builds on the preprocessed Vectra data, modifying the dataframe to include the number of neighbors for each cell, classified by cell type.
•	Output: A dataframe containing original Vectra data as well as a neighborhood profile for each cell. This enriched data is subsequently used in machine learning analysis.
3. 4-8-24_Public_PLS-DA_Only_InDepthAnalysis-multiradius-reundersampling-cellabundances.ipynb
•	Objective: Perform PLS-DA analysis on Vectra data, utilizing neighborhood profiles as features.
•	Input: Data from Vectra with appended neighborhood profiles.
•	Output: Generates PLS-DA plots, VIP scores, confusion matrices, ROC curves, permutation tests, and results from re-undersampling, which are displayed as accuracy distributions.
4. SpatialAnalysis_KCrossCode_Public1.Rmd
•Description: This R Markdown file evaluates spatial associations between specified center and target cells at a range of distances (e.g., 0-200 μm). Users can analyze multiple center cells for their spatial relationship to a single target cell for comparison in a single plot, with bootstrap confidence intervals for robustness.
•	Output: Visualizations of spatial associations over varying radii, with theoretical comparisons based on Poisson distributions.

