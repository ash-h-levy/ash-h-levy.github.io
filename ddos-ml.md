## This can be your internal website page / project page

**Project description:** Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

### 1. Retreive Data from Kaggle and Upload into BigQuery
I found the data for this project on [Kaggle](https://www.kaggle.com/datasets/ramakrishna0810/classification-of-ddos). The dataset contained two tables, one for training and one for testing. 

### 2. Create a Random Forest using BigQueryML

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

```SQL
CREATE MODEL IF NOT EXISTS `ddos_classification.radom_forest_model`
  OPTIONS (
    MODEL_TYPE = 'RANDOM_FOREST_CLASSIFIER',
    INPUT_LABEL_COLS = ['outcome'],
    DATA_SPLIT_METHOD = 'NO_SPLIT'
  ) AS
SELECT *
FROM `ddos_classification.ddos_train`
```

### 2. Assess assumptions on which statistical inference will be based

```SQL
#cast outcome as int64
SELECT 
 *,
 CAST(outcome AS INT64) AS outcome_int
 FROM `ddos_classification.ddos_test`
```

### 3. Support the selection of appropriate statistical tools and techniques

```SQL
ALTER TABLE `ddos_classification.ddos_test`
RENAME COLUMN outcome_int TO outcome
```

### 4. Provide a basis for further data collection through surveys or experiments

```SQL 
SELECT
  COUNT(*) AS count_incorrect,
  (1-(COUNT(*)/17169))*100 AS prediction_accuracy
FROM
  ML.PREDICT(MODEL `model-creation-383116.ddos_classification.radom_forest_model`,
    (SELECT *
    FROM `ddos_classification.ddos_test`
    ))
WHERE outcome != predicted_outcome
```
For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
