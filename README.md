# Multiple linear regression with interaction effects for load forecasting


## Project description

Electric load forecasting lies at the heart of  power  system  operation  routines  such  as  economic  dispatch and optimal power flow.  This sparked a lot of interest in recent years towards  developing  accurate  models for  predicting  electric  load.  Prior  art  in  this domain employed time-series and linear regression as means for developing good  forecasting  models.  In this project, we use **multiple regression with interaction effects and cyclical features encoding** to develop a new model that can accurately predict electric load from several features including the temperature.  We  test our full model together with various reduced-order models that arise after considering subsets of all features and  quantify  their  performance  via both standard  **goodness-of-fit-criteria** such as the adjusted R-squared as well as criteria that rely on the **prediction error**. 



## Description of files


There are **four** main files in this project repository:

- `dataPrep.py`
- `DataAnalysis.py`
- `holiday_list_conv.py`
- `Load_forecasting.py`

The `dataPrep.py` **Ana describe**

## Project details

### Load-temperature characteristic

From the two figures below, we see that there is high correlation between the peaks and valleys of the temperature and the electric load. This  aligns  well  with  intuition  and  corroborates  the  causal relationship  between  temperature  and  load  that  is,  high  and low  temperature  are  the  main  drivers  behind  the electric load  peaks. We  can  hence  forecast  the  load  through  its  relationship  with temperature. 
![Load](load_four_years.png)
![Temperature](temperature_four_years.png)
Using  our  data,  we  plot  the  load  versus  temperature  characteristic to get a sense of its overall shape. We  see  that,  this  characteristic  has a  predominantly  quadratic/cubic  U-shape.  We  note  that,  this curve  is  not symmetric  as  its right  part  exhibits  steeper  slope  than  the  left  part.  The minimum  of  this curve  appears at  62  F.  Given  the  shape of this curve one can easily conclude that piecewise linear, piecewise quadratic, continuous quadratic or cubic functions seem to be the most appropriate functions for capturing the basic relationship between the load and temperature. In this project, we explore both a continuous  quadratic  function and a cubic function to  model  the  load-temperature  relationship. 

![caption='Load-temperature characteristic'](load_temp.png)


### Capturing seasonal effects on load-temperature characteristic via interaction effects
Having discussed the main form of the load-temperature characteristics, we now explore how the particular month of the year, day of the week, and hour of the day affect the load either directly via energy-demanding human activities or indirectly via changes in the load-temperature relationship.

#### Effect of month of the year on electric load
Summer months are characterized by high temperatures while winter months by low temperatures. Therefore each different month of the year contributes to a different part of the load-temperature characteristic. The months between May and September contribute to the right part while the months between December and March to the left part and the rest of the months to the bottom part. Now, the critical question is:

- *Can the same load-temperature characteristic be used to capture the relationship between temperature and load in different months?*

To gain more insight, we study the load-temperature characteristic for several months of the year. From these plots, we see that the quantitative relationship between the temperature and the load varies along with the month. This simply means that same temperature will lead to different electric load levels in different months. A few days with high temperatures in May will not lead to the same load as days with the same temperatures in August as people would probably not turn on AC in May even if the temperature in some days is high. Similarly, a few cold days in September will not result in the same load as days with the same temperature in October as a lot of central heating systems are usually scheduled to turn on in October.
It it clear from this analysis that the **load-temperature characteristic for different months would be different**. Therefore, the function that describes the relationship between the load and the temperature really depends on the month under consideration. In regression analysis, such effects can be formally accounted for in a model through interaction effects. Here, we consider **interaction effects among the temperature-load  characteristic and each month** in our model by adding new features.



#### Effect of day of the week on the electric load
The load-temperature characteristic does not depend on the particular day of the week e.g., the same temperature during the week should lead to approximately the same Load in a weekday and the weekends, assuming that everything else remains equal. There is no reason for people to react to a particular temperature differently during a weekday than in the weekend. Further, there is not reason for the temperatures during the week to be different than the temperatures during the weekend. Nevertheless, the load on the weekdays will be different than the load on the weekend primarily due to people engaging in different activities on the weekends than on weekdays that demand different energy levels. To consider this direct effect, we use several cyclical variables

**Ana fill out**
--- Monday, other weekday, Saturday, Sunday, and other Holidays. These variables will take on the values 0 or 1 depending on the day of the week.



#### Effect of hour of the day on the load
The temperature varies with the hour of the day. We want to see whether the load-temperature characteristic depends on the hour of the day. Plotting the load for different hours of the day, we see that the load-temperature characteristic does change with the hour of the day. This aligns with intuition as low temperature in the middle of the the night will not lead to the same electric load as the same temperature at noon the day after--- as people most likely will not wake up and turn on heat in the middle of the night. 
To account for this effect, we allow **interaction of the load-temperature characteristic with the hour of the day** by adding new features.
The hour of the day also affects the load through the heat build-up effect. The temperature at the previous hour will affect the load at the current hour together with the temperature at the current hour. To understanding this,  consider the following two scenarios. In the first scenario,  consider a winter day where the temperature at the previous hour is higher than the temperature at the curren hour. In this case, the buildings' walls would have stored some heat and thus there is not need for people to ramp up their heating systems at the current hour. In the second scenario,  consider that the temperature in the previous hour is the same with the temperature at the current hour (and equal to the temperature at the current hour of the previous scenario). In this case there is not much heat build-up in the buildings so at the current hour people would have to to use their heating systems more heavily despite having the same temperature as in the previous scenario.

## Results

The **features** we use in this project are:

- `features =['TREND','TMP','TMP2','TMP3','SIN_MONTH','COS_MONTH','TMPxSIN_MONTH',`
            `'TMPxCOS_MONTH','TMP2xSIN_MONTH','TMP2xCOS_MONTH', 'TMP3xSIN_MONTH','TMP3xCOS_MONTH',`
           ` 'TMPxSIN_HOUR','TMPxCOS_HOUR','TMP2xSIN_HOUR','TMP2xCOS_HOUR', 'TMP3xSIN_HOUR','TMP3xCOS_HOUR',`
           ` 'DTMPxSIN_HOUR', 'DTMPxCOS_HOUR']`
            
where TMP, TMP2 and TMP3 denote the temperature, temperature squared and temperature in the cubic power, respectively. The features SIN_MONTH, COS_MONTH, SIN_HOUR, COS_HOUR denote the cyclical variables associated with the particular month of the year and hour of the day. We construct various models by considering the following
