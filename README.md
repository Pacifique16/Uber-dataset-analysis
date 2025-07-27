# **🚕 Uber Fares Analysis with Power BI**

A full-cycle data analysis project using **Python (Pandas)** and **Power BI** to uncover insights from the Uber Fares Dataset. This project demonstrates real-world data wrangling, exploratory data analysis, and interactive dashboard development for data storytelling.

<br>

## 👨‍🎓 Author
 **NAME**:   Pacifique HARERIMANA
 <br>
 **ID**:        26937
 <br>
 **CONCENTRATION**:   Software Engineering

<br>
<br>

# 🚦 PHASE 1: Dataset Understanding & Cleaning

### 📦 Dataset Source

* [Uber Fares Dataset – Kaggle](https://www.kaggle.com/datasets/yasserh/uber-fares-dataset)

### 🧾 Initial Columns:

* `key`, `fare_amount`, `pickup_datetime`, `pickup_longitude`, `pickup_latitude`, `dropoff_longitude`, `dropoff_latitude`, `passenger_count`

### ✅ Steps Performed:

```python
# Load Data
df = pd.read_csv("uber.csv")

# Drop extra columns
df.drop(columns=["Unnamed: 0", "key"], inplace=True)

# Convert datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'], errors='coerce')

# Drop missing rows
df.dropna(inplace=True)
```





# 📊 PHASE 2: Exploratory Data Analysis (EDA)

### 🔍 Descriptive Stats

```python
df.describe()
```
<br>
Result:
<br>
<img width="1320" height="523" alt="describe" src="https://github.com/user-attachments/assets/d0f1eec4-b199-4833-b167-02a6a35c9750" />
<br>
<br>

### 📌 Outlier Check

```python
print("Max Fare:", df['fare_amount'].max())  # 350.0
```
<br>
Result:
<br>
<img width="1397" height="507" alt="outlier detection" src="https://github.com/user-attachments/assets/ade524f6-bd1c-4057-9b4f-e624f4aa320c" />
<br>
<br>

# 📏 PHASE 3: Feature Engineering

### 🌍 Haversine Distance Formula

```python
def haversine_distance(lat1, lon1, lat2, lon2):
    # simplified for readability
    ...

df['distance_km'] = haversine_distance(
    df['pickup_latitude'], df['pickup_longitude'],
    df['dropoff_latitude'], df['dropoff_longitude']
)
```
<br>

### 🕒 Time Features

```python
df['hour'] = df['pickup_datetime'].dt.hour
df['day'] = df['pickup_datetime'].dt.day
df['month'] = df['pickup_datetime'].dt.month
df['weekday'] = df['pickup_datetime'].dt.dayofweek
df['peak_hour'] = df['hour'].apply(lambda x: 1 if x in [7,8,9,17,18,19] else 0)
```

Result:
<br>
<img width="691" height="266" alt="hour, day, month, weekday, peak time," src="https://github.com/user-attachments/assets/7246c090-e747-4874-b1ba-dd716a647f25" />

<br>
<br>


# 💾 PHASE 4: Export for Power BI

```python
df.to_csv("uber_cleaned.csv", index=False)
```

<br>

# 📈 PHASE 5: Power BI Visualization Dashboard

> 📍 **Power BI File**: `uber_fare_dashboard.pbix`

### ✅ Completed Visuals:

| Visual                | Type               | Insight              |
| --------------------- | ------------------ | -------------------- |
| **Fare Distribution** | Histogram          | Pricing spread       |
| **Fares by Hour**     | Line Chart         | Peak times           |
| **Fares by Weekday**  | Column Chart       | Weekly trends        |
| **Fares by Month**    | Line Chart         | Seasonal variation   |
| **Geographic Map**    | Map/Scatter        | Pickup hot zones     |
| **Ride Duration**     | Proxy via distance | Trip length behavior |

<br>
Result:
<br>
<img width="1347" height="750" alt="1" src="https://github.com/user-attachments/assets/38d48cb6-e222-407c-a9ef-c0b98b8819ba" />
<br>
<img width="1166" height="627" alt="2" src="https://github.com/user-attachments/assets/aa3b692d-bbf6-4c19-9e73-0f15ce269313" />
<br>
<img width="1147" height="651" alt="3" src="https://github.com/user-attachments/assets/29b4be82-2512-42f8-aaf8-ab5b82b864d8" />
<br>
<img width="1061" height="596" alt="4" src="https://github.com/user-attachments/assets/c16597d4-f6b1-4b07-8c2f-147c39a3d28b" />

<br>
<br>

# 🧠 PHASE 6: Analytical Insights

* 🕛 Most rides occur between **5 PM – 7 PM** (evening peak)
* 📆 Friday and Saturday show **higher fare averages**
* 🌍 Ride density clusters in **downtown areas** (NYC zone)
* 📉 Most fares fall between **\$5 – \$20**
* 📏 Longest rides show proportionally higher fares, but outliers exist




# 🧠 Final Words of Wisdom

> “Data is the new oil, and dashboards are the refinery.”
> Let your dashboard speak louder than rows of numbers.

