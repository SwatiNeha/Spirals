# Spirals: Motion Analysis for Control vs Parkinson’s Patients

This project analyzes **hand-drawn spiral data** collected from both Parkinson’s patients and healthy controls.  
By transforming raw `.svc` stylus signals into interpretable features, we explore how motor control differences manifest in drawing patterns, pen pressure, and kinematics.  

---

## Real-World Applications

This spiral motion analysis project goes beyond data science practice — it connects directly to healthcare and digital diagnostics.

In clinical settings, neurologists often ask patients to draw spirals as part of Parkinson’s assessments. By digitizing and analyzing these drawings, we can move from subjective visual judgment to quantitative metrics. Features like speed variability, pen pressure fluctuations, and jaggedness of curves can act as biomarkers for motor instability. This makes screening more consistent and scalable, especially in early detection.

For remote health monitoring, stylus-enabled tablets or smartphones could capture spirals at home, giving doctors continuous insights into disease progression without requiring frequent hospital visits. This would also allow clinical trials to collect richer data with less patient burden.

From a data science and research perspective, the pipeline demonstrates how handwriting and motion data can be transformed into meaningful features, clustered, and validated against known groups. The same methodology could be extended to other motor disorders (e.g., essential tremor, multiple sclerosis) or even to rehabilitation monitoring, where improvements in handwriting can signal therapy effectiveness.

In short, this project shows how a simple drawing task can be turned into a non-invasive, digital biomarker pipeline, bridging the gap between raw pen signals and actionable healthcare insights.

---

## Workflow

1. **Data Preprocessing**
   - Parse `.svc` files → `x, y, timestamp, pen_state, azimuth, altitude, pressure`  
   - Assign patient IDs (`Ill_1`, `Ctrl_2`, …)  
   - Remove timestamp outliers (per patient, IQR rule)  
   - Export cleaned datasets  

2. **Exploratory Data Analysis (EDA)**
   - Spiral drawings (`x vs y`)  
   - Time-series of x, y, pressure, azimuth, altitude vs timestamp  
   - 3D traces (`x, y, timestamp`)  
   - Correlation heatmaps  

3. **Feature Engineering** (per participant)
   - Speed, Acceleration  
   - Direction & Direction Change  
   - Pressure Variation  
   - Total Distance  
   - Avg Active Speed (threshold-based)  
   - CV of Speed, Peak Speed  

4. **Clustering**
   - **K-Means**, **DBSCAN**, **Agglomerative (Ward’s method)**  
   - Cluster validation: Silhouette, Davies–Bouldin, Dunn  
   - External validation: Adjusted Rand Index (ARI) vs Ill/Control labels  

5. **Dimensionality Reduction**
   - PCA (2D projection)  
   - t-SNE visualization  

---
## Visual Highlights

### Spiral & Motion Plots
![Spiral Comparison](figures/spirals.png)

Ill subjects show irregular, shaky spirals, while controls show smoother, more uniform curves.  

### Pressure & Pen Dynamics
![Pressure vs Time](figures/pressure.png)

Parkinson’s patients exhibit higher variability and inconsistency in pressure and pen tilt (azimuth/altitude).  

### Clustering Results
![Clustering](figures/clustering.png)

Different algorithms capture motor-control differences to varying degrees.  

### Validation Metrics
![Silhouette](figures/silhouette.png)

Silhouette indicate reasonable separation between Ill and Control groups.  

---

## Results at a Glance

| Method        | Avg. Silhouette ↑ | Davies–Bouldin ↓ | Dunn ↑ | Adjusted Rand Index ↑ |
|---------------|------------------|------------------|--------|------------------------|
| **K-Means**   | *0.640*           | *0.996*           | *0.288* | *0.464*                 |
| **DBSCAN**    | *0.624*           | *1.063*           | *0.393* | *0.464*                 |
| **AHC (Ward)**| *0.740*           | *0.891*           | *0.421* | *0.474*                 |

**↑ higher is better, ↓ lower is better**  

---
## Quick Start

1. Install dependencies in R:

   ```r
   install.packages(c(
     "dplyr","ggplot2","plotly","scatterplot3d","corrplot","tidyr",
     "ggthemes","RColorBrewer","reshape2","dbscan","fpc","clusterCrit",
     "mclust","Rtsne","cluster","dendextend","factoextra","FNN"
   ))

2. Place .svc files under:

    data_new/Ill/
   
    data_new/Control/

4. Run:
   
   ```r
   source("EDA_Merging.R")     # Preprocessing + visualization
   source("Final_Project.R")   # Feature engineering + clustering

---

## Key Insights

- Parkinson’s spirals are **irregular and jagged**, compared to smoother control spirals.  
- Pressure and tilt signals show **inconsistency** in patients, suggesting motor instability.  
- Clustering methods (especially **AHC**) separate Ill vs Control reasonably well.  
- **PCA/t-SNE** reveal clear latent structure, with Ill and Control often grouped separately.  

---

## Applications

- Non-invasive screening for Parkinson’s symptoms via handwriting  
- Feature engineering pipeline for digital pen data  
- Comparative evaluation of clustering methods for biomedical signals  

