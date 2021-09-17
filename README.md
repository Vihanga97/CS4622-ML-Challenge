# 170275K | CS4622-Machine Learning | Pump it Up: Data Mining the Water Table

Highest score = **0.8170**
Rank = **1615**

Github Code Link = [https://github.com/Vihanga97/CS4622-ML-Challenge.git](https://github.com/Vihanga97/CS4622-ML-Challenge.git)

![Submission](/images/submission.jpg)

## Exploratory Data Analysis

This corpus is a collection of data regarding the functionality of water pumps, obtained from Taarifa and the Tanzanian Ministry of Water. It consists of 40 feature variables (including the id), and the target variable is divided into three categories as 'functional', 'functional needs repair', and 'non functional.'

### Main Findings from the Exploratory Data Analysis

Most of the variables included in the corpus are categorical. A few boolean and numerical featurs exist as well. The most noteworthy facts discovered during the EDA are as follows.

- 'amount_tsh' is unevenly distributed within a wide range from 0 to 350000, where a majority of values were 0.
- 'num_private' has zero values for 98.73% of data.
- All data points in the corpus have the same value of 'GeoData Consultants Ltd' for 'recorded_by.'
- Around 47% of data in the feature 'scheme_name' are null.
- The target variable exhibits a severe class imbalance, with 54.3%, 38.4%, and 0.07% of the corpus belonging to classes 'functional', 'functional needs repair', and 'non functional' respectovely.
- 'funder,' 'installer', 'permit', 'public_meeting', 'scheme_management', 'scheme_name', and 'subvillage' have null values.
- The following features are highly correlated.
  - 'extraction_type' and 'extraction_type_class' and 'extraction_type_group'
  - 'management' and 'management_group'
  - 'payment' and 'payment_type'
  - 'quantity' and 'quantity_group'
  - 'region' and 'region_code'
  - 'source' and 'source_class' and 'source_type'
  - 'water_quality' and 'quality_group'
  - 'waterpoint_type' and 'waterpoint_type_group'

## Preprocessing

### Dropping Columns

The dropped columns and the reasons for dropping them are as follows.

- 'extraction_type_class' : High correlation with 'extraction_type'
- 'extraction_type_group' : High correlation with 'extraction_type'
- 'id' : Unique to each data point
- 'num_private' : Consists mostly of zeros
- 'payment' : High correlation with 'payment_type'
- 'quality_group' : High correlation with 'water_quality'
- 'quantity_group' : High correlation with 'quantity'
- 'recorded_by' : Has the same value for all data points
- 'region' : High correlation with 'region_code'
- 'source_class' : High correlation with 'source'
- 'source_type' : High correlation with 'source'
- 'waterpoint_type_group' : High correlation with 'waterpoint_type'

### Filling Missing Values

Null values included in all features were filled with the median value of the feature.

### Encoding

The following columns were target encoded.

-
- 'lga'
- 'scheme_name'
- 'subvillage'
- 'ward'
- 'wpt_name'

The following columns were one-hot encoded.

- 'basin'
- 'extraction_type'
- 'funder'
- 'installer'
- 'management'
- 'management_group'
- 'payment_type'
- 'quantity'
- 'scheme_management'
- 'source'
- 'water_quality'
- 'waterpoint_type'

The following column was label encoded.

- status_group : 'functional'->2, 'functional needs repair'->1, 'non functional'->0

### Other preprocessing steps

- Min-Max Scaling : Applied to the column 'amount_tsh', applied to the whole dataset before feeding to Niave Bayes Model
- Standard Scaling : Applied to the whole dataset before feeding to the Neural Network Model
- Adding Features : 'location' = 'longitude' \* 'latitude'
- Thresholding : Labels with lower counts in 'funder', 'scheme_management', 'management', and 'installer' were replaced by 'other'
- Changing features : Only the year is extracted from 'date_recorded'

## Models Used and Hyperparameters

### Random Forest

n_estimators=1000, max_depth=None, min_samples_split=6, min_samples_leaf=2, max_features='auto', min_impurity_decrease=0.1, min_impurity_split=None, bootstrap=True, warm_start=True

### XGBoost

base_score=0.5, booster='dart', colsample_bylevel=1, colsample_bynode=1, colsample_bytree=0.4, gamma=0.0, importance_type='gain', learning_rate=0.05, max_delta_step=0, max_depth=3, min_child_weight=7, missing=None, n_estimators=100, n_jobs=1,num_class=3, nthread=None, objective='multi:softmax', random_state=0, reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None, silent=None, subsample=1, verbosity=1

### K Nearest Neighbours

n_neighbors=5

### Logistic Regression

multi_class='multinomial'

### Naive Bayes

None

### Neural network

test_size=0.33, learning_rate = 0.01, epochs = 100, batch_size = 5000, validation_split = 0.1

_Hyperparameter tuning has only been done for Random Forest, XGBoost and Neural Network models._

## Feature importance (XGBoost)

![Features](/images/feature_importance.png)
