### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 04/08/2026
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```python
# Visitor segmentation based on characteristics
# read the data
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("clustervisitor.csv")
X = df["Age"].tolist()
k = 3

# Perform segmentation based on characteristics (e.g., age groups)
centroids = X[:k]
max_iterations = 100

for iteration in range(max_iterations):
    clusters = {i: [] for i in range(k)}
    cluster_labels = []

    for point in X:
        distances = [abs(point - c) for c in centroids]
        closest_cluster = distances.index(min(distances))
        clusters[closest_cluster].append(point)
        cluster_labels.append(closest_cluster)

    new_centroids = []
    for i in range(k):
        if clusters[i]:
            new_centroids.append(sum(clusters[i]) / len(clusters[i]))
        else:
            new_centroids.append(centroids[i])

    if new_centroids == centroids:
        break
        
    centroids = new_centroids

df['Cluster'] = cluster_labels
for i in range(k):
    print(f"Cluster {i + 1} (Centroid: {centroids[i]:.2f}):")
    print(df[df['Cluster'] == i])
    print()

```
### Output:
<img width="780" height="835" alt="image" src="https://github.com/user-attachments/assets/432feeb3-f35b-463f-9c5b-7438501f0168" />

### Visualization:
```python
colors = ['red', 'blue', 'green']
for i in range(k):
    cluster_data = df[df['Cluster'] == i]
    plt.scatter(
        cluster_data['Age'], 
        cluster_data['Cluster'], 
        color=colors[i % len(colors)], 
        label=f'Cluster {i + 1}'
    )

for i, c in enumerate(centroids):
    plt.scatter(c, i, color='black', marker='X', s=200)

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.legend()
plt.grid(True)
plt.show()
```
### Output:
<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/77862d69-df0e-4ec1-a5c7-dd06578e7594" />


### Result:
Thus, the K-Means clustering algorithm was successfully implemented, and the visitors were grouped into different clusters and visualized using a scatter plot.
