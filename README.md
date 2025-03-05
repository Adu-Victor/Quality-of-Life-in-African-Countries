# Quality-of-Life-in-African-Countries
---
![Quality of Life](https://github.com/Adu-Victor/Quality-of-Life-in-African-Countries/blob/main/Assets/Images/map-of-africa.png)

# Table of Content

- [Project Objectives](#Project Objectives)
- [Data Source](#Data Source)
- [Data cleaning](#Data Cleaning)
- [Exploratory Analysis](#Exploratory Analysis)
- [Dashboard Output](#Final Dashboard Output)
- [Summary of Insight](#roject Insight)


# Project Objectives
1. Clean the data
2. Extract only the countries from the African Continent
3. Create a new column for sub-regions corresponding to each of the countries
4. Connect data to Power BI
5. Create measures using Dax in Powwer BI
6. Build Dashborad
7. Document insights
 
# Data Source
The data was downloaded from Kaggle. Click here to assess the data https://www.kaggle.com/datasets/ahmedmohamed2003/quality-of-life-for-each-country

# Data Cleaning
Data was cleaned using MysQL. Codes, below

```sql
-- checking the information about the entire table
SELECT count(*)
FROM INFORMATION_SCHEMA.COLUMNS
where TABLE_NAME= "quality_of_life";
```

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
