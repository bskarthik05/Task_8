# Customer Segmentation using K-Means Clustering

This project demonstrates unsupervised machine learning to segment customers from the "Mall Customers" dataset. The goal is to identify distinct groups of customers based on their annual income and spending score, which can help in devising targeted marketing strategies.

---

## Project Objective

The primary objective is to apply the K-Means clustering algorithm to partition customers into several groups. By understanding the characteristics of each group, a business can:

- Create targeted advertising campaigns.
- Develop personalized product recommendations.
- Optimize pricing and promotional strategies.

---

## Dataset

The project uses the `Mall_Customers.csv` dataset, which contains the following columns:
- **CustomerID**: A unique identifier for each customer.
- **Gender**: The gender of the customer.
- **Age**: The age of the customer.
- **Annual Income (k$)**: The annual income of the customer in thousands of dollars.
- **Spending Score (1-100)**: A score assigned by the mall based on customer behavior and spending nature (1 being low, 100 being high).

For this analysis, we primarily focus on **Annual Income (k$)** and **Spending Score (1-100)**.

---

## Technologies Used

- **Language**: Python 3
- **Libraries**:
  - `Pandas`: For data manipulation and loading the CSV file.
  - `Scikit-learn`: For implementing the K-Means algorithm, scaling data, and evaluating the model.
  - `Matplotlib` & `Seaborn`: For data visualization, including plotting the clusters and the Elbow Method graph.
  - `Numpy`: For numerical operations.

---

## The Process: Step-by-Step Explanation

The entire process is broken down into five main steps as implemented in the Python script.

### 1. Data Loading and Preprocessing

First, we load the `Mall_Customers.csv` dataset into a Pandas DataFrame. We then select the two features essential for our clustering analysis: `Annual Income (k$)` and `Spending Score (1-100)`.

Since K-Means is a distance-based algorithm, it's sensitive to the scale of the data. A feature with a larger range (like annual income) could dominate the clustering process over a feature with a smaller range. To prevent this, we use `StandardScaler` from Scikit-learn to standardize our data, giving all features a mean of 0 and a standard deviation of 1.

### 2. Finding the Optimal Number of Clusters (K) with the Elbow Method

A critical step in K-Means is choosing the number of clusters, K. We use the **Elbow Method** to find the optimal K.

- We iterate through a range of K values (e.g., from 1 to 10).
- For each K, we fit a K-Means model and calculate the **inertia**. Inertia is the sum of squared distances of samples to their closest cluster center (also known as Within-Cluster Sum of Squares or WCSS).
- We then plot the inertia for each K. The plot typically looks like an arm. The point where the rate of decrease in inertia sharply slows down forms an "elbow." This elbow point is considered the optimal number of clusters.

For our dataset, the elbow is clearly visible at **K=5**.

### 3. Fitting the K-Means Model

With the optimal K value of 5, we create an instance of the `KMeans` model from Scikit-learn and fit it to our scaled data. The `fit_predict` method assigns each data point (customer) to one of the 5 clusters. These cluster assignments are then added as a new column to our original DataFrame for easier analysis.

### 4. Visualizing the Clusters

To understand the results, we create a scatter plot of the customer data:

- The x-axis represents 'Annual Income'.
- The y-axis represents 'Spending Score'.
- Each point is color-coded based on the cluster it belongs to.
- The centroids (centers) of each cluster are marked with a red 'X'.

This visualization provides an intuitive understanding of the customer segments.

### 5. Evaluating the Clustering

Finally, we evaluate the quality of our clustering using the **Silhouette Score**.

- The Silhouette Score measures how similar an object is to its own cluster compared to other clusters.
- The score ranges from -1 to 1. A score close to +1 indicates that the clusters are dense and well-separated. A score near 0 indicates overlapping clusters, and a negative score usually indicates that samples might have been assigned to the wrong cluster.

Our model achieved a Silhouette Score of approximately **0.55**, which suggests that the clusters are reasonably well-defined.

---

## Results and Interpretation

The 5 clusters can be interpreted as distinct customer personas:

- **Cluster 0 (Orange): Careful Spenders** - High income but low spending score.
- **Cluster 1 (Purple): Standard Customers** - Average income and average spending score.
- **Cluster 2 (Green): Target Customers** - High income and high spending score. (**Prime Target**)
- **Cluster 3 (Blue): Careless Spenders** - Low income but high spending score.
- **Cluster 4 (Yellow): Sensible Customers** - Low income and low spending score.
