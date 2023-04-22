# Archive of Our Own 2021 Data Dump Explortory Data Analysis 
The Archive of Our Own (AO3) is a popular fanfiction archive with over 7 million fanworks, encompassing various fandoms, pairings, and genres. As a platform, AO3 offers a wealth of data that can be analyzed and mined to gain insights into various aspects of fandom culture and behavior.
This project aims to conduct an exploratory data analysis (EDA) on the AO3 dataset to uncover patterns and trends in fanfiction writing and consumption using BigQuery and Looker. The analysis will focus on the following research questions:
1. What are the most popular fandoms on AO3?
2. Which genres and pairings are the most popular?
3. How has the number of fanworks on AO3 grown over time?
4. How long are fanworks on average?
5. What percentage of fanworks on AO3 are completed?
6. What are the most popular languages used in fanworks on AO3? 

## 1. ETL 

The dataset used in this project was obtained from the Archive of Our Own (AO3) website. AO3 provided the dataset for analysis to the general public, which was then downloaded and uploaded to BigQuery for analysis. The dataset consists of two CSV files containing information on fanfiction works, including fandoms, genres, pairings, word count, date created, and date last updated. The files were uploaded to BigQuery using its user interface (UI) for further analysis.


## 2. Create a unique value for each entry

Sure, here's a revised version:

The initial dataset obtained from the Archive of Our Own (AO3) did not contain a unique identifier for each work. To avoid potential issues with data analysis, it was necessary to assign a unique value to each work. This was achieved using BigQuery's GENERATE_UUID() function, which assigns a random universally unique identifier.

The following SQL code was used to create a new column for the UUIDs, assign a unique ID to each row, and set the work_id as the primary key:


``` SQL
#Create column to add UUID to 
ALTER TABLE `ao3-2021-data-dump.ao3_dump_2021.works`
ADD COLUMN work_id STRING

#Assigns unique id to each row. Each row at this point represents one unique work
UPDATE `ao3-2021-data-dump.ao3_dump_2021.works`
SET work_id = GENERATE_UUID()
WHERE work_id IS NULL

#Makes work_id the primary key for the table 
ALTER TABLE `ao3-2021-data-dump.ao3_dump_2021.works`
ADD PRIMARY KEY (work_id)
NOT ENFORCED


```

With the unique ID assigned to each work, we can now perform various analyses and queries on the data without running into issues with duplicate or missing values. 


## 5. Summary Data

``` SQL
SELECT
  COUNT(DISTINCT work_id) AS work_count,
  AVG(word_count) AS avg_word_count,
  MAX(word_count) AS max_word_count,
  MIN(creation_date) AS oldest_work,
  ((
    SELECT
      COUNT(DISTINCT work_id)
    FROM
      `ao3-2021-data-dump.ao3_dump_2021.works`
    WHERE
      restricted = TRUE)/COUNT(work_id))*100 AS percent_restricted,
  ((
    SELECT
      COUNT(DISTINCT work_id)
    FROM
      `ao3-2021-data-dump.ao3_dump_2021.works`
    WHERE
      complete = TRUE)/COUNT(work_id))*100 AS percent_completed,
FROM
  `ao3-2021-data-dump.ao3_dump_2021.works`
 ```

## 4. Finding the most common tags

```SQL
WITH
  works_created_by_day AS (
  SELECT
    creation_date,
    COUNT(DISTINCT work_id) AS work_count
  FROM
    `ao3-2021-data-dump.ao3_dump_2021.works`
  GROUP BY
    creation_date
    )

  
SELECT
  creation_date,
  SUM(work_count) OVER (ORDER BY creation_date) AS running_total
FROM
  works_created_by_day
GROUP BY
  creation_date, work_count

```

### 3. Support the selection of appropriate statistical tools and techniques

``` SQL
WITH
  unnest_tag_id AS (
  WITH
    tag_id_split AS (
    SELECT
      work_id,
      SPLIT(tags, "+") AS tags_split
    FROM
      `ao3-2021-data-dump.ao3_dump_2021.works`)
  SELECT
    work_id,
    tag_id
  FROM
    tag_id_split,
    UNNEST(tags_split) AS tag_id),
  tag_id_as_string AS (
  SELECT
    name AS tag_name,
    type AS tag_type,
    CAST(id AS STRING) AS tag_id_string
  FROM
    `ao3-2021-data-dump.ao3_dump_2021.tags` )
SELECT
  tag_id_string,
  tag_name,
  COUNT(DISTINCT work_id) AS work_count
FROM
  unnest_tag_id
JOIN
  tag_id_as_string
ON
  tag_id_string = tag_id
WHERE
  tag_type = "Freeform"
GROUP BY
  tag_id_string,
  tag_name
ORDER BY
  work_count DESC
```
### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
