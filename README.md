# AQI India — Station-Level Pollution Intelligence Pipeline

This repository contains the local, fully-functional setup of the AQI India Station-Level Pollution Intelligence Pipeline. You can run this pipeline directly on your machine in VS Code as a Python script or an interactive Jupyter Notebook.

---

## 📁 Directory Structure

After running, the directory will look like this:

```text
d:\HACKATHONS\AQI INDIA\
├── data/                    # Raw dataset folder (automatically downloaded)
│   └── aqi_india.csv        # Station-level pollution readings dataset
├── outputs/                 # All generated charts, tables, and reports
│   ├── charts/              # Visual plots (hotspots, trends, etc.)
│   │   ├── geo_hotspots.png
│   │   ├── hourly_trend.png
│   │   ├── pollutant_counts.png
│   │   ├── pollutant_distribution.png
│   │   ├── pollution_clusters.png
│   │   ├── spis_risk_bands.png
│   │   └── risk_band_feature_importance.png
│   ├── tables/              # Cleaned CSV summaries, rankings, and clusters
│   │   ├── cleaned_dataset.csv
│   │   ├── city_summary.csv
│   │   ├── station_summary.csv
│   │   ├── anomalies.csv
│   │   ├── spis_risk_scores.csv
│   │   └── city_pollution_clusters.csv
│   └── insights_summary.txt # General text summary report
├── pipeline.py              # Pure Python script version of the pipeline
├── pipeline.ipynb           # Interactive Jupyter Notebook (VS Code ready)
├── dashboard.py             # Interactive local Streamlit Web UI App
├── requirements.txt         # Required Python packages list
└── README.md                # Setup & instruction guide (This file)
```

---

## 🚀 Setup & Run Instructions

Follow these simple steps to run the project locally on your machine:

### 1. Open Workspace in VS Code
Open VS Code, click **File** -> **Open Folder**, and select:
`d:\HACKATHONS\AQI INDIA`

### 2. Create a Virtual Environment (Recommended)
Open a terminal in VS Code (Ctrl + ` or **Terminal** -> **New Terminal**) and run:
```powershell
python -m venv venv
```

### 3. Activate the Virtual Environment
Depending on your shell, run:
* **PowerShell**:
  ```powershell
  .\venv\Scripts\Activate.ps1
  ```
  *(Note: If you get a policy error, run `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process` first)*
* **Command Prompt (CMD)**:
  ```cmd
  .\venv\Scripts\activate.bat
  ```

### 4. Install Dependencies
Run the following command to install the required libraries:
```powershell
pip install -r requirements.txt
```

### 5. Run the Pipeline

You have two ways to run the pipeline:

#### **Method A: Run as a Python Script (Fastest)**
Simply execute this command in your terminal:
```powershell
python pipeline.py
```
This will automatically:
1. Download the Kaggle dataset to `data/aqi_india.csv` using `kagglehub`.
2. Process the data, clean it, and train the ML models.
3. Save all outputs, plots, and summaries in the `outputs/` folder.

#### **Method B: Run Interactively in VS Code (Recommended for analysis)**
1. Open the [pipeline.ipynb](file:///d:/HACKATHONS/AQI%20INDIA/pipeline.ipynb) file inside VS Code.
2. If prompted, select your Python virtual environment kernel (`venv`) in the top-right corner.
3. Run cells one-by-one by clicking the play button next to them, or click **Run All** at the top.

#### **Method C: Run as a local Streamlit Web App Dashboard (Interactive GUI)**
Simply execute this command in your terminal:
```powershell
streamlit run dashboard.py
```
This will launch a beautiful browser window containing interactive maps, custom state/city filtering, and 24-hour predictive trend graphs.


---

## 🧠 Key Features Implemented

1. **Auto-Download:** Uses `kagglehub` to fetch public Kaggle datasets anonymously without requiring API keys or login.
2. **Schema & Cleaning:** Filters out invalid geographical coordinates and missing average values.
3. **Anomaly Flagging:** Uses robust statistical IQR to flag outlier values per pollutant type.
4. **SPIS Scoring (Station Pollution Intelligence Score):** Calculates a 0-100 composite index combining average concentration, variance spread, anomaly rates, and reading persistence.
5. **Pollutant-Signature Clustering:** Uses K-Means to cluster cities based on their multi-pollutant fingerprint.
6. **Risk-Band ML Classifier:** Trains a Random Forest Classifier to assess and rank feature drivers.
