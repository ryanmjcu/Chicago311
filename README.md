# Chicago 311 Service Requests Mini-Project

## Introduction
In this mini-project, I take a look into 311 service request data from the City of Chicago. Within, I focus on data cleaning and data visualization, while using best practices along the way.

## Background
While studying for Data Analyst certification on DataCamp, some of the instructional videos utilized Evanston, Illinois' 311 request data. As a Chicago resident,
this caught my eye and inspired me to look up if my city also published it's 311 data. As you may have guessed,
[they do in fact publish it for public viewing/downloading](https://data.cityofchicago.org/Service-Requests/311-Service-Requests/v6vf-nfxy/about_data)! 

## Main Goals

As this was intended to be a mini-project, there were only two primary objectives to accomplish:
### 1. Utilize Python to load, inspect, and clean the data as needed
### 2. Load the data into Power BI for visualization and dashboard certification

## Data Loading
```py 
import pandas as pd

chicago311 = pd.read_csv('D:Chicago311\chicago311_Service_Requests.csv')

chicago311_staging = chicago311.copy()
```

## Data Cleaning
```py
# Convert "%DATE%" field type to datetime
chicago311_staging['CREATED_DATE'] = pd.to_datetime(chicago311_staging['CREATED_DATE'],format = '%m/%d/%Y %H:%M:%S %p')

chicago311_staging['LAST_MODIFIED_DATE'] = pd.to_datetime(chicago311_staging['LAST_MODIFIED_DATE'],format = '%m/%d/%Y %H:%M:%S %p')

chicago311_staging['CLOSED_DATE'] = pd.to_datetime(chicago311_staging['CLOSED_DATE'],format = '%m/%d/%Y %H:%M:%S %p')
```

This step ensures all the date fields are of the correct data type, next I look into missing (null) values:
```py
# Identify missing values
print(chicago311_staging['COMMUNITY_AREA'].isna().value_counts())
print(chicago311_staging['WARD'].isna().value_counts())

# Drop NaN rows
chicago311_staging = chicago311_staging.dropna(subset = 'COMMUNITY_AREA')
chicago311_staging = chicago311_staging.dropna(subset = 'WARD')
```
Why drop instead of fill? 

Filling with a median or other aggregate value doesn't make sense for what the field is representing. While I could utilize the coordinates or latitude/longitude with a map of the city to fill in these values manually, that is both time-consuming and has minimal impact on the data. We saw that missing values make up <2000 rows of our nearly 2,000,000, so I made the decision to drop these rows.

Next, I made the final cleaning step which was to convert floats in int where appropriate:

```py
# Convert necessary floats to int
chicago311_staging['COMMUNITY_AREA'] = chicago311_staging['COMMUNITY_AREA'].astype('int')
chicago311_staging['WARD'] = chicago311_staging['WARD'].astype('int')
```

Finally, I just have to export the cleaned dataframe to a new .csv file before I can load that into Power BI for visualization!

```py
chicago311_staging.to_csv('chicago311.csv')
```

Now to create the visualizations, you can find my published dashboard [here!](https://app.powerbi.com/view?r=eyJrIjoiNWY1YjBkZDgtNGRlZS00YzYwLTg0NzAtMjQ1MjA5YTExZmMyIiwidCI6ImIxZDMxOTdlLTRlOGYtNGVkZC1hYzJjLTZlZWY4ZTJhMGRiNCJ9&pageName=41fb499f27976d7a0526)