# 2013-2022 Michigan Water Consumption Analysis

## Table of Contents
- [Summary](#Summary)
- [Data Source](#Data-Source)
  - [Description](#Description)
  - [Data Dictionary](#Data-Dictionary)
- [Tools](#Tools)
- [Data Cleaning and Manipulation](#data-cleaning-and-manipulation)
- [Insights](#insights)
- [Contributing](#contributing)
- [License](#license)


## Summary
This analysis explores water consumption in the state of Michigan from the years 2013 to 2022. The focus is on understanding how water was used across different counties, the sources of water (whether it came from the the Great Lakes, or rather from groundwater, or inland sources), and the industries that used it, as well as which used it the most. The goal is to identify patterns, trends, and insights into Michigan's water usage in the span of an entire decade.

### Data Source

#### Description

2013-2022 Michigan Water Data: The dataset used in this analysis is from the 'water_use_data_2013_to_2022.csv' file. It contains data on the year and Michigan counties where water use was measured, the source of the water (e.g., the Great Lakes, groundwater, inland sources), the volume of water in gallons, and the industry that consumed the water. These variables allow for analysis of water usage patterns, including when, where, and for what purpose water was used.

The dataset came from a Kaggle dataset that can be found [here](https://www.kaggle.com/datasets/oleksiimartusiuk/michigan-water-use-data-2013-to-2022).

#### Data Dictionary

| Column       | Data Type       | Description                                                                      |
|-------------------|-------------|-----------------------------------------------------------------------------|
| `Unnamed: 0`      | Integer     | Index of the values.                        |
| `county`          | Text        | The Michigan county where the water usage was measured.                     |
| `gallons_from_great_lakes`      | Integer     | The volume of water from the Great Lakes used, by gallons.    |
| `gallons_from_groundwater`      | Integer     | The volume of water from the ground sources used, by gallons. |
| `gallons_from_inland_surface`   | Integer     | The volume of water from the inland sources used, by gallons. |
| `total_gallons`            | Integer     | The combined volume of water from all sources by gallons.          |
| `industry`        | Text        | The industry that consumed the water (e.g., Agriculture, Manufacturing).    |
| `year`            | Integer     | The year in which the water usage data was recorded.                        |

### Tools

- DB Browser (SQLite) - Data Cleaning, Exploration and Manipulation
  - Utilized to process the data and ensure it was in a usable format for visualization and further analysis.
- Python - Data Analysis and Visualization
  - Utilized to perform statistical analyses and create simple visualizations to explore the spread and distribution of the data.
- Tableau - Data Visualization
  - Utilized in creating an interactive dashboard that presents the data in a user-friendly manner, allowing users to explore Michigan's water consumption trends over the decade.
 

## Data Cleaning and Manipulation

### Renaming the columns and table

To make the queries easier to read, we will be changing the name of the table and some of the columns through the 'Alter' function in SQL

```sql
-- Rename the csv's table if needed to a simpler one
Alter table 'water_use_data_2013_to_2022' rename to MichiganWater;

-- Rename the columns to something less complex names
Alter table MichiganWater rename column 'Unnamed:0' to ID;
Alter table MichiganWater rename column 'gallons_from_great_lakes' to GreatLakeGallons;
Alter table MichiganWater rename column 'gallons_from_groundwater' to GroundwaterGallons;
Alter table MichiganWater rename column 'gallons_from_inland_surface' to InlandGallons;
Alter table MichiganWater rename column 'total_gallons_all_sources' to AllSources;
```

### Querying Useful Data

The rows with industry as 'Total All Sectors' will not be needed for the analysis, due to the seperate ones being useful to making insights and they prove to be redundant due to having the option to sum the values. Therefore we will make a new table that does not have this listed as the industry, while at the same time ranking the industries by how much water they use in each county, by year.


```sql
-- Rank the amount of water used by each industry, in each year, while also figuring how much water from each source was used
Create Table MIWater as Select 
	Year, 
	County,
	'Michigan' as State,
	Industry,
	GreatLakeGallons AS GreatLakeConsumption, 
	GroundwaterGallons AS GroundwaterConsumption, 
	InlandGallons AS InlandConsumption, 
	AllSources as AllConsumption,
	dense_rank() over(PARTITION by year, county order by Allsources desc) as 'Industry Rank'
from MichiganWater
where Industry != 'Total All Sectors';
```

## Exploratory Data Analysis
### Python

1. Importing the software libraries needed for analyzing the data, along with the dataset itself.

```py
# Imports the software libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

# Creates path for the dataset to be imported, and imports it
file_path = '~/Downloads/MIWater.csv'
data = pd.read_csv(file_path)
```


2. What are the summary statistics for the numerical values?
```py
# Calculate the summary statistics for the numerical values
data.describe()
```

![Screenshot 2024-08-14 at 02-49-53 Vendors - Jupyter Notebook](https://github.com/user-attachments/assets/0a3900f0-f375-4db9-a190-5d4e6cacca5c)


From the summary statistics of all the numeric variables, something very noticeable is that for Inland and Great Lake, 75% of values come up as 0. And with Groundwater 25%. This likely means that between counties, most industries use Groundwater at a more common rate than they use water from the Great Lake or Inland sources. Despite that however, Great Lake has the highest maximum volume by at least 4 times any other source. Which could mean that Great Lake consumption, is the highest in total of all sources.




3. What are the summary statistics for the categorical values?
```py
# Gather the categorical values and find the summary statistics of them
categorical = data.dtypes[data.dtypes=="object"].index
data[categorical].describe()
```





![Screenshot 2024-08-14 at 02-54-33 Vendors - Jupyter Notebook](https://github.com/user-attachments/assets/8da1fd1b-2ec3-49d0-9684-50602f1f514f)



From the categorical summary statistics are 85 different counties in the county variable for Michigan. We can also see that there are 7 different industries throughout. The state variable of course, only has Michigan in it, as we are only looking at the singular state and its water use for this analysis.


4. 




### SQL


