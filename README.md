# Chicago-Crime-Analysis
# Analyzing Crime Trends in Chicago

### Team:
- **Aman Shah** - A20560279
- **Khushi Shah** - A20560254
- **Sneha Veerla** - A20582712
- **Sirojiddin Kamolijonov** - A20594489

## Abstract
This project investigates crime patterns using a dataset of reported crimes in Chicago from 2001 to the present. The study aims to uncover insights into the temporal, spatial, and categorical trends of crimes and develop predictive models to assist in crime analysis and prevention.

## Objectives
- Explore and understand the distribution of crime across time, space, and categories.
- Identify key correlations and relationships among features like time, arrest status, and location.
- Apply dimensionality reduction and unsupervised learning techniques to reveal patterns.
- Develop and evaluate predictive models to classify crime types effectively.
- Propose strategies for improving the accuracy and usability of crime analysis models.

## Methods
- **Data Exploration**: Cleaning and preprocessing a sample of 100,000 crime records to remove duplicates and missing values.
- **Visualization**: Utilizing correlation heatmaps, scatter plots, and advanced techniques like PCA, UMAP, and t-SNE for dimensionality reduction and pattern identification.
- **Predictive Modeling**: Training machine learning models (Logistic Regression, Ridge Classifier, and XGBoost) on selected features to classify crimes.
- **Evaluation**: Applying cross-validation and metrics like accuracy, precision, recall, and F1-score to assess model performance.
- **Improvement**: Experimenting with feature selection, regularization, and ensemble methods to optimize performance.

## Key Findings
- Strong temporal patterns with higher crime rates during specific hours and months.
- Geospatial analysis identified high-crime areas and hotspots across Chicago.
- Logistic Regression and Ridge Classifier provided baseline classification accuracy, while XGBoost demonstrated improved performance.
- Dimensionality reduction via PCA and t-SNE provided meaningful visual insights but required further refinement for predictive use.
- Strategies like feature engineering and hyperparameter tuning showed potential for boosting model accuracy.

## Summary
This project highlights the value of data-driven approaches in understanding crime dynamics. Insights from temporal and spatial analyses can assist policymakers and law enforcement agencies in resource allocation and crime prevention strategies. Predictive models demonstrated the feasibility of automating crime classification, with potential applications in real-time surveillance and decision-making systems. Future work could incorporate additional datasets (e.g., socioeconomic factors) to improve predictive power and broaden the scope of crime analysis.

## Data Overview
**Source**: The dataset, *Crimes - 2001 to Present*, is publicly available on the City of Chicago's data portal ([data.cityofchicago.org](https://data.cityofchicago.org)).

It contains detailed records of reported crimes in Chicago from 2001 to the present, including attributes like the type of crime, location, and temporal details.

### Features and Target Variable
- **ID**: Unique identifier for the crime report.
- **Case Number**: A unique identifier for each reported case.
- **Date**: The date and time when the crime occurred.
- **Block**: Approximate address of the crime.
- **Primary Type**: The category of the crime (e.g., THEFT, BATTERY, NARCOTICS).
- **Description**: A detailed description of the type of crime.
- **Location Description**: Where the crime occurred (e.g., STREET, RESIDENCE, PARK).
- **Arrest**: Whether an arrest was made (True/False).
- **Domestic**: Whether the crime was domestic-related (True/False).
- **Latitude and Longitude**: Geographic coordinates for crime location.
- **Year, Month, Day of Week, Hour**: Temporal details derived from the Date column.

**Target Variable**: *Primary Type* (crime category).

### Data Types and Structures
- **Categorical**: Primary Type, Location Description, Arrest, Domestic.
- **Numerical**: Latitude, Longitude, Year, Month, Hour.
- **Date/Time**: Date.
- **Data Structure**: The dataset is structured as a CSV file, typically containing millions of rows and around 22 columns.

