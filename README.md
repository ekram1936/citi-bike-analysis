# Citi Bike NYC Analysis and Ride Demand Prediction

<figure>
    <img src="image/citi-bike.png" style="width:100%">
</figure>
This Challenge focuses on analyzing the **Citi Bike NYC** data to uncover patterns in bike usage and predict ride demand using various machine learning models. Through data analysis, we also answer several key business questions that can help improve Citi Bike's operations, optimize their fleet distribution, and enhance customer satisfaction.

## Challenge Overview

The primary objectives of this challenge are to:

- Pay attention to seasonality, member types, bike types, and locations as key factors that influence the business
- Don’t spread yourself too thin, and explore many hypotheses. Be targeted.
- Demonstrate the use of at least 1 advanced analytical technique in Statistics or Machine Learning
- Be sure to highlight the technical challenges of processing the data
- Give concrete recommendations. It should follow implicitly or explicitly that the recommendations would not have been possible without analyzing the data

---

## Table of Contents

- [Challenge Overview](#project-overview)
- [Business Questions Addressed](#business-questions-addressed)
- [Predictive Modeling](#predictive-modeling)
- [Key Recommendations](#key-recommendations)
- [Installation](#installation)
- [Usage](#usage)
- [References](#references)

---

## Business Questions Addressed

#### 1. **What are the peak demand times for bike rentals?**

- Peak demand occurs during **morning and evening rush hours** on weekdays, with a similar trend on weekends, especially for electric bikes.

#### 2. **How does ride demand vary day by day and week by week?**

- **Tuesday and Wednesday** have the highest number of rides, closely followed by **Monday**. **Thursday and Friday** show a decline in ride frequency compared to the first three days of the week.The number of rides is comparatively lower on **Saturday and Sunday**, which could indicate a reduction in demand during weekends.

#### 3. **Which stations have the highest and lowest inflows and outflows of bikes?**

- Stations like **Hoboken Terminal (River St & Hudson Pl)** and **Grove St PATH** are high-demand stations for both inflows and outflows.

#### 4. **How do ride patterns differ between casual users and members?**

- **Members prefer electric bikes**, while **casual users tend to use classic bikes** more frequently, especially on weekends.

#### 5. **What are the most popular routes for members vs. casual users?**

- **Members** tend to have fixed routes connecting **business districts**, while **casual users** favor scenic and leisure-friendly routes.

#### 6. **How does bike type usage vary by time of day (weekdays vs. weekends)?**

- **Electric bikes** are more popular during peak hours and weekdays, while classic bikes are used more evenly across weekends.

#### 7. **How should bike allocation be optimized between classic and electric bikes?**

- High-demand stations, such as **Grove St PATH**, should prioritize **electric bikes**, while stations with higher casual usage should have **more classic bikes**.

---

## Predictive Modeling

---

### Features and Target

This section provides an overview of the **features** (input columns) used to train the model and the **target column** that the model is predicting.

#### **Features (Input Columns):**

| Column Name              | Description                                                                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **time_segment_encoded** | Encoded categorical variable representing the time segment of the day (e.g., morning, afternoon, evening). It is one of the most important features in the prediction model. |
| **hour**                 | Represents the hour of the day (0-23). Significant in determining ride demand fluctuations across different hours.                                                           |
| **day_type_encoded**     | Encoded categorical variable that indicates whether the day is a weekday or weekend. This affects commuting vs. leisure usage patterns.                                      |
| **month**                | Numeric feature representing the month (1-12), which helps capture seasonal variations in ride demand.                                                                       |
| **day_of_week_encoded**  | Encoded categorical variable representing the day of the week (e.g., Monday, Tuesday). Important for identifying trends like higher demand during weekdays.                  |
| **season_encoded**       | Encoded categorical variable representing the season (e.g., winter, summer). This helps capture broader seasonal variations in bike usage.                                   |

#### **Target Column (Output):**

| Column Name    | Description                                                                                                               |
| -------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **ride_count** | The number of rides (demand) for a given hour, day, and location. This is the value that the model is trained to predict. |

---

### Example Data:

| time_segment | hour | day_type | month | day_of_week | season | ride_count |
| ------------ | ---- | -------- | ----- | ----------- | ------ | ---------- |
| Night        | 12   | Weekday  | 7     | Monday      | Winter | 69         |
| Evening      | 19   | Weekend  | 5     | Saturday    | Summer | 199        |

---

#### Models Used:

- **Ridge Regression**
- **Lasso Regression**
- **ElasticNet**
- **Random Forest Regressor**
- **Gradient Boosting Regressor**
- **XGBoost Regressor**

### Algorithm Performance Comparison

| Algorithm            | Train RMSE | Train R² | Train MAE | Test RMSE | Test R² | Test MAE | Training Time (s) |
| -------------------- | ---------- | -------- | --------- | --------- | ------- | -------- | ----------------- |
| **Ridge**            | 0.7319     | 0.4643   | 0.5444    | 0.7646    | 0.4380  | 0.5710   | 0.0951            |
| **Lasso**            | 0.7323     | 0.4637   | 0.5441    | 0.7635    | 0.4396  | 0.5688   | 0.0940            |
| **ElasticNet**       | 0.7320     | 0.4642   | 0.5443    | 0.7643    | 0.4383  | 0.5704   | 0.2193            |
| **Random Forest**    | 0.3296     | 0.8914   | 0.2050    | 0.3818    | 0.8598  | 0.2455   | 135.8315          |
| **GradientBoosting** | 0.3457     | 0.8805   | 0.2200    | 0.3776    | 0.8629  | 0.2443   | 84.1148           |
| **XGBoost**          | 0.3391     | 0.8850   | 0.2119    | 0.3749    | 0.8649  | 0.2405   | 19.2470           |

### Summary of Performance:

- The **XGBoost** algorithm performs the best with the lowest **Test RMSE** (0.3749) and the highest **Test R²** (0.8649), while also having a relatively low training time compared to **Random Forest**.
- **Random Forest** and **Gradient Boosting** also perform well with similar **Test R²** scores, but take much longer to train.
- **Ridge**, **Lasso**, and **ElasticNet** show similar results with lower accuracy compared to the tree-based models.

---

### Feature Importance from XGBoost Model

The XGBoost model was used to predict Citi Bike ride demand. Below is the feature importance ranking derived from the model. These features provide insight into the most important factors influencing ride demand.

#### **Feature Importance Table:**

| Feature                  | Importance |
| ------------------------ | ---------- |
| **time_segment_encoded** | 0.532174   |
| **hour**                 | 0.225450   |
| **day_type_encoded**     | 0.132463   |
| **month**                | 0.091806   |
| **day_of_week_encoded**  | 0.013760   |
| **season_encoded**       | 0.004348   |

---

## Key Recommendations

#### 1. **Expand Fleet and Stations in High-Demand Areas**

- Stations like **Hoboken Terminal** and **Grove St PATH** should have **more electric bikes** to meet the growing demand.

#### 2. **Launch Seasonal Promotions and Incentives**

- Introduce **seasonal campaigns** during high-demand months and targeted promotions for weekends to boost usage.

#### 3. **Implement Dynamic Pricing**

- Use **dynamic pricing** during peak demand hours (morning and evening) to manage demand and increase revenue.

#### 4. **Right-Size the Fleet Based on Demand**

- **Reduce the number of bikes** at low-demand stations and increase availability at high-demand stations.

#### 5. **Targeted Maintenance Scheduling**

- Prioritize **electric bikes** for maintenance as they have higher usage, ensuring minimal downtime during peak hours.

#### 6. **Increase Membership Conversions**

- Provide **membership incentives** for casual users, offering them benefits like discounted electric bike rides on weekends.

---

## Installation

To run the project, you need to have the following dependencies installed:

- Python 3.x
- Jupyter Notebook
- Scikit-learn
- Pandas
- Matplotlib
- XGBoost
- SHAP

#### Clone the Repository

```bash
git clone https://github.com/your_username/Citi_Bike_NYC_Ride_Demand_Prediction.git
cd Citi_Bike_NYC_Ride_Demand_Prediction
```

---

## Usage

To run the analysis and predictions, open the provided Jupyter Notebook in the repository.

```bash
jupyter notebook Citi_Bike_NYC_Analysis.ipynb
```

---

## References

- [Citi Bike NYC Open Data](https://www.citibikenyc.com/system-data)
- [XGBoost Documentation](https://xgboost.readthedocs.io/)
- [SHAP Documentation](https://shap.readthedocs.io/en/latest/)

---
