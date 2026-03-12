# Chicago 311 Service Requests Mini-Project

## Introduction
In this mini-project, I take a look into 311 service request data from the City of Chicago. Within, I focus on data cleaning and data visualization, while using best practices along the way.

## Background
While studying for Data Analyst certification on DataCamp, some of the instructional videos utilized Evanston, Illinois' 311 request data. As a Chicago resident,
this caught my eye and inspired me to look up if my city also published it's 311 data. As you may have guessed,
they do publish it for public viewing/downloading! 

## Main Goals

As this was intended to be a mini-project, there were only two primary objectives to accomplish:
### 1. Utilize Python to load, inspect, and clean the data as needed
### 2. Load the data into Power BI for visualization and dashboard certification

## Data Loading, Inspection, and Cleaning 
```py 
import pandas as pd

chicago311 = pd.read_csv('D:Chicago311\chicago311_Service_Requests.csv')
```
