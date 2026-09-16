# Customer Segmentation Using RFM Analysis and K-Means Clustering

## Project Overview

This project performs customer segmentation using RFM (Recency, Frequency, Monetary) analysis and K-Means clustering.

The main goal is to analyze customer purchasing behavior and group customers into meaningful segments based on their transaction history.

---

## Objectives

* Clean and preprocess the dataset
* Calculate RFM metrics
* Scale features for machine learning
* Apply K-Means clustering
* Use Elbow Method to find optimal clusters
* Evaluate clustering using:

  * Silhouette Score
  * Davies-Bouldin Index
* Visualize customer segments

---

## Dataset

The dataset contains the following columns:

* Invoice
* Invoice Date
* Customer ID
* Quantity
* Price

### Formula

TotalAmount = Quantity × Price

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Google Colab / Jupyter Notebook

---

## Project Workflow

Dataset
↓
Data Loading
↓
Data Cleaning
↓
Feature Engineering
↓
RFM Calculation
↓
Feature Scaling
↓
K-Means Clustering
↓
Evaluation
↓
Visualization

---

## Data Cleaning Steps

### 1. Load Dataset

```python
df = pd.read_csv("sales2.xlsx - Sheet1.csv")
```

### 2. Inspect Data

```python
df.head()
df.info()
df.describe()
```

### 3. Remove Missing Customer IDs

```python
df = df.dropna(subset=["Customer ID"])
```

### 4. Remove Invalid Records

```python
df = df[(df["Quantity"] > 0) & (df["Price"] > 0)]
```

### 5. Remove Duplicates

```python
df = df.drop_duplicates()
```

---

## Feature Engineering

```python
df["TotalAmount"] = df["Quantity"] * df["Price"]
```

---

## RFM Analysis

### Recency

Measures how recently a customer made a purchase.

### Frequency

Measures how often a customer makes purchases.

### Monetary

Measures how much money a customer spends.

### RFM Table

```python
rfm = df.groupby("Customer ID").agg(
    Recency=("InvoiceDate", lambda x: (reference_date - x.max()).days),
    Frequency=("Invoice", "nunique"),
    Monetary=("TotalAmount", "sum")
)
```

---

## Feature Scaling

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
rfm_scaled = scaler.fit_transform(rfm)
```

---

## K-Means Clustering

```python
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=2, random_state=42)
rfm["Cluster"] = kmeans.fit_predict(rfm_scaled)
```

---

## Elbow Method

```python
plt.plot(range(2, 11), inertia)
```

---

## Evaluation Metrics

### Silhouette Score

```python
from sklearn.metrics import silhouette_score
silhouette_score(rfm_scaled, rfm["Cluster"])
```

### Davies-Bouldin Index

```python
from sklearn.metrics import davies_bouldin_score
davies_bouldin_score(rfm_scaled, rfm["Cluster"])
```

---

## Visualization

```python
plt.scatter(rfm["Frequency"], rfm["Monetary"], c=rfm["Cluster"])
plt.show()
```

---

## Cluster Summary

```python
cluster_summary = rfm.groupby("Cluster")[["Recency","Frequency","Monetary"]].mean()
print(cluster_summary)
```

---

## Business Applications

* Customer retention strategies
* Personalized marketing campaigns
* Loyalty programs
* Targeted promotions
* Identification of high-value customers

---

## How to Run

1. Clone the repository
2. Open the notebook in Jupyter or Google Colab
3. Upload the dataset
4. Install required libraries
5. Run all cells

---

## Key Takeaway

Data Cleaning → RFM → Scaling → Clustering → Evaluation → Insights


## Lakshiya s s
