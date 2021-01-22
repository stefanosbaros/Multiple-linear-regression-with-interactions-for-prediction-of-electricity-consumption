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


## Load-temperature characteristic

From the two figures below, we see that there is high correlation between the peaks and valleys of the temperature and the electric load. This  aligns  well  with  intuition  and  corroborates  the  causal relationship  between  temperature  and  load  that  is,  high  and low  temperature  are  the  main  drivers  behind  the  load  peaks. We  can  hence  forecast  the  load  through  its  relationship  with temperature. 
![Load](load_four_years.png)
![Temperature](temperature_four_years.png)
Using  our  data,  we  plot  the  load  versus  temperature  characteristic to get a feeling of its shape. We  see  that,  this  characteristic  has  predominantly  a  quadratic/cubic  U-shape.  We  note  that,  this curve  is  not symmetric  with  its right  part  exhibiting  steeper  slope  than  the  left  one.  The minimum  of  this curve  appears to be  around  62  F.  Given  the  shape of this curve one easily concludes that piecewise linear, piecewise quadratic, continuous quadratic or cubic functions seem to be the most appropriate functions for capturing the basic relationship between the load and temperature. In this project, we explore both a continuous  quadratic  function and a cubic function to  model  the  load-temperature  relationship. 

![caption='Load-temperature characteristic'](load_temp.png)