### Initial Observations
- The dataset is large and diverse, covering a wide range of criminal activity over multiple decades.
- The *Primary Type* column has more than 30 unique categories, suitable for multi-class classification.
- Certain columns, such as Latitude and Longitude, can be used to visualize crime hotspots geographically.
- Temporal columns (Year, Month, Hour) provide insights into seasonal and daily crime patterns.
- Data cleaning is required due to missing values in Latitude, Longitude, or Primary Type.
- Categorical columns (Location Description, Arrest, Domestic) need encoding for modeling purposes.

## Data Preprocessing
### Handling Missing Values:
- **Identifying Missing Data**: Checked for missing values in critical columns using `data.isnull().sum()`.
- **Actions Taken**:
  - Rows missing the *Primary Type* (target variable) were removed.
  - Rows with missing Latitude and Longitude values were dropped for geographic analysis.
  - Other missing values were handled based on the importance of the column.

### Encoding Categorical Variables:
- **Label Encoding**: Used for *Primary Type* to convert crime categories into numeric labels for classification tasks.
- **One-Hot Encoding**: Applied to *Location Description* to retain meaningful categorical data.
- Converted *Arrest* and *Domestic* (binary variables) to 0 and 1.

### Removing Outliers:
- Used the interquartile range (IQR) method to identify and remove outliers in numeric columns like Latitude, Longitude, and Hour.

## Data Transformation
- **Scaling**: Used *StandardScaler* to scale numeric features like Latitude, Longitude, Year, and Hour.
- **Normalization**: Applied normalization to Latitude and Longitude for clustering and hotspot visualization.

## Exploratory Data Analysis (EDA)
EDA revealed significant trends:
- **Seasonality**: Crimes are more prevalent during the warmer summer months and tend to peak around specific holidays.
- **Time of Day**: Higher crime rates are observed during late-night and early morning hours, particularly for violent crimes.
- **Geographical Patterns**: Crime hotspots are concentrated in certain areas, such as downtown and the South Side of Chicago.
- Correlations were identified between features, suggesting areas for further predictive modeling.

## Model Development
### Linear Regression
- **Purpose**: Used for baseline comparison, though linear regression was not ideal for predicting categorical crime types.
- **Limitations**: Assumes linear relationships and does not perform well for non-linear data.

### Random Forest Classifier
- **Advantages**: Effective for handling both categorical and numerical data, robust against overfitting, and can manage missing data.
- **Limitations**: Less interpretable than simpler models.

### Gradient Boosting Machines (XGBoost)
- **Advantages**: High predictive accuracy, especially for large datasets with complex patterns.
- **Limitations**: Computationally expensive and sensitive to noisy data.

## Evaluation Metrics
- **Accuracy**: Measures correct predictions.
- **F1-Score**: Balances precision and recall, important for imbalanced datasets.
- **Precision and Recall**: Precision measures false positives, recall measures false negatives.
- **Confusion Matrix**: Displays detailed class-wise predictions.
- **Log-Loss**: Measures how well the model predicts probabilities.

### Results (Micro Average)
- **Precision**: 0.299
- **Recall**: 0.533
- **F1-Score**: 0.383
- **Support**: 7379

### Key Findings from the Model
- XGBoost performed well in detecting high-incident crimes but struggled with less frequent crimes (e.g., BATTERY).
- The recall for certain crime types like NARCOTICS was high, but precision was lower, suggesting the need for more refined models.
- Class imbalance was a significant issue, with some categories like BATTERY showing very poor results.

## Limitations
- **Class Imbalance**: Some crime types were underrepresented, leading to skewed performance.
- **Feature Selection**: Additional factors, like socioeconomic data, were not included.
- **Data Quality**: Missing or incorrect data could introduce biases.
- **Overfitting**: Some models overfitted the training data, impacting generalization.
- **Limited Data**: Only a sample of the data was used, possibly missing broader trends.
- **External Factors**: The model does not account for external influences like policy changes.

## Conclusion
The project analyzed crime trends in Chicago and built predictive models to classify crime types. XGBoost outperformed other models but was still challenged by class imbalance. Future improvements could involve addressing this imbalance, refining feature engineering, and exploring advanced models to improve accuracy.

---

Feel free to adapt this format further to match your project's specific structure and requirements!
