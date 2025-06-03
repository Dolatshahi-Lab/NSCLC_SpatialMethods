Tumor Microenvironment Spatial Analysis with Vectra Data
updated updated - 6_3_25 GH


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
3. 3-12-23_SpatialAnalysis_Vectra_Neighborfinding_Algorithms.ipynb
   •	Description: This code builds on the preprocessed Vectra data, modifying the dataframe to include the number of neighbors for each cell, classified by cell type.
   •	Output: A dataframe containing original Vectra data as well as a neighborhood profile for each cell. This enriched data is subsequently used in machine learning analysis.
5. 4-8-24_Public_PLS-DA_Only_InDepthAnalysis-multiradius-reundersampling-cellabundances.ipynb
  •	Objective: Perform PLS-DA analysis on Vectra data, utilizing neighborhood profiles as features.
  •	Input: Data from Vectra with appended neighborhood profiles.
  •	Output: Generates PLS-DA plots, VIP scores, confusion matrices, ROC curves, permutation tests, and results from re-undersampling, which are displayed as accuracy distributions.
7. SpatialAnalysis_KCrossCode_Public1.Rmd
   •Description: This R Markdown file evaluates spatial associations between specified center and target cells at a range of distances (e.g., 0-200 μm). Users can analyze multiple center cells for their spatial relationship to a single target cell for comparison in a single plot, with bootstrap confidence intervals for robustness.
  •	Output: Visualizations of spatial associations over varying radii, with theoretical comparisons based on Poisson distributions.

Files and Folders 
Folder 1: quality_control_and_processing
NSCLC_data_processing
    Description: Quality control and Processing of the data, analyzing distributions and assinging labels
    Output: Processed object data for input to NSCLC_neighbor_finding
NSCLC_neighbor_finding 
    Description: Runs custom neighborhood algorithm to create local neighborhood profiles for each cell at 30 and 200 um
    Output: neighborhood data for 30um and 200um
NSCLC_neighbor_matching
    Description: joins the 30um and 200um neighborhood data for downstream analysis
    
figureS1_residuals.ipynb
    Description: Code for figure S1. Looks at how log transforming the data affects model performance and residuals. 
    Pairs with figure S1

figure_2A_B_renderings.ipynb
    Description: Code associated with renderings used in figure 2. Here we create the images that will be modified in illustrator to demonstrate how the pipeline is working
    Pairs with figure 2A and 2B
    
figure_2C_D_counts_neighborhood_model_comparisons.ipynb
    Description: Code associated with the models that compare performance when using only phenotypic count data vs the transformed neighborhood data vs both. Here we create and compare the performance of models to benchmark whether this transformed data has additional information above and beyond simply count information.
    Pairs with figure 2C and 2D
    
figure_2E_G_distributions.ipynb
    Description: Code associated with the figures that investigate the structure of the transformed neighborhood data. 
    pairs with figure 2E, 2F, and 2G
    
figure_3_ifn_intensity.ipynb
    Description: Code associated with figure 3 which investigates the associateions between IFN gamma intensity and local neighborhood. 
    Includes all figure related pre processing, PLS modelilng, and univariate analysis and renderings

figure_6_luad_grade.ipynb
    Description: Code associated with figure 6 which looks at differences in neighborhoods between cells in high vs low grade LUAD patients. 
    Includes all case study specific preprocessing, modeling, univaraite analysis, and renderings.
   
figure_6_luad_grade.ipynb
    Description: Code associated with figure 6 which looks at differences in neighborhoods between cells in high vs low grade LUAD patients. 
    Includes network correlations related to figure 6