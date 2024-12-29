# Beer Rating Prediction

This project predicts the overall rating of beers based on various characteristics, such as beer attributes, review aspects, and user information. By analyzing these factors, the model aims to help understand what influences beer ratings the most.

## Table of Contents

- [Project Objective](#project-objective)
- [Dataset Description](#dataset-description)
- [Installation and Requirements](#installation-and-requirements)
- [Project Workflow](#project-workflow)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Results](#results)
- [File Structure](#file-structure)
- [Contributing](#contributing)

## Project Objective

The primary goal of this project is to build a machine learning model that can accurately predict the **overall rating** of a beer based on a set of features, including beer properties, review ratings, and user demographics. This helps identify the key factors that contribute to high ratings and can assist breweries in understanding consumer preferences.

## Dataset Description

The dataset consists of multiple columns that describe the beer, the user, and the review details. The most relevant columns for our analysis include:

- **Beer Attributes**:
  - `beer/ABV`: Alcohol by volume of the beer.
  - `beer/style`: Style of the beer.
  
- **Review Aspects**:
  - `review/appearance`, `review/aroma`, `review/palate`, `review/taste`: Ratings (1.0 to 5.0) for each aspect of the beer.
  - `review/text`: The written review, which will be processed with natural language processing (NLP) techniques.
  - `review/overall`: The overall rating for the beer, which is the target variable for prediction.

- **User Information**:
  - `user/ageInSeconds`: User's age at the time of the review, recorded in seconds.
  - `user/gender`: Gender of the user, if specified.

### Target Variable

The target variable is `review/overall`, representing the beer’s overall rating (on a scale of 1.0 to 5.0).

## Installation and Requirements

To run this project, ensure that Python and the necessary libraries are installed.

1. **Clone the repository**:
   ```bash
   git clone https://github.com/subhajyoti007/beer-rating-prediction.git
   cd beer-rating-prediction
   ```

2. **Install dependencies**:
   Install the required packages listed in `requirements.txt`.
   ```bash
   pip install -r requirements.txt
   ```

## Project Workflow

1. **Data Loading and Initial Exploration**:
   - Load the `train.csv` file and examine the data structure, missing values, and data types.
   
2. **Data Cleaning**:
   - Drop rows where the target variable (`review/overall`) is missing.
   - Fill missing values for numeric fields, such as `beer/ABV` and review scores (e.g., `review/appearance`).
   - Convert `user/ageInSeconds` to `user_age` in years for easier analysis.

3. **Feature Engineering**:
   - **Text Processing**: Use TF-IDF (Term Frequency-Inverse Document Frequency) to process the `review/text` field and extract meaningful keywords.
   - **One-Hot Encoding**: Transform categorical fields such as `beer/style` and `user/gender` into numeric form using one-hot encoding.

4. **Model Training**:
   - Split the data into training and testing sets.
   - Use `RandomForestRegressor` for prediction, applying `GridSearchCV` to optimize hyperparameters (e.g., `n_estimators`, `max_depth`).
   
5. **Model Evaluation**:
   - Use evaluation metrics like RMSE (Root Mean Squared Error) and MAE (Mean Absolute Error) to measure the model's performance.
   - Display the feature importance plot to highlight which attributes contribute most to predicting the overall rating.

## Model Training and Evaluation

### Model Training
The `RandomForestRegressor` model was chosen for this project due to its ability to handle complex datasets and its resistance to overfitting. The hyperparameters are optimized using a grid search over a range of values:

- `n_estimators`: Number of trees in the forest.
- `max_depth`: Maximum depth of the tree.
- `min_samples_split` and `min_samples_leaf`: Minimum samples required for splits and leaf nodes.

### Evaluation Metrics

- **Root Mean Squared Error (RMSE)**: Evaluates the standard deviation of residuals, showing how far predictions deviate from actual values.
- **Mean Absolute Error (MAE)**: Measures the average magnitude of errors in predictions.

After training, the model displays both RMSE and MAE values to give a clear view of its performance.

### Feature Importance

The model’s feature importance plot identifies the top features influencing the overall rating. These insights can help breweries and analysts understand key rating factors and user preferences.

## Results

After tuning and training, the model's performance is assessed using the test dataset. The RMSE and MAE scores provide a quantitative understanding of its accuracy, while the feature importance plot reveals the primary factors contributing to the predictions.

Key features influencing beer ratings include:
- Ratings for **appearance**, **aroma**, **taste**, and **palate**.
- Specific **keywords** extracted from `review/text`.
- Beer attributes such as **ABV** and **style**.

## File Structure

```plaintext
beer-rating-prediction/
├── data/
│   └── train.csv               # Dataset file with beer reviews
├── main.py                     # Main script for data processing, model training, and evaluation
├── requirements.txt            # List of required Python packages
└── README.md                   # Project description and instructions
```

## Contributing

Contributions are welcome! To contribute:
1. **Fork the repository**.
2. **Create a new branch**: `git checkout -b feature/YourFeature`.
3. **Commit your changes**: `git commit -m 'Add your feature'`.
4. **Push to the branch**: `git push origin feature/YourFeature`.
5. **Open a pull request**.
