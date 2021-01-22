# Multiple linear regression with interaction effects for load forecasting


## Project description
Forecasting electric load accurately lies at the heart of  power  system  operation  routines  such  as  economic  dispatch and optimal power flow. For this reason, there is a lot of interest  on  developing  accurate  models for  predicting  electric  load  over  recent  years.  Prior  art  in  this domain used time-series and linear regression as means for developing good  forecasting  models.  In this project, we use multiple regression with interaction effects and cyclical features encoding to develop a new model that can accurately predict electric load from several features including the temperature.  We  validate  different versions of our  model  and  quantify  their  performance  via both standard  goodness-of-fit-criteria such as the adjusted $R^2$ as well as criteria that rely on the prediction error. 


## Description of files

There are **four** main files in this project repository:

- `dataPrep.py`
- `DataAnalysis.py`
- `holiday_list_conv.py`
- `Load_forecasting.py`

The `dataPrep.py` **Ana describe**

## Project details

### Load-temperature characteristic

From the two figures below, we see that there is high correlation between the peaks and valleys of the temperature and the electric load. This  aligns  well  with  intuition  and  corroborates  the  causal relationship  between  temperature  and  load  that  is,  high  and low  temperature  are  the  main  drivers  behind  the  load  peaks. We  can  hence  forecast  the  load  through  its  relationship  with temperature. 
![Load](load_four_years.png)
![Temperature](temperature_four_years.png)
Using  our  data,  we  plot  the  load  versus  temperature  characteristic to get a feeling of its shape. We  see  that,  this  characteristic  has  predominantly  a  quadratic/cubic  U-shape.  We  note  that,  this curve  is  not symmetric  with  its right  part  exhibiting  steeper  slope  than  the  left  one.  The minimum  of  this curve  appears to be  around  62  F.  Given  the  shape of this curve one easily concludes that piecewise linear, piecewise quadratic, continuous quadratic or cubic functions seem to be the most appropriate functions for capturing the basic relationship between the load and temperature. In this project, we explore both a continuous  quadratic  function and a cubic function to  model  the  load-temperature  relationship. 

![caption='Load-temperature characteristic'](load_temp.png)


### Seasonal effects on Load - temperature characteristic
Having discussed the main form of the load-temperature characteristics, we now explore how the particular month of the year, day of the week, and hour of the day affect the load either directly via energy-demanding human activities or indirectly via changes in the load-temperature relationship.

#### Effect of Month of the Year on Load
Summer months are characterized by high temperatures while winter months by low temperatures. Therfore each different month of the year contributes to a different part of the load-temperature characteristic. The months between May and September contribute to the right part while the months between December and March to the left part and the rest of the months to the bottom part. Now, the critical question is:
- Can the same load-temperature characteristic be used to explain the relationship between temperature and load in different months?
To gain more insight, we plot the Load-Temperature characteristic for several months of the year. From these plots, we see that the quantitative relationship between the temperature and the load changes with the months e.g., same temperature leads to different load levels in different months. A few days with high temperatures in May won't lead to the same Load as days with the same temperatures in August because people would probably not turn on AC in May even if the temperature of some days is high. Similarly, a few cold days in September won't result in the same Load as days with the same temperature in October as a lot of central heating systems are scheduled to turn on in October.
It it clear from this analysis that the Load-Temperature characteristic for different months would be different. Therefore, the parameters of the funciton that describes the relationship between the Load and the Temperature really depends on the month under consideration. In regression analysis, this effect can be formally accounted in the model through interaction effects. We consider interaction among the temperature-load  characteristic and each month in our model captured by multiplying the Load-Temperature function with the month variable.

