# 2013-2022 Michigan Water Consumption Analysis

## Table of Contents
- [Summary](#Summary)
- [Data Source](#Data-Source)
  - [Description](#Description)
  - [Data Dictionary](#Data-Dictionary)
- [SQL Analysis](#sql-analysis)
- [Python Analysis](#python-analysis)
- [Insights](#insights)
- [Contributing](#contributing)
- [License](#license)


### Summary
This analysis explores water consumption in the state of Michigan from the years 2013 to 2022. The focus is on understanding how water was used across different counties, the sources of water (whether it came from the the Great Lakes, or rather from groundwater, or inland sources), and the industries that used it, as well as which used it the most. The goal is to identify patterns, trends, and insights into Michigan's water usage in the span of an entire decade.

### Data Source

#### Description

2013-2022 Michigan Water Data: The dataset used in this analysis is from the 'water_use_data_2013_to_2022.csv' file. It contains data on the year and Michigan counties where water use was measured, the source of the water (e.g., the Great Lakes, groundwater, inland sources), the volume of water in gallons, and the industry that consumed the water. These variables allow for analysis of water usage patterns, including when, where, and for what purpose water was used.

The dataset came from a Kaggle dataset that can be found [here](https://www.kaggle.com/datasets/oleksiimartusiuk/michigan-water-use-data-2013-to-2022).

#### Data Dictionary

| Column Name       | Data Type   | Description                                                                 |
|-------------------|-------------|-----------------------------------------------------------------------------|
| `Unnamed: 0`      | Integer     | Index of the values.                        |
| `county`          | Text        | The Michigan county where the water usage was measured.                     |
| `year`            | Integer     | The year in which the water usage data was recorded.                        |
| `gallons_from_great_lakes`      | Integer     | The volume of water from the Great Lakes used, by gallons.    |
| `gallons_from_groundwater`      | Integer     | The volume of water from the ground sources used, by gallons.    |
| `gallons_from_inland_surface`      | Integer     | The volume of water from the inland sources used, by gallons.    |
| `industry`        | Text        | The industry that consumed the water (e.g., Agriculture, Manufacturing).    |
| `year`            | Integer     | The year in which the water usage data was recorded.                        |

### Tools

- DB Browser (SQLite) - Data Cleaning, Exploration and Manipulation
  - Utilized to process the data and ensure it was in a usable format for visualization and further analysis.
- Python - Data Analysis and Visualization
  - Utilized to perform statistical analyses and create simple visualizations to explore the spread and distribution of the data.
- Tableau - Data Visualization
  - Utilized in creating an interactive dashboard that presents the data in a user-friendly manner, allowing users to explore Michigan's water consumption trends over the decade.
