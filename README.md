# Google Pixel Watch - Eating Detection Dataset

This repository contains sensor data collected from Google Pixel Watch devices for eating activity detection and classification.

## Dataset Overview

The dataset includes **raw sensor measurements**, **extracted features**, and **ML model predictions** for eating behavior detection using wearable sensors.

**Period**: July - September 2024  
**Device**: Google Pixel Watch  
**Purpose**: Eating vs. Non-eating activity classification

## Repository Structure

### 1. Features (`features/`)

Extracted features and ML model predictions from processed sensor data.

**File**: `features.json`

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
    "predictionProb": {
      "random_forest_classifier": 0.681,
      "gradient_boosting_classifier": 0.810,
      ...
    }
  }
}
```

### 2. Raw Pixel Data (`raw_pixel_data/`)

Time-series sensor measurements from Google Pixel Watch accelerometer and gyroscope.

**File naming**: `{month}_test_id_{id}.json.gz`

- Compressed JSON files (gzip)
- Organized by month and subject ID
- Files split into parts when >100MB (e.g., `_part_1.json.gz`, `_part_2.json.gz`)

**Data fields**:
- `timestamp`: Measurement timestamp
- `test_id`: Subject identifier
- `values`: Sensor readings (accelerometer, gyroscope, heart_rate, battery)
- `connectionType`: WiFi/Cellular
- `signal_strength`: Connection quality
- `_id`: MongoDB document ID
- `timestamp_send`: When data was sent from device
- `timestamp_kafka_source`: Kafka source timestamp
- `timestamp_kafka_sink`: Kafka sink timestamp

**Months**:
- `july_*`: July 2024
- `august_*`: August 2024  
- `september_*`: September 2024

**Sample structure**:
```json
[
  {
    "timestamp": "2024-08-28 16:19:12.240000",
    "test_id": 103,
    "signal_strength": 0,
    "connectionType": "WiFi",
    "_id": "66cf4e12abf78441838c34ce",
    "values": {"heart_rate": 81.0},
    "timestamp_send": "2024-08-28 16:19:28.993000",
    "recovered": false,
    "signal_type": "None",
    "timestamp_kafka_source": "2024-08-28 16:19:29.887000",
    "timestamp_kafka_sink": "2024-08-28 16:19:30.060000"
  },
  {
    "timestamp": "2024-08-28 16:19:12.260000",
    "test_id": 103,
    "signal_strength": 0,
    "connectionType": "WiFi",
    "_id": "66cf4e12abf78441838c34d0",
    "values": {
      "accel_y": -0.544988,
      "accel_z": 9.081536,
      "accel_x": 3.5034943
    },
    "timestamp_send": "2024-08-28 16:19:28.993000",
    "recovered": false,
    "signal_type": "None",
    "timestamp_kafka_source": "2024-08-28 16:19:29.887000",
    "timestamp_kafka_sink": "2024-08-28 16:19:30.060000"
  },
  {
    "timestamp": "2024-08-28 16:19:12.260000",
    "test_id": 103,
    "signal_strength": 0,
    "connectionType": "WiFi",
    "_id": "66cf4e12abf78441838c34d1",
    "values": {
      "gyro_y": 0.0027488936,
      "gyro_x": -0.004886922,
      "gyro_z": 0.014660766
    },
    "timestamp_send": "2024-08-28 16:19:28.993000",
    "recovered": false,
    "signal_type": "None",
    "timestamp_kafka_source": "2024-08-28 16:19:29.887000",
    "timestamp_kafka_sink": "2024-08-28 16:19:30.060000"
  }
]
```

## Notes

- **Large files** have been split into multiple parts (`_part_1`, `_part_2`, etc.) to comply with GitHub's 100MB file size limit
- All timestamps are in UTC
- Test IDs are anonymized subject identifiers
- Negative test IDs indicate preliminary/testing data
- Data is compressed using gzip to reduce storage size
- Each sensor reading is stored as a separate JSON object in the array
- Accelerometer values are in m/s²
- Gyroscope values are in rad/s

## Contact

For questions or issues, please contact: marodriguezf@uc.cl
