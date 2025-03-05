# Quality-of-Life-in-African-Countries
---
![Quality of Life](Assets/Images/map-of-africa.png)

# Table of Content

- [Project Objectives](#Project Objectives)
- [Data Source](#Data Source)
- [Data cleaning & transformation](#Data Cleaning & transformation)
- [Exploratory Analysis](#Exploratory Analysis)
- [Dashboard Output](#Final Dashboard Output)
- [Summary of Insight](#roject Insight)


# Project Objectives
1. Clean the data
2. Create a new column for sub-regions corresponding to each of the countries
3. Extract only the countries from the African Continent
4. Connect data to Power BI
5. Create measures using Dax in Powwer BI
6. Build Dashborad
7. Document insights
 
# Data Source
The data was downloaded from Kaggle. Click here to assess the data https://www.kaggle.com/datasets/ahmedmohamed2003/quality-of-life-for-each-country

# Data Cleaning & transformation
Data was cleaned using MysQL. Codes, below

### SQL Query 1
```sql
-- checking the information about the entire table
SELECT count(*)
FROM INFORMATION_SCHEMA.COLUMNS
where TABLE_NAME= "quality_of_life";
```

### SQL Query 2
```sql
-- Creating New column for sub_regions
ALTER TABLE quality_of_life
ADD  sub_region VARCHAR(20);

-- updating continent column for West African states (n=16)
UPDATE quality_of_life
SET sub_region = "Western Africa"
WHERE country IN ('Benin', 'Burkina Faso', 'Cape Verde', 'Ivory Coast', 'The Gambia', 'Ghana', 'Guinea', 'Guinea-Bissau', 'Liberia', 'Mali',
				'Niger', 'Nigeria', 'Senegal', 'Sierra Leone','Togo');
             
             
 -- updating continent column for North African states (n=7)
UPDATE quality_of_life
SET sub_region = "Northern Africa"
WHERE country IN ('Algeria', 'Egypt', 'Libya', 'Morocco', 'Sudan', 'Tunisia', 'Western Sahara');     
           

 -- updating continent column for East African states (n=13)
UPDATE quality_of_life
SET sub_region = "Eastern Africa"
WHERE country IN ('Burundi', 'Comoros', 'Djibouti', 'Ethiopia', 'Eritrea', 'Kenya', 'Rwanda', 'Seychelles', 'Somalia',
				'South Sudan', 'Sudan', 'Tanzania','Uganda');
                

 -- updating continent column for Central African states (n=11) 
UPDATE quality_of_life
SET sub_region = "Central Africa"
WHERE country IN ('Angola', 'Burundi', 'Chad', 'Equatorial Guinea', 'Gabon', 'Cameroon', 'Central African Republic', 'Democratic Republic of the Congo',
'Republic of the Congo','Rwanda', 'Sao Tomé and Principe');


-- updating continent column for South African states (n=13) 
UPDATE quality_of_life
SET sub_region = "Southern Africa"
WHERE country IN ('Botswana','Eswatini', 'Gambia','Lesotho', 'Madagascar', 'Malawi','Mauritania', 'Mauritius', 'Mozambique', 'Namibia', 
				'South Africa', 'Zambia', 'Zimbabwe');
```

### SQL Query 3
```sql
-- extracting Only African countries from the data
CREATE VIEW qol_Africa AS
	SELECT *
	FROM 
		quality_of_life
	WHERE
		sub_region IS NOT NULL;
        
-- Checking final selected dataset
SELECT *
FROM 
	quality_of_life.qol_africa;
 ```
# Exploratory Analysis
Some queries were run to find anwers to series of questions that provides better understanding of the data. These queries were executed to explore details regarding of the seven(7) indicators used for measuring the quality of life.

### SQL Query 4 (cost of living)
```sql
-- ANALYSIS ON COST OF LIVING
		-- average cost of living for entire Africa
		SELECT AVG(`Cost of Living Value`) AS 'average_cost_of_living(Africa) '
		FROM quality_of_life.qol_africa;

		-- average cost of living for western Africa
		SELECT AVG(`Cost of Living Value`) AS 'average_cost_of_living(Western Africa) '
		FROM quality_of_life.qol_africa
		WHERE sub_region = "Western Africa";

		-- average cost of living for Eastern Africa
		SELECT AVG(`Cost of Living Value`) AS 'average_cost_of_living(Eastern Africa) '
		FROM quality_of_life.qol_africa
		WHERE sub_region = "Eastern Africa";

		-- average cost of living for Northern Africa
		SELECT AVG(`Cost of Living Value`) AS 'average_cost_of_living(Northern Africa) '
		FROM quality_of_life.qol_africa
		WHERE sub_region = "Northern Africa";

		-- average cost of living for Southern Africa
		SELECT AVG(`Cost of Living Value`) AS 'average_cost_of_living(Southern Africa) '
		FROM quality_of_life.qol_africa
		WHERE sub_region = "Southern Africa";

		-- average cost of living for Central Africa
		SELECT AVG(`Cost of Living Value`) AS 'average_cost_of_living(Central Africa) '
		FROM quality_of_life.qol_africa
		WHERE sub_region = "Central Africa";

		-- Finding country with the lowest cost of living and its corresponding sub-region
		SELECT country, (`Cost of Living Value`), sub_region
		FROM quality_of_life.qol_africa
		WHERE `Cost of Living Value` > 0
		ORDER BY `Cost of Living Value` ASC;

		-- Finding country with the highest cost of living and its corresponding sub-region
		SELECT country, (`Cost of Living Value`), sub_region
		FROM quality_of_life.qol_africa
		WHERE `Cost of Living Value` > 0
		ORDER BY `Cost of Living Value` DESC;
```
