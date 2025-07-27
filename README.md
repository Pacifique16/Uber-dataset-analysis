

# **🚕 Uber Fares Dataset Analysis using Power BI**

This project explores Uber ride data using **Python for data preparation** and **Power BI for visualization and storytelling**. From cleaning raw fare records to building a powerful interactive dashboard, this project uncovers how time, distance, and location affect fare pricing.

---

## 📦 Dataset

* **Source**: [Kaggle – Uber Fares Dataset](https://www.kaggle.com/datasets/yasserh/uber-fares-dataset)
* **Size**: 17,847 rows after cleaning
* **Features**:

  * Fare amount
  * Pickup & dropoff coordinates
  * Pickup timestamp
  * Passenger count

---

## 💻 Technologies Used

* Python (Pandas, NumPy, Seaborn, Matplotlib)
* Google Colab (for scripting & data cleaning)
* Power BI Desktop (for dashboard creation)
* GitHub (for hosting code and deliverables)

---

## 👨‍🎓 Author

**Pacifique HARERIMANA**
*AUCA – Introduction to Big Data Analytics (INSY 8413)*
Instructor: Eric Maniraguha

---

## 🧹 Data Preparation in Python

Cleaned, transformed, and enriched the dataset using Google Colab.

```python
import pandas as pd

# Load and inspect data
df = pd.read_csv("uber.csv")

# Drop unnecessary columns
df.drop(columns=["Unnamed: 0", "key"], inplace=True)

# Convert to datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'], errors='coerce')

# Drop missing records
df.dropna(inplace=True)
```

✅ **Final shape**: 17,847 rows × 7 columns
📷 *Screenshot: Data preview in Colab*

---

## 🧠 Feature Engineering

Added useful analytical fields:

```python
# Calculate ride distance using Haversine formula
from numpy import radians, sin, cos, sqrt, arctan2

def haversine(lat1, lon1, lat2, lon2):
    R = 6371  # Earth's radius in km
    dlat = radians(lat2 - lat1)
    dlon = radians(lon2 - lon1)
    a = sin(dlat/2)**2 + cos(radians(lat1)) * cos(radians(lat2)) * sin(dlon/2)**2
    return 2 * R * arctan2(sqrt(a), sqrt(1-a))

df['distance_km'] = haversine(
    df['pickup_latitude'], df['pickup_longitude'],
    df['dropoff_latitude'], df['dropoff_longitude']
)

# Time-based features
df['hour'] = df['pickup_datetime'].dt.hour
df['month'] = df['pickup_datetime'].dt.month
df['weekday'] = df['pickup_datetime'].dt.dayofweek
df['peak_hour'] = df['hour'].apply(lambda x: 1 if x in [7,8,9,17,18,19] else 0)
```

📷 *Screenshot: Feature columns in DataFrame*

---

## 📤 Export to Power BI

```python
df.to_csv("uber_cleaned.csv", index=False)

# Trigger download in Colab
from google.colab import files
files.download("uber_cleaned.csv")
```

📷 *Screenshot: Export and download step in Colab*

---

## 📊 Power BI Dashboard Overview

The final dashboard includes multiple visuals with slicers, filters, and interactivity.

| 🔎 Insight                 | 📈 Chart Type                |
| -------------------------- | ---------------------------- |
| Fare distribution          | Histogram (binned bar chart) |
| Peak hours of travel       | Line chart                   |
| Trends across weekdays     | Clustered column chart       |
| Seasonal/monthly variation | Line chart                   |
| Ride length estimation     | Based on distance            |
| Pickup location patterns   | Map/Scatter                  |

📷 *Screenshots: Each visual on dashboard*

---

## 🎯 Key Insights

* 🚕 Most rides are **short-distance**, low-fare trips (\$5–\$20)
* 🕒 **Evening hours** (5–7 PM) have the highest ride volume
* 🗓️ Fridays and Saturdays record **higher average fares**
* 🌍 Dense ride activity in **central urban areas** (via map)
* 📏 Fares generally scale with distance — but outliers exist

---

## 🧠 Unique Value

To enhance this project and stand out:

✅ Added a **fare binning DAX column** for histogram clarity
✅ Used a **custom scatter chart** workaround for map when native maps were disabled
✅ Applied **interactive slicers** to allow users to filter by:

* Hour of day
* Weekday
* Peak hour
* Passenger count

---



## 💬 Final Thought

> "A good dashboard doesn’t just show data — it tells a story."
> This project transforms raw Uber data into meaningful insights that could help any urban ride-sharing service optimize operations.

---


