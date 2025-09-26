# Used Bike Price Prediction

## Overview

This project predicts the price of used bikes in India based on their specifications and features using machine learning. It covers:

- Data cleaning and preprocessing of messy datasets
- Feature engineering to create meaningful predictors
- ML model training and evaluation
- Prediction for new bike listings

Models included:

- **Linear Regression**
- **Random Forest Regressor**
- **Gradient Boosting Regressor**

---

## Dataset

The dataset contains information about used bikes, including:

| Column Name   | Description                                      |
|---------------|--------------------------------------------------|
| model_name    | Full name of the bike including brand & model   |
| model_year    | Year the bike was manufactured                   |
| kms_driven    | Distance traveled in kilometers                 |
| owner         | Ownership status (first owner, second owner, etc.) |
| location      | City or region of sale                           |
| mileage       | Mileage of the bike (kmpl)                      |
| power         | Power output of the bike (bhp)                  |
| price         | Price of the bike (INR)                          |

---

## Features Engineering

Features created for machine learning:

1. **engine_cc**: Engine capacity extracted from the model name  
2. **brand**: Bike brand extracted from the model name  
3. **bike_age**: Current year minus model year  
4. **power_to_cc**: Ratio of power to engine capacity  
5. **price_log**: Log-transformed price to reduce skewness  

---

## Data Cleaning

- Remove duplicates and reset index  
- Extract numeric values from messy text in `kms_driven`, `mileage`, `power`  
- Fill missing values in numeric columns with median  
- Fill missing values in categorical columns with `"Unknown"`  

---

## Preprocessing

- Numeric columns scaled using **StandardScaler**  
- Categorical columns encoded using **OneHotEncoder**  
- Preprocessing applied via a **ColumnTransformer** inside a **Pipeline** with the model  

---

## Model Training & Evaluation

- Train-test split: 80% training, 20% testing  
- Models trained: Linear Regression, Random Forest, Gradient Boosting  
- Evaluation metrics:
  - Mean Absolute Error (MAE)
  - Root Mean Squared Error (RMSE)
  - R² Score  

---

## Usage

1. **Clone the repository**  
```bash
git clone <repo-url>
cd used-bike-price-prediction
````

2. **Create and activate a virtual environment** (optional but recommended)

```bash
# Create virtual environment
python -m venv .venv

# Activate
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```


3. **Run the notebook or script**

```bash
jupyter notebook
# or
python bikes.py
```

4. **Predict on new data**

```python
new_bike = pd.DataFrame({
    'engine_cc': [150],
    'power': [15],
    'mileage': [40],
    'bike_age': [3],
    'power_to_cc': [15/150],
    'location': ['bangalore'],
    'brand': ['Honda']
})

predicted_log_price = pipeline.predict(new_bike)[0]
predicted_price = np.expm1(predicted_log_price)
print("Predicted Price:", predicted_price)
```

---

## Dependencies

* Python 3.10+
* pandas
* numpy
* scikit-learn
* matplotlib (optional, for visualizations)

## Project Structure

```
used-bike-price-prediction/
│
├── bikes.csv                  # Dataset
├── bikes.py     # Full pipeline script
└── README.md                  # Project overview

---

## Results

After training, model evaluation metrics can be summarized:

| Model             |    MAE   |   RMSE   |    R²    |
| ----------------- | -------  | -------- | -------- |
| Linear Regression | 0.303860 | 0.849255 | 0.485753 |
| Random Forest     | 0.239711 | 0.846569 | 0.489001 |
| Gradient Boosting | 0.250429 | 0.818104 | 0.522788 |
