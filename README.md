# 🚦 US Traffic Accidents Analysis (2016–2023)

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=flat-square&logo=pandas)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Viz-3F4F75?style=flat-square&logo=plotly)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

> **Internship Project** — An end-to-end exploratory data analysis of 7.7 million US traffic accidents, uncovering patterns in time, weather, geography, and road infrastructure.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Data Cleaning & Preprocessing](#-data-cleaning--preprocessing)
- [Feature Engineering](#-feature-engineering)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Key Insights & Summary Statistics](#-key-insights--summary-statistics)
- [Technologies Used](#-technologies-used)
- [How to Reproduce](#-how-to-reproduce)
- [Conclusion](#-conclusion)
- [Author & Acknowledgments](#-author--acknowledgments)

---

## 🔍 Project Overview

This project performs a comprehensive analysis of the **US Accidents dataset** — one of the largest publicly available traffic accident datasets — covering **7.7 million records** across **49 US states** from January 2016 to March 2023.

**Goals:**
- Identify temporal patterns (time of day, day of week, month, year)
- Analyze the impact of weather conditions on accident severity
- Examine the role of road infrastructure in accidents
- Visualize geographic hotspots across the United States
- Engineer meaningful features to deepen analytical insights

---

## 📦 Dataset

| Attribute       | Details                                                                 |
|----------------|-------------------------------------------------------------------------|
| **Source**      | [Kaggle – US Accidents by Sobhan Moosavi](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents) |
| **Size**        | 7,728,394 rows × 46 columns (~4 GB)                                    |
| **Time Period** | January 2016 – March 2023                                              |
| **Coverage**    | 49 US States                                                           |

> ⚠️ **Note:** The dataset is not included in this repository due to its large size (~4 GB). Please download it from Kaggle and follow the setup instructions below.

---

## 📁 Project Structure

```
us-traffic-accidents-analysis/
│
├── Accident.ipynb              # Main Jupyter Notebook (all code & analysis)
├── README.md                   # Project documentation (this file)
├── .gitignore                  # Excludes dataset and generated output files
│
├── outputs/                    # (Generated locally, not committed)
│   ├── 01_severity_distribution.png
│   ├── 02_missing_values.png
│   ├── 03_time_patterns.png
│   ├── 04_weather_analysis.png
│   ├── 05_infrastructure_analysis.png
│   ├── 06_correlation_heatmap.png
│   ├── 07_top_locations.png
│   ├── 08_duration_distribution.png
│   ├── 09_source_airport_analysis.png
│   ├── 10_wind_analysis.png
│   ├── 11_distance_vs_severity.png
│   └── 11_distance_vs_severity.png
```

---

## 🧹 Data Cleaning & Preprocessing

The raw dataset underwent rigorous cleaning before analysis:

- **Filtered** only essential columns from the 46-column dataset
- **Converted** `Start_Time`, `End_Time`, and `Weather_Timestamp` to datetime format
- **Dropped** rows with missing critical fields (`Start_Lat`, `Start_Lng`, `Start_Time`), reducing dataset to **6,985,228 clean records**
- **Removed** duplicate rows based on `ID` — none found
- **Imputed** missing numeric values (`Temperature`, `Humidity`, `Visibility`, `Wind_Speed`, `Precipitation`, `Wind_Chill`) with their respective **median** values
- **Filled** missing categorical values (`Weather_Condition`, `Wind_Direction`, `Airport_Code`, `Street`, `County`) with `'Unknown'`

---

## ⚙️ Feature Engineering

Several new features were derived to enrich the analysis:

| Feature          | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `Hour`           | Hour extracted from `Start_Time`                                           |
| `Day_of_Week`    | Day of week extracted from `Start_Time`                                    |
| `Month`          | Month extracted from `Start_Time`                                          |
| `Year`           | Year extracted from `Start_Time`                                           |
| `Weekday_Flag`   | `1` = Weekend, `0` = Weekday                                               |
| `Duration_Min`   | `End_Time − Start_Time` in minutes, capped at 0–1440 min                  |
| `Infra_Count`    | Sum of 13 boolean infrastructure flags (signals, junctions, crossings, etc.) |
| `Weather_Grouped`| Rare weather conditions grouped into `'Other'`                             |
| `Severity_Cat`   | Numeric severity (1–4) mapped to: Minor, Moderate, Serious, Severe         |

---

## 📊 Exploratory Data Analysis

A total of **13+ visualizations** were generated, including two interactive HTML maps.

---

### 1. 📈 Severity Distribution
**<img width="800" height="500" alt="01_severity_distribution" src="https://github.com/user-attachments/assets/94bd2868-4be2-46cd-ad80-9dec16679686" />
**
- Most accidents fall under **Severity 2 (Moderate)**
- **Severity 4 (Severe)** is the least common category

---

### 2. ❓ Missing Values
**<img width="1200" height="800" alt="02_missing_values" src="https://github.com/user-attachments/assets/c213fa92-fc43-4255-96a0-d0faf8d8c4cf" />
**
- `End_Lat`/`End_Lng` had ~3.4M missing values
- `Precipitation` had ~2.2M missing values
- Addressed through imputation and filtering strategies

---

### 3. ⏰ Time Patterns
**<img width="1500" height="1200" alt="03_time_patterns" src="https://github.com/user-attachments/assets/be4142ee-4c53-4fc1-94c5-cd59b6d07ee8" />
** *(4 subplots)*

- **By Hour:** Dual peaks at **7–9 AM** and **4–6 PM** (rush hours); lowest at 3–5 AM
- **By Day:** **Friday** has the most accidents; **Sunday** the least
- **By Month:** Peak in **summer (June–August)**; lowest in **February**
- **By Year:** Steady increase from 2016 to 2023 (improved data collection over time)

---

### 4. 🌦️ Weather Analysis
**<img width="1800" height="500" alt="04_weather_analysis" src="https://github.com/user-attachments/assets/064b6f8e-c6d3-47a3-ac1c-dc47a5f821bb" />
** *(3 subplots)*

- **Top Weather Conditions:** "Fair" is most common, followed by "Partly Cloudy" and "Cloudy"
- **Temperature vs Severity:** Higher severity tends to occur at **lower temperatures** (winter accidents more severe)
- **Visibility vs Severity:** **Lower visibility** correlates with higher accident severity

---

### 5. 🛣️ Infrastructure Analysis
**<img width="1400" height="500" alt="05_infrastructure_analysis" src="https://github.com/user-attachments/assets/39ed3827-f1e1-4c03-a68c-a0a9523c7df1" />
** *(2 subplots)*

- **Infrastructure Count vs Severity:** Slight negative correlation — more infrastructure = slightly lower severity (likely due to urban lower speeds)
- **Day vs Night:** ~65% of accidents occur during the day; however, **night accidents tend to be more severe**

---

### 6. 🔥 Correlation Heatmap
**<img width="1200" height="1000" alt="06_correlation_heatmap" src="https://github.com/user-attachments/assets/b0c59281-6489-4d45-87cd-4ec6b8194894" />
**

Key correlations with Severity:
- `Visibility`: **−0.12** (lower visibility → higher severity)
- `Temperature`: **−0.07**
- `Infra_Count`: **−0.12**
- `Duration` mildly correlates with `Distance` (0.08) and `Severity` (0.06)

---

### 7. 📍 Top Locations
**<img width="1800" height="600" alt="07_top_locations" src="https://github.com/user-attachments/assets/fea36ef4-c40c-43c6-acda-dc136ff7a3be" />
** *(3 bar charts)*

- **Top States:** California (1.57M), Texas, Florida
- **Top Counties:** Los Angeles, Harris
- **Top Streets:** Predominantly interstate highways (I-95, I-10, etc.)

---

### 8. ⏳ Accident Duration
**<img width="1200" height="500" alt="08_duration_distribution" src="https://github.com/user-attachments/assets/351ee4e6-3e4c-41e8-8637-0b1c0c0a1d10" />
**

- Right-skewed distribution; most accidents clear within **30–60 minutes**
- **Median duration:** 62.7 minutes | **Mean duration:** 111.5 minutes
- Severe accidents significantly pull up the average

---

### 9. ✈️ Source & Airport Analysis
**<img width="1200" height="500" alt="09_source_airport_analysis" src="https://github.com/user-attachments/assets/1b10f652-fc3f-4aa8-aa11-cac389a881fe" />
** *(2 subplots)*

- All data sources show similar average severity (~2.2)
- **Near airports:** Slightly higher severity (2.25 vs 2.21) — possibly due to higher speeds or unfamiliar rental drivers

---

### 10. 💨 Wind Analysis
**<img width="1400" height="500" alt="10_wind_analysis" src="https://github.com/user-attachments/assets/be4b5d33-4aa8-4ce2-86f3-808eb57bdd06" />
** *(2 subplots)*

- **Top Wind Directions in Severe Accidents:** Southwest and West
- **Wind Chill vs Severity:** Lower wind chill (colder conditions) → higher accident severity

---

### 11. 📏 Distance vs Severity
**<img width="1000" height="500" alt="11_distance_vs_severity" src="https://github.com/user-attachments/assets/5513bc8c-f259-46b3-a44d-a2cf63353460" />
**

- Higher severity accidents tend to **block greater road distances**
- Clear positive relationship between road impact and accident severity

---

---

## 📌 Key Insights & Summary Statistics

| Metric                         | Value                          |
|-------------------------------|-------------------------------|
| Total Accidents Analyzed       | 6,985,228                     |
| Date Range                     | 2016-01-14 to 2023-03-31      |
| States Covered                 | 49                            |
| Most Common Weather            | Fair                          |
| Peak Accident Hour             | 7:00 AM                       |
| Day with Most Accidents        | Friday                        |
| Most Dangerous State           | California (1,567,136)        |
| Most Dangerous County          | Los Angeles                   |
| Average Severity               | 2.23 / 4                      |
| Severe Accidents (Severity 3+4)| 21.2%                         |
| Average Duration               | 111.5 minutes                 |
| Median Duration                | 62.7 minutes                  |

---

## 🛠️ Technologies Used

| Tool / Library   | Purpose                              |
|-----------------|--------------------------------------|
| Python 3.8+      | Core programming language            |
| Pandas           | Data manipulation & cleaning         |
| NumPy            | Numerical computations               |
| Matplotlib       | Static visualizations                |
| Seaborn          | Statistical plots & heatmaps         |
| Jupyter Notebook | Interactive development environment  |

---

## ▶️ How to Reproduce

### 1. Clone the Repository
```bash
git clone https://github.com/Mehul5124/us-traffic-accidents-analysis.git
cd us-traffic-accidents-analysis
```

### 2. Download the Dataset
- Go to [Kaggle – US Accidents](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents)
- Download `US_Accidents_March23.csv` and rename it to `Accident_Dataset.csv`
- Place it in the **root folder** of the project

### 3. Install Dependencies
```bash
pip install pandas numpy matplotlib seaborn
```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook Accident.ipynb
```

### 5. Run All Cells
- All outputs (`.png` images and `.html` maps) will be generated automatically in the working directory.

---

## ✅ Conclusion

This analysis of 6.98 million US traffic accidents reveals several critical patterns:

- 🕐 **Rush hours (7–9 AM & 4–6 PM)** and **Fridays** are the highest-risk times
- ❄️ **Poor visibility, low temperatures, and cold wind chill** significantly increase accident severity
- 🏙️ **Urban infrastructure** (signals, crossings) shows a slight negative correlation with severity, likely due to lower urban speeds
- 📍 **California** — particularly **Los Angeles County** — is the most accident-prone region in the US
- ⏱️ Most accidents are **minor-to-moderate** and clear within an hour; however, severe accidents can last **2+ hours**, causing major traffic disruptions

---

## 👤 Author & Acknowledgments

**Author:** Mehul Balsara
**Role:** Data Science Intern
**GitHub:** [@Mehul5124](https://github.com/Mehul5124)

**Acknowledgments:**
- 📊 [Sobhan Moosavi](https://smoosavi.org/) — for creating and sharing the US Accidents dataset
- 🏆 [Kaggle](https://www.kaggle.com/) — for hosting the dataset
- 🐍 The open-source Python community — for the amazing libraries that made this analysis possible

---

*⭐ If you found this project useful, feel free to star the repository!*
