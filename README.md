# Electric-Load-Forecasting

A data mining-based approach to forecast electric load demand in 10 major cities of the USA using time-series analysis.

## 📂 Overview

This project analyzes hourly electricity demand and weather data to:

* Identify consumption-weather patterns using clustering
* Predict future electricity demand using machine learning
* (In Progress) Develop a web interface for interactive data exploration

The project involves preprocessing, feature engineering, unsupervised learning, supervised forecasting, and visualizations.

---

## 📊 Dataset

* **Source**: Kaggle (`merged_data.csv`)
* **Size**: 212,066 hourly records
* **Features**:

  * `demand`, `precipIntensity`, `precipProbability`, `temperature`, `humidity`, `pressure`, `windSpeed`, `timestamp`

### 🔧 Preprocessing

* Dropped 25,924 rows with missing demand (12.22%) → 186,142 rows remaining
* Interpolated missing weather data using time-based methods (grouped by city)
* Feature Engineering: Extracted `hour`, `day of week`, `month`, `year`, `season`
* Removed \~1% outliers using `IsolationForest (contamination=0.01)`

---

## 📌 Methods

### Clustering Analysis

* **Dimensionality Reduction**:

  * PCA (2 components, 35.12% variance explained)
  * t-SNE (on 5,000-point subsample)
* **Algorithms**:

  * K-Means (k=4, elbow method, silhouette score: 0.138)
  * DBSCAN (eps=0.5, min\_samples=5; 5,859 clusters, 79,528 noise points)
  * Hierarchical Clustering (Ward linkage, 1,000-point subsample)

📈 **Best Performer**: K-Means based on silhouette score

---

### Predictive Modeling

* **Feature Engineering**: Added 24-hour lag (`demand_lag_24`)

* **Models Used**:

  * Naive Forecast (baseline)
  * Random Forest (n\_estimators=100, max\_depth=10)
  * Gradient Boosting (n\_estimators=100, max\_depth=3)
  * Stacking Ensemble (Random Forest + Gradient Boosting + Linear Regression)

* **Evaluation Metrics**: MAE, RMSE, MAPE

* **Split**: 80% training / 20% testing

#### 🔍 Results

| Model              | MAE         | RMSE        | MAPE       |
| ------------------ | ----------- | ----------- | ---------- |
| Naive Forecast     | 4375.58     | 5533.95     | 115.26%    |
| Random Forest      | 3108.30     | 3608.34     | 80.17%     |
| Gradient Boosting  | 3199.98     | 3640.38     | 84.64%     |
| **Stacking Model** | **3111.69** | **3583.76** | **81.45%** |

---

## 📊 Visualization

Saved in `plots/` directory:

* PCA and t-SNE visualizations
* Elbow curve and dendrogram
* K-Means cluster visualization
* Hourly demand plots
* Actual vs. predicted demand plots

---

## 🔎 Clustering Insights

* **Cluster 0**: Mixed patterns — 7309 MWh, temp: 0.47, hour: 12.5, month: 7.0
* **Cluster 1**: High-demand hot afternoons — 10838 MWh, temp: 0.70, hour: 14.3, month: 7.5
* **Cluster 2**: Mixed patterns — 6473 MWh, temp: 0.51, hour: 9.6, month: 9.8
* **Cluster 3**: Mixed patterns — 6495 MWh, temp: 0.46, hour: 10.8, month: 2.7

✅ **Key Insight**: Cluster 1 highlights peak demand on hot summer afternoons.

---

## 🚀 Installation

```bash
git clone https://github.com/your-username/Electric-Load-Forecasting.git
cd Electric-Load-Forecasting
pip install -r requirements.txt
```

Place `merged_data.csv` in the project root directory.

---

## 🛠 Usage

```bash
python preprocessing.py
python clustering.py
python modeling.py
```

View visualizations in the `plots/` directory.

To launch the web interface (coming soon):

```bash
python app.py
```

---

## 🔮 Future Work

* Complete web interface for interactive visualizations
* Add additional features
* Real-time data support
* Further model optimization

---

