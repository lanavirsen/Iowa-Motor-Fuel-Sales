# :fuelpump: Iowa Motor Fuel Sales Project

## :construction: This repository is a Work-In-Progress :construction:

![Iowa logo](https://github.com/lanavirsen/Iowa-Motor-Fuel-Sales/assets/101061448/d8279a2f-619b-46b7-9cf0-829a041da9c4)

# Introduction

In this project, I explore the dataset **"Iowa Motor Fuel Sales by County and Year"**.

### About the dataset

From **data.iowa.gov**:

Iowa motor fuel retailers are businesses that offer a range of fuel options, including gasoline, diesel, ethanol, and biodiesel. Iowa Code section 452A.33 requires all Iowa fuel retailers to report motor fuel and diesel gallons to the Iowa Department of Revenue and for the Department to prepare and submit an annual report of fuel gallons to the Iowa Governor and Legislature. The full annual reports related to this dataset are published on the [Iowa Department of Revenue web page](https://tax.iowa.gov/report-category/retailers-annual-gallons).

**The State of Iowa set a goal to replace 25.0 percent of petroleum in Iowa with biofuel by 2020,** and the `Biofuel Distribution Percentage` measures how the State is doing toward meeting that goal. 

### Within the scope of this project, I aim to answer the following questions:

- How have sales of different types of fuel changed over the 2012-2022 period?
- How do fuel sales and the biofuel distribution percentage correlate with the number of retail locations?
- What is the biofuel distribution percentage across different counties, and how does it compare to the state's goal?
- How does the biofuel distribution percentage trend over the years, and does the state meet its 2020 goal?

### The tools I use:

- **Python**: Primary programming language used for data manipulation and analysis.
- **Pandas**: Python library for data manipulation and analysis, used for cleaning and transforming the dataset.
- **Matplotlib/Seaborn**: Visualization libraries in Python, employed for creating plots and graphs to explore data trends.
- **Geopandas**: An extension of Pandas, used for working with geospatial data.
- **Scikit-learn**: Machine learning library used for predictive modeling and analysis.
- **NumPy**: A fundamental package for scientific computing in Python.
- **Jupyter Notebook**: Interactive computing environment used for documenting the data analysis process.

# Data Sources

1. The dataset **"Iowa Motor Fuel Sales by County and Year"** has been provided by: Iowa Department of Revenue.

- [Dataset link](https://data.iowa.gov/Sales-Distribution/Iowa-Motor-Fuel-Sales-by-County-and-Year/hbwp-wys3/about_data)  
- Access & Use information: This dataset is intended for public access and use.
- License: CC0
- Data Last Updated: March 4, 2024
- Data Coverage: 
  - Start Date: 2012
  - End Date: 2022

2. The Shapefile **"Iowa County Boundaries"**, used for geographical visualization, has been provided by: Iowa Geospatial Data Clearinghouse.

- [Shapefile link](https://geodata.iowa.gov/datasets/iowa::iowa-county-boundaries/about)
- Accessibility: Public - anyone can see this content
- Data Updated: January 28, 2020

# The dataset's description

The dataset has 9 columns and 1075 rows.

**Data.iowa.gov** provided the following description of the dataset's columns:

|                                 Column name |                                                                                                Description |       Type |
|--------------------------------------------:|-----------------------------------------------------------------------------------------------------------:|-----------:|
|                               Calendar Year |                                                                           Calendar year when fuel was sold |     Number |
|                                      County |                                                                                 County where fuel was sold | Plain text |
|                  Number of Retail Locations |                                                          Number of retail fuel locations within the county |     Number |
|     Non-Ethanol Gasoline Sales (in gallons) |                                                                       Gallons of non-ethanol gasoline sold |     Number |
|         Ethanol Gasoline Sales (in gallons) |                                                                           Gallons of ethanol gasoline sold |     Number |
|    Clear and Dyed Diesel Sales (in gallons) |                                                                      Gallons of clear and dyed diesel sold |     Number |
| Clear and Dyed Biodiesel Sales (in gallons) |                                                                   Gallons of clear and dyed biodiesel sold |     Number |
|           Pure Biodiesel Sales (in gallons) |                                                                             Gallons of pure biodiesel sold |     Number |
|             Biofuel Distribution Percentage | Biofuel Distribution Percentage = (Pure Ethanol Gallons + Pure Biodiesel Gallons) / Total Gasoline Gallons |     Number |

# Steps done

## 1. Data Cleaning

### 1.1. Renaming Columns

I needed to rename one column due to a formatting issue.

### 1.2. Handling Missing Values

The dataset contained missing values in various columns

After closer inspection, I decided to keep the missing values for now, as most of them wouldn't affect the analysis I was conducting in the scope of this project. The ones that later proved to affect the integrity of the geographical visualization got imputed (through interpolation and extrapolation) in one of the following steps. 

### 1.3. Considerations Regarding Data Types

Three of the columns that were expected to have integer values had their data type set to float due to the missing values present.

As I decided to keep the missing values, the data type of the columns remained set to float. 

### 1.4. Checking String Case

To avoid possible future issues when I would be merging the dataset with geographical data, I reinforced title case in the `County` column.

### 1.5. Handling Duplicates

There were no duplicates in the dataset.

### 1.6. Identifying Outliers

The dataset revealed a great number of outliers in different columns. 

After a thorough investigation, I replaced some outliers that appeared to be errors, while retaining most values identified as outliers.

## 2. Analysis

### 2.1. Trend Analysis

I analyzed sales trends over the years to understand the market dynamics for different types of fuels.

### 2.2. Impact of Retail Locations

I evaluated the impact of the `Number of Retail Locations` on fuel sales, as well as the `Biofuel Distribution Percentage`.

To explore the relationship, I used scatter plots and correlation analysis. 

### 2.3. Regional Insights

I examined the `Biofuel Distribution Percentage` across different counties through geographical visualization.

For that, I used **geopandas** library and a shapefile defining the boundaries of Iowa's counties.

As the visualization revealed missing values for the `Biofuel Distribution Percentage` for some counties for certain years, these values got imputed (through interpolation and extrapolation).

### 2.4. Biofuel Adoption

- I assessed Iowa's progress towards the state's goal of replacing 25% of petroleum with biofuel by 2020.
- I identified counties with `Biofuel Distribution` equal or above 25% in 2020.
- Assuming a linear trend, I predicted when the state could achieve its goal.

# Conclusion

Answering the questions posed at the beginning on this project.

## How have sales of different types of fuel changed over the 2012-2022 period?

![Figure 1](https://github.com/lanavirsen/Iowa-Motor-Fuel-Sales/assets/101061448/a06d8fbf-8c1c-4c02-be04-bf1aa466497a)

*Figure 1: Annual sales trends for various fuel types.*

- **Total Ethanol Gasoline Sales** generally remained high. They were increasing in the period between 2012 and 2016, peaking at over 1.37 billion gallons in 2016, then plateaued between 2016 and 2019 before starting to decrease from nearly 1.35 billion gallons in 2019 to slightly over 1.11 billion gallons in 2022.
- **Total Clear and Dyed Biodiesel Sales** were on the rise from about 286 million gallons in 2012 to approximately 495 million gallons in 2019, then entering a potential plateau. 
- **Total Clear and Dyed Diesel Sales**  showed fluctuations over the years with a peak in 2015 (over 481 million gallons) before beginning to decline, with a slight increase to nearly 350 million gallons noted in 2022.
- **Total Pure Biodiesel Sales**, introduced in 2018, remain relatively stable with a slight decrease over the registered years from nearly 210 million gallons in 2018 to about 198 million gallons in 2022.
- **Total Non-Ethanol Gasoline Sales**  consistently decreased throughout the entire period from approximately 272 million gallons in 2012 to around 163 million gallons in 2022.

## How do fuel sales and the biofuel distribution percentage correlate with the number of retail locations?

The number of retail locations has a strong positive relationship with fuel sales across all types (in other words, fuel sales increase proportionally with the number of retail outlets). Figure 2 below shows the heatmap of the relationships sorted by their strength.

![Figure 2](https://github.com/lanavirsen/Iowa-Motor-Fuel-Sales/assets/101061448/31780c66-e0d8-452f-bd01-5879a359e2be)

*Figure 2: Correlation of the number of retail locations with fuel sales and the biofuel distribution percentage.*

A correlation coefficient close to 1 indicates a strong positive relationship, while a coefficient near 0 suggests no linear relationship.

No relationship between the `Number of Retail Locations` and the `Biofuel Distribution Percentage` was found.

## What is the biofuel distribution percentage across different counties, and how does it compare to the state's goal?

The State of Iowa set a goal to replace 25% of petroleum in the state with biofuel by 2020.

The data shows that **by 2020, the majority (75%) of Iowa's counties had the `Biofuel Distribution Percentage` below 13.6%**, falling significantly short of this target.

There were **6 counties** with `Biofuel Distribution` equal or above 25% in 2020, or **6.1% of all the counties** of state Iowa.
These counties are listed below on Figure 3.

![Figure 3](https://github.com/lanavirsen/Iowa-Motor-Fuel-Sales/assets/101061448/d125dd77-4f8e-46f0-b880-c746d09e0757)

*Figure 3: The list of counties with biofuel distribution equal or above 25% in 2020.*

The following animation on Figure 4 illustrates the yearly changes in biofuel distribution percentages across Iowa counties over a decade.

A color scale is used where deep red signifies a low `Biofuel Distribution Percentage` (0%), transitioning to an off-white for percentages around 25% (the state's goal), and culminating in deep blue for the highest percentages (up to 50%).

![Figure 4](https://github.com/lanavirsen/Iowa-Motor-Fuel-Sales/assets/101061448/b2893471-e8c9-4001-bd7b-c594531d2dd0)

*Figure 4: Animated biofuel distribution percentage by county (2012-2022).*

## How does the biofuel distribution percentage trend over the years, and does the state meet its 2020 goal?

There has been a gradual increase in the biofuel distribution percentage from **9.4% in 2012** to **15.1% in 2022**, but **the state did not achieve its goal of replacing 25% of petroleum with biofuel by 2020**.

![Figure 5](https://github.com/lanavirsen/Iowa-Motor-Fuel-Sales/assets/101061448/fac2a29b-0696-4774-8f51-e47e5ca91777)

*Figure 5: Annual average biofuel distribution percentage and forecast to 25% goal.*

Assuming a linear trend, the `Biofuel Distribution Percentage` is **predicted to reach 25% in the year 2042**.
