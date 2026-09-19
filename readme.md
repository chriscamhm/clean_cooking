# Classification models to identify main cooking fuel source in Colombia

## Overview
This repository contains the codebase used to evaluate and predict the primary cooking fuel sources of Colombian households. Despite widespread access to electricity (94.92%) and natural gas (68%), a significant portion of the population continues to rely on transitional or polluting fuels like firewood. 

The goal of this project is to use machine learning classification models to identify the characteristics of households that primarily use off-grid or polluting sources for cooking, despite having access to modern energy grids. 

For the complete study, theoretical background, and in-depth exploratory data analysis, please refer to the detailed document: **PTNY8.pdf**.

## Dataset
The data is sourced from the **Colombian Living Standards Survey (CLSS) of 2023**, conducted by the National Statistics Department (DANE). 

### Data Preprocessing
*   **Filtering:** Households without access to either electricity or natural gas were excluded to focus strictly on users making a choice despite grid access. Missing values and specific outliers (e.g., `999` in `green_access`) were dropped, resulting in a final dataset of 79,439 households.
*   **Target Variable (`energy_cook`):** Categorized into three main classes based on WHO guidelines:
    1.  **Clean Fuels (CF):** Electricity, Gas
    2.  **Clean Fuels Off-Grid (LPG):** Liquefied Petroleum Gas
    3.  **Transitional/Polluting Fuels (PF):** Oil, Coal, Firewood, Waste material
*   **Features:** Includes socioeconomic status (SES), education level, property rights, house type, urban/rural residency, household size, age, access to public services (water, sewage, garbage), and appliance ownership (stove, fridge).

## Methodology
The numerical variables were normalized using the z-score method, and categorical variables were transformed using one-hot encoding. The dataset was split into training (70%) and testing (30%) sets.

Four multilabel classification models were trained and tuned using GridSearch Cross-Validation:
1.  **Multinomial Logistic Regression (MLG)**
2.  **Random Forest (RF)**
3.  **Extreme Gradient Boosting (XGB)**
4.  **Support Vector Machines (SVM)**

## Key Results
*   **Model Performance:** All models performed similarly with no signs of overfitting. The **SVM model** achieved the highest accuracy on the test set (**74.0%**), while MLG had the lowest (72.5%).
*   **Class Prediction:** All models accurately predicted the Clean Fuels (CF) category but struggled to distinguish between the LPG and Polluting Fuels (PF) categories. This is likely due to overlapping characteristics among middle-income urban households and lower-income rural households.
*   **Feature Importance:** Evaluated via the SVM model, the most critical features for prediction were:
    1.  Access to sewage (public service)
    2.  Possession of a stove
    3.  Access to public water
    4.  Urban residency
*   **Conclusion:** Surprisingly, Socioeconomic Status (SES) and education levels were the *lowest* contributors to the model's predictions. The results emphasize that mere connection to an energy grid is insufficient; structural factors like urban infrastructure, public services, and appliance ownership (stoves) are the primary drivers in the transition to clean cooking.
