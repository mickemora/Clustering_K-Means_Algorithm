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

This project is written in **R** and uses the following packages:

- `ggplot2` - for data visualization
- `animation` - for visualizing the K-Means clustering process
- `stats` - for the built-in `kmeans()` function

## Dataset

The script expects a CSV file named:

```text
crime_data.csv
```

The code reads the dataset using:

```r
crime0 <- read.csv("crime_data.csv")
```

Then it selects the `Murder` and `Assault` columns for clustering:

```r
crime <- crime0[, c('Murder','Assault')]
```

## Workflow

### 1. Load Required Packages

The lab installs and loads the packages required for visualization and animation:

```r
install.packages("ggplot2")
install.packages("animation")

library(ggplot2)
library(animation)
```

### 2. Load and Explore the Dataset

The script reads the crime dataset and creates an initial scatter plot of the selected variables:

```r
plot(crime, pch=16)
```

This helps visualize the distribution of the data before clustering.

### 3. Normalize the Data

Because K-Means is distance-based, feature scale matters. The lab defines a custom min-max normalization function:

```r
normIt <- function(feature){
  normalized <- ((feature - min(feature)) / (max(feature) - min(feature)))
  return(normalized)
}
```

The normalization step helps prevent one variable from dominating the clustering result simply because it has a larger numeric range.

### 4. Run K-Means Clustering

The lab initially runs K-Means using five clusters:

```r
c1 <- kmeans(nor_crime, 5)
```

It then inspects the result object to understand the cluster assignments and cluster centers.

### 5. Evaluate Cluster Count with the Elbow Method

The project defines helper functions to calculate total within-cluster sum of squares, also called distortion:

```r
kmeans.totwithinss.k <- function(dataset, number_of_centers){
  km <- kmeans(dataset, number_of_centers)
  km$tot.withinss
}
```

The lab then evaluates values of `k` from 1 to 10 and plots the elbow curve:

```r
maxk <- 10
dis_vct <- kmeans.distortion(nor_crime, maxk)

plot(1:maxk,
     dis_vct,
     type = 'b',
     col = 'blue',
     xlab = "Number of cluster",
     ylab = "Total WithinSS",
     main = "Elbow Curve Plot")
```

The lab notes that the distortion begins to stabilize around **k = 4 or k = 5**, suggesting that either value may be a reasonable cluster count.

### 6. Animate K-Means

The project uses the `kmeans.ani()` function from the `animation` package to visualize how K-Means iteratively updates cluster centers:

```r
num_cluster = 4
result <- kmeans.ani(nor_crime, num_cluster)
```

This helps illustrate how the algorithm converges toward final clusters.

### 7. Visualize Final Clusters

The final visualization uses `ggplot2` to plot the normalized murder and assault values, color-coded by cluster assignment. Cluster centers are shown as black points.

```r
plot.crime <- ggplot(data = nor_crime, aes(x = Murder, y = Assault, color = result$cluster))

plot.crime + geom_point(alpha = .25, size = 5) +
  geom_point(data = centers, aes(x = Murder, y = Assault), size = 5, color = 'black') +
  scale_color_gradientn(colours = rainbow(num_cluster)) +
  theme(plot.title = element_text(hjust = 0.5)) +
  ggtitle("K-means clusters")
```

## Key Concepts Demonstrated

This project demonstrates several foundational machine learning and data mining concepts:

- Unsupervised learning
- K-Means clustering
- Feature scaling
- Min-max normalization
- Centroids / cluster centers
- Cluster assignment
- Total within-cluster sum of squares
- Distortion
- Elbow method
- Cluster visualization
- Iterative convergence

## How to Run

1. Clone this repository:

```bash
git clone https://github.com/mickemora/Clustering_K-Means_Algorithm.git
```

2. Open the project in RStudio or another R environment.

3. Make sure the file `crime_data.csv` is available in the working directory.

4. Run the lab script.

5. Install any missing packages when prompted.

## Notes

This repository is intended as a learning lab rather than a production machine learning application. It is useful for understanding the mechanics of K-Means clustering, especially the importance of normalization and choosing an appropriate number of clusters.

## Potential Enhancements

Future improvements could include:

- Adding the `crime_data.csv` file or linking to the data source
- Adding sample output charts
- Comparing results for `k = 4` and `k = 5`
- Adding a short business interpretation of each cluster
- Refactoring the lab into a more formal R script or R Markdown notebook
- Adding comments about reproducibility and random seeds

## Summary

This project applies K-Means clustering to U.S. state crime data using `Murder` and `Assault` as the main clustering dimensions. It demonstrates the end-to-end clustering workflow: data loading, normalization, cluster modeling, elbow curve analysis, animation, and final visualization.
