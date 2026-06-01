# Clustering K-Means Algorithm

This repository contains a small R-based machine learning lab focused on **unsupervised learning with the K-Means clustering algorithm**.

The project demonstrates how to load a dataset, select relevant numerical features, normalize the data, run K-Means clustering, evaluate different values of `k` using the elbow method, animate the clustering process, and visualize the final clusters.

## Project Overview

The lab uses a crime-related dataset for the 50 U.S. states. The dataset includes crime occurrence or rate information such as:

- Murder
- Assault
- Rape
- Urban population
- Predefined cluster information

For the clustering exercise, the lab focuses primarily on two dimensions:

- `Murder`
- `Assault`

These two features are used to group states into clusters based on similarity in crime patterns.

## Main Objective

The objective of this project is to demonstrate the practical workflow of applying K-Means clustering to a simple dataset.

The lab walks through the following concepts:

1. Loading and inspecting the data
2. Selecting features for clustering
3. Visualizing the raw data distribution
4. Normalizing features using min-max scaling
5. Running K-Means clustering
6. Inspecting cluster assignments and centroids
7. Using the elbow method to evaluate the number of clusters
8. Animating the K-Means clustering process
9. Visualizing the final clusters with `ggplot2`

## Technologies Used

- R
- ggplot2
- animation
- stats

## What I Learned

Through this project I learned:

- How unsupervised learning differs from supervised learning and when clustering is an appropriate technique.
- Why feature normalization is critical for distance-based algorithms such as K-Means.
- How K-Means assigns observations to clusters by minimizing the distance to cluster centroids.
- How cluster centroids are iteratively updated until the algorithm converges.
- How to use the Elbow Method and total within-cluster sum of squares (distortion) to estimate an appropriate number of clusters.
- How visualization techniques can help interpret clustering results and identify natural groupings in data.
- How K-Means can be applied to real-world segmentation problems beyond crime data, including customer segmentation, defect analysis, warranty analytics, and operational pattern discovery.
- The importance of preprocessing and feature selection in achieving meaningful clustering outcomes.

## Dataset

The script expects a CSV file named `crime_data.csv` and uses the Murder and Assault features for clustering.

## Workflow

1. Load required packages.
2. Read and visualize the crime dataset.
3. Normalize features using min-max scaling.
4. Run K-Means clustering.
5. Evaluate candidate values of k using the Elbow Method.
6. Animate the clustering process.
7. Visualize final clusters and centroids.

## Key Concepts Demonstrated

- Unsupervised Learning
- K-Means Clustering
- Feature Scaling
- Min-Max Normalization
- Centroids
- Cluster Assignment
- Distortion Metrics
- Elbow Method
- Data Visualization
- Iterative Convergence

## How to Run

1. Clone the repository.
2. Open the project in RStudio.
3. Ensure `crime_data.csv` is available.
4. Run the lab script.

## Potential Enhancements

- Add sample output charts.
- Compare results for multiple values of k.
- Include business interpretation of cluster assignments.
- Convert the lab into an R Markdown notebook.
- Add reproducibility controls using random seeds.

## Summary

This project applies K-Means clustering to U.S. state crime data using Murder and Assault as the primary dimensions. It demonstrates the complete workflow of data preparation, normalization, cluster analysis, model evaluation, visualization, and interpretation.