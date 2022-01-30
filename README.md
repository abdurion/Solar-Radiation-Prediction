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
Lastly, the year, month, day, hour, and minute columns are transformed into a timeseries column that is set to the index.

# Exploratory Data Analysis
![GHI and Air Temperature over a month](https://i.imgur.com/5g3TqCf.png)
Plot (1) - The air temperature and GHI are weakly correlated. As seen in the plot, at approximately 35.5 °C, the GHI value starts to degrade, which could be due to the impact of the high heat on the material of the solar panels or the humidity.\
<br>
![GHI and Relative Humidity over a month](https://i.imgur.com/gNBZHb8.jpg)
Plot (2) - The humidity and GHI are weakly negatively correlated. As seen in the plot, in June (month six) the humidity reaches its lowest value of 25%, while the GHI reaches its highest point. Also, moving to July and August, the GHI rapidly drops. Hence, we can conclude that the humidity impacts the GHI.\
<br>
![GHI For Each City](https://i.imgur.com/ZOineDv.png)
Plot (3) – the median doesn’t differ significantly from one city to another. However, we can conclude that Wadi Aldwasser and Sharurah have the best GHI values, and the Southern region has better GHI values, while the eastern region has the lowest GHI values.\
<br>
![Average GHI Per Location (Monthly)](https://i.imgur.com/ZgbenBA.png)
Plot (4) – the heat map shows that, on average, May and June are the most suitable for solar energy. Additionally, we can conclude that Sharurah and Wadi Aldwasser are the most consistent locations.\
<br>
![GHI per Month (Sharurah)](https://i.imgur.com/KMoZ4wS.png)
Plot (5) – this plot takes a closer look at one of the best locations for solar energy projects in the kingdom. The plot confirms that May is the best time for solar energy projects.\
<br>
![Hourly GHI For Sharurah in May](https://i.imgur.com/Fa2LKIo.png)
Plot (6) – At an hourly rate, on average, the GHI reaches its peak at 12 PM in Sharurah during May.\
<br>

# Building Regression Models
### Regression Problem
We achieved the best results by implementing an XGBoost regression model and hyperparameter tuning using a grid search.
```
params = { 'max_depth': [3,6,10],
           'learning_rate': [0.01, 0.05, 0.1],
           'n_estimators': [10, 100]
         }

xgbr = XGBRegressor(seed = 42)

clf = GridSearchCV(
    estimator=xgbr, 
    param_grid=params,
    scoring='neg_mean_squared_error', 
    cv = 5,
    verbose=1
)

xgbr_model = XGBRegressor(
    objective = 'reg:squarederror',
    n_estimators=100,
    max_depth = 3,
    learning_rate=0.05,
    random_state=42
)
```
We then see that the best parameters to the get the best mean test score is:
| param_max_depth | param_learning_rate | param_n_estimators | mean_test_score | rank_test_score |
|---|---|---|---|---|
| 3 | 0.05 | 100 | -20215.36 | 1 |
<br>
The results were:
| R^2 | 0.83 |
|---|---|
| MSE | 19886.39 |
| MAE | 88.03 |
<br>

### Timeseries Problem Using ARIMA Model
We can train the ARIMA model since we are working with a time series problem. Forecasting would be dependant on the time of the day.\
![Autocorrelation](https://i.imgur.com/X2JIwtV.png)
As expected, we can see the relationship varies from the autocorrelation. Negative correlation in night and positive in day hours.\
<br>
![Partial Correlation](https://i.imgur.com/efPxve2.png)
Looking at the partial correlation, there are not complete trend going on. Hence, we don't need any differencing.\
<br>
We trained the ARIMA model with these parameters.
```
model = ARIMA(train, order = (2, 0, 6))
result = model.fit(disp = 0)
print(result.summary())
```
#### Summary Results
![ARIMA Model Results](https://i.imgur.com/I7PDUiu.png)
The ma.L4.ghi_derived coefficient is close to zero. Hence, it could be removed to enhance the performance of the model.

#### Performance
![GHI Forecast](https://i.imgur.com/gORaAah.png)
## Timeseries Problem Using ARIMA Model
### Summary Results
### Performance
