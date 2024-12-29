# Formula 1 Racing Analytics

This repository contains two complementary projects analysing Formula 1 racing data from the 2023 season.

- Project 1: F1 Lap Time Prediction
- Project 2: Driver Style Analysis (Verstappen vs. Norris)

## Requirements

- R
  - Required packages:
    - `openxlsx`
    - `dplyr`
    - `plotly`
    - `knitr` (for RMarkdown)
- python >= 3.8
  - Required packages:
    - `fastf1`
    - `pandas`
    - `numpy`
    - `scikit-learn`

## Usage

1. Execute the `dataPipeline.py` file to create the necessary directories, accumulate, pre-process and store the required data.
2. Run the `Lap-Time Model Comparison.ipynb` file to generate the complete analysis for Project 1.
3. Run the `Driving Style Comparison.Rmd` file to generate the complete analysis for Project 2.

## Project Structure

```text
├── F1 TELEMETRY ANALYSIS/         # Root project directory
    ├── __pycache__/              # Python bytecode cache
    ├── .git/                     # Git repository data
    ├── .vscode/                  # VS Code configuration
    ├── Cache/                    # Temporary data storage
    ├── Data/                     # Raw and processed F1 data
    ├── helpers/                  # Core functionality modules
    │   ├── __pycache__/
    │   ├── dataCollection/       # F1 data collection modules
    │   │   ├── __pycache__/
    │   │   ├── driverMetrics.py  # Driver performance data collection
    │   │   ├── raceCalendar.py   # Race schedule handling
    │   │   ├── raceTelemetry.py  # Race telemetry data collection
    │   │   ├── trackGeometry.py  # Track characteristics analysis
    │   │   └── trackWeather.py   # Weather data collection
    │   ├── dataPreprocessing.py  # Data preprocessing functions
    │   ├── initialization.py     # Setup and initialization code
    │   ├── misc.py              # Miscellaneous utility functions
    │   └── modelComparison.py   # Model evaluation utilities
    ├── Presentation/            # Project presentation materials
    ├── scripts/                 # Execution scripts
    │   ├── .gitignore
    │   ├── dataPipeline.py     # Main data processing pipeline
    │   └── Driving Style Comparison.Rmd  # R Markdown analysis
    ├── Lap-Time Model Comparison.ipynb    # Jupyter notebook for lap time analysis
    └── README.md               # Project documentation
```

### Key Components

#### Data Collection Modules

- `driverMetrics.py`: Collects and processes driver performance statistics
- `raceCalendar.py`: Handles F1 race schedule and event information
- `raceTelemetry.py`: Gathers real-time race telemetry data
- `trackGeometry.py`: Analyses track characteristics and layout
- `trackWeather.py`: Collects weather conditions data

#### Processing and Analysis

- `dataPreprocessing.py`: Data cleaning and preparation functions
- `Lap-Time Model Comparison.ipynb`: Main analysis of lap time predictions
- `Driving Style Comparison.Rmd`: Statistical analysis of driving styles

#### Pipeline and Utilities

- `dataPipeline.py`: Orchestrates the entire data processing workflow
- `initialization.py`: Project setup and configuration
- `modelComparison.py`: Functions for comparing prediction models
- `misc.py`: Helper functions used throughout the project

#### Documentation and Presentation

- `Reports/`: Project reports and visualization materials
- `README.md`: Comprehensive project documentation

---

## Project 1: F1 Lap Time Prediction

A machine learning approach to predict Formula 1 lap times using various models and comprehensive race data.

> Data was taken from the FastF1 library, for each driver and each race in the 2023 season. Laps where there was an incident on track were not included.

### Data Collection Infrastructure

#### Core Modules

1. **`RaceCalendar` Module**
   - Retrieves official F1 race schedules
   - Extracts event details (round number, event name, location, date)

2. **`TrackGeometryAnalyzer` Module**
   - Track length calculation
   - Elevation profile analysis
     - Maximum/minimum elevation
     - Total elevation change
     - Elevation standard deviation
   - Track curvature assessment
     - Corner count
     - Total/maximum curvature
     - Standard deviation

3. **`TrackWeatherAnalyzer` Module**
   - Air and track temperature
   - Rainfall data
   - Humidity-wind interaction
   - Wind chill factor
   - Surface grip index

4. **`DriverMetrics` Module**
   - Points before current event
   - Best lap times and deltas
   - Qualifying position
   - Sector-wise lap times
   - Tire compound data

5. **`RaceTelemetry` Module**
   - Lap start times
   - Lap times
   - Tire information
   - Sector times
   - Track status

### Model Implementation

#### 1. Linear Regression

- Baseline model
- Performance metrics:
  - Mean Absolute Error: 3.9319
  - R² Score: 0.7397

#### 2. Decision Tree Regressor

- Best performing model
- Hyperparameters:
  - `max_depth`: 20
  - `min_samples_split`: 2
  - `min_samples_leaf`: 10
- Performance metrics:
  - Mean Absolute Error: 0.9487
  - R² Score: 0.9478

#### 3. Random Forest Regressor

- Ensemble approach
- Hyperparameters:
  - `n_estimators`: 100
  - `max_depth`: 15
  - `min_samples_split`: 20
  - `min_samples_leaf`: 100
- Performance metrics:
  - Mean Absolute Error: 1.6796
  - R² Score: 0.8922

### Feature Importance

Top 5 most influential features:

1. Track Length (56.40%)
2. Elevation Standard Deviation (14.58%)
3. Total Elevation Change (6.23%)
4. Curvature Standard Deviation (5.17%)
5. Number of Corners (4.16%)

---

## Project 2: Driver Style Analysis (Verstappen vs. Norris)

A statistical comparison between Max Verstappen and Lando Norris using multiple linear regression models to analyse their driving styles and performance characteristics.

### Methodology

- Multiple linear regression models for each driver
- Two-sample testing for coefficient comparison
- Residual analysis
- Feature significance testing

### Data Processing

- Filtered for dry-weather laps
- Stratified sampling across tracks
- One-hot encoding for categorical variables
- Interaction terms for compound-specific tire effects

### Key Findings

#### Model Performance

- Verstappen Model:
  - Adjusted R²: 0.8901
  - Significant predictors: 16 variables
  
- Norris Model:
  - Adjusted R²: 0.8836
  - Significant predictors: 13 variables

#### Significant Style Differences

1. **Track Complexity Management**
   - Verstappen shows more consistent performance on complex tracks
   - Lower sensitivity to number of corners and maximum curvature
   - More efficient adaptation to track characteristics

2. **Tire Management**
   - Verstappen demonstrates superior tire management
   - Lower lap time degradation with tire wear
   - More consistent performance across tire compounds

3. **Performance Factors**
   - Different sensitivity to track temperature
   - Varying responses to humidity-wind interactions
   - Distinct patterns in point progression impact

---

## Author Information

Siddhant Shah  
Email: `siddshah@bu.edu`
Institution: Boston University

## Acknowledgments

- FastF1 library developers
- Formula 1 for data access
- Boston University CS Department
