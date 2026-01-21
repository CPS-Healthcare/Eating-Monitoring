# Google Pixel Watch - Eating Detection Dataset

This repository contains sensor data collected from Google Pixel Watch devices for eating activity detection and classification.

## Dataset Overview

The dataset includes **raw sensor measurements**, **extracted features**, and **ML model predictions** for eating behavior detection using wearable sensors.

**Period**: July - September 2024  
**Device**: Google Pixel Watch  
**Purpose**: Eating vs. Non-eating activity classification

## Repository Structure

### 1. Raw Sensor Data (`pixel_watch_data_2024/`)

Time-series sensor measurements from Google Pixel Watch accelerometer and gyroscope.

**File naming**: `{month}_test_id_{id}.json.gz`

- Compressed JSON files (gzip)
- Organized by month and subject ID
- Files split into parts when >100MB (e.g., `_parte_1.json.gz`, `_parte_2.json.gz`)

**Data fields**:
- `timestamp`: Measurement timestamp
- `test_id`: Subject identifier
- `values`: Sensor readings (accelerometer, gyroscope, battery, etc.)
- `connectionType`: WiFi/Cellular
- `signal_strength`: Connection quality

**Months**:
- `julio_*`: July 2024
- `agosto_*`: August 2024  
- `septiembre_*`: September 2024

### 2. ML Model Predictions (`cloudresults_all.json`)

Machine Learning classification results with features and predictions.

**File**: `cloudresults_all.json` (8.99 MB, 2,082 records)

**Content**:
- **85 extracted features** per window (acceleration/gyroscope statistics)
- **4 ML model predictions**:
  - Random Forest Classifier
  - Gradient Boosting Classifier
  - Bagging Classifier
  - XGBoost Classifier
- Prediction probabilities
- Execution times

**Sample structure**:
```json
{
  "test_id": 1000,
  "timestamp": "2024-09-05 16:45:06.463000",
  "values": {
    "features": {
      "az_med_min": 5.385,
      "ax_med_max": 5.842,
      "ay_med_mean": -2.560,
      ...
    },
    "prediction": {
      "random_forest_classifier": 1,
      "gradient_boosting_classifier": 1,
      "bagging_classifier": 0,
      "xgboost_classifier": 0
    },
    "predicionProb": {
      "random_forest_classifier": 0.681,
      "gradient_boosting_classifier": 0.810,
      ...
    }
  }
}
```

## Notes

- **Large files** have been split into multiple parts (`_parte_1`, `_parte_2`, etc.) to comply with GitHub's 100MB file size limit
- All timestamps are in UTC
- Test IDs are anonymized subject identifiers
- Negative test IDs indicate preliminary/testing data
- Data is compressed using gzip to reduce storage size

## Contact

For questions or issues, please contact: marodriguezf@uc.cl
