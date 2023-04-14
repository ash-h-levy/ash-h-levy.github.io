## This can be your internal website page / project page

**Project description:** Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

### 1. Create a unique value for each entry

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

```SQL
UPDATE `ao3-2021-data-dump.ao3_dump_2021.works`
SET work_id = GENERATE_UUID()
WHERE work_id IS NULL

```

### 2. Assess assumptions on which statistical inference will be based

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
