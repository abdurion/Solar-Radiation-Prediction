## Solar-Radiation-Prediction
This project explores solar irradiance data collected from the NASA earth observing system project to evaluate long-term climate trends to predict the Global Horizontal Irradiance (GHI) and ensure the fulfillment of the required energy production.
<br>
<br>
[Raw Dataset](https://drive.google.com/file/d/1-I9EuifioMKqO2e1PSMOPKPKxqg8LZGR/view?usp=sharing) <br>
['Dashboard-Ready' Dataset](https://drive.google.com/file/d/11gnCoO1SOZAadrHr01RIIwkrcHgvZWSv/view?usp=sharing)
<br>
<br><br>
2B||!2B <br>
Team Members <br>
[Abdulrahman Alqumaidy](https://github.com/abdurion) <br>
[Hawra Alhulail](https://github.com/Hawra31) <br>
[Nawaf Althobaiti](https://github.com/Nawaf-Althobaiti) <br>
[Rahaf Alhazmi](https://github.com/Rahaf-alhazmi) <br>
[Fatimah Aldajani](https://github.com/FamAldajani) <br>
 

# Introduction
### Background
The Kingdom of Saudi Arabia aspires to increase its share of renewable energy production to stabilize its sustainable economy and diversify its energy sources. Hence, it has initiated the National Renewable Energy Program (NREP) as a part of its 2030 vision. Additionally, it has formed the Circular Carbon Economy Program (CCEP) for managing emissions to support its commitment to reaching a Net-Zero greenhouse gas emission by 2060.

### Problem Statement
Since Saudi weather is solar abundant, solar energy is considered the most feasible choice for renewable energy. Therefore, this project aims to predict the Global Horizontal Irradiance (GHI) by utilizing solar irradiance data to investigate Saudi Arabia’s solar energy projects' potential.

# Dataset Review
## Dataset Description
The dataset is collected by a solar radiation monitoring network across Saudi Arabia operated by King Abdulaziz City for Science and Technology and the National Renewable Energy Laboratory (NREL). The purpose of the dataset is to support the validation of satellite data collected by NASA to evaluate their long-term climate trends based on EOS Terra Platforms measurements data collection.

The data is collected from 10 stations in Saudi Arabia over six years, starting from 1998. For this project, we integrated the monthly data files for each year from 2000 to 2002. Hence, the overall shape of the dataset is 3,106,166 rows by 17 columns.
<br>
The table below lists the dataset features:
|     Field #    |     Element    |
|---|---|
|     1    |     Four-digit year    |
|     2    |     Month (1–12)    |
|     3    |     Day of the month    |
|     4    |     Hour of the day (0–23)    |
|     5    |     Minute of the hour (0–55)    |
|     6    |     Global horizontal irradiance, zenith angle corrected, W/m2    |
|     7    |     SERI_QC flag on global horizontal irradiance    |
|     8    |     Global horizontal irradiance, derived, W/m2    |
|     9    |     SERI_QC flag on derived global horizontal irradiance, always equal to 06    |
|     10    |     Direct normal irradiance, W/m2    |
|     11    |     SERI_QC flag on direct normal irradiance    |
|     12    |     Diffuse horizontal irradiance, W/m2    |
|     13    |     SERI_QC flag on diffuse horizontal irradiance    |
|     14    |     Air temperature, °C    |
|     15    |     SERI_QC flag on air temperature    |
|     16    |     Relative humidity, %    |
|     17    |     SERI_QC flag on relative   humidity    |

### Flags
The dataset included several SERI_QC flag features, which are used to describe the conditions of the data observations. The table below lists the flags and their description:
|     Flag    |     Description     |
|---|---|
|     00    |     Untested   (raw data)    |
|     01    |     Passed   one-component test; data fall within min-max limits.    |
|     02    |     Passed   two-component test; data fall within min-max limits.    |
|     03    |     Passed   three-component test; data come within limits.    |
|     06    |     Value estimated;   passes all pertinent SERI_QC test    |
|     07    |     Failed   one-component test; lower than allowed minimum.    |
|     08    |     Failed   one-component test; higher than allowed maximum    |
| 99 | Missing Data |


# Data Preprocessing
As mentioned above, the dataset is integrated from several files, each specified by the location, year, and month. However, the dataset required the additional columns listed below:
| 1 | Latitude |
|:---:|---|
| 2 | Longitude |
| 3 | Elevation |
| 4 | Location |
| 5 | Region |

### Imputation
We’ve identified the outliers as the points greater or less than 1.5 multiplied by the interquartile range added to the 75th or subtracted from the 25th quartiles. Additionally, several observations in the dataset are classified as untrusted or haven’t passed all the required criteria have been turned into nulls. The table below explains the imputation methodologies:
| Variable | Imputation | Imputation Method |
|---|---|---|
| Humidity | Filled in based on the location | Mean |
| Temperature | Filled sequentially | Forward Fill |
| GHI, DNI, DHI | - Values > 1000 = 1000 (Correct max) - Values < 0 = 0 (Correct min) | Selective Replacement |\

The plots below indicate that at a first glance, the dataset appears to be clean. However, it holds several wrong values.
![outlier plot](https://i.imgur.com/9hLNlht.png) ![After removing outlier](https://i.imgur.com/Uj11aFZ.png)

## Transformation
# Exploratory Data Analysis
# Building Regression Models
## Regression Problem
## Timeseries Problem Using ARIMA Model
### Summary Results
### Performance
