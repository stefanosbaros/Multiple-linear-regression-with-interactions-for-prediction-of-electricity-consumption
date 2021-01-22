# Multiple Linear Regression with Interaction Effects for Load Forecasting


## Project description
Accurately forecasting electric load lies at the heart of  power  system  operation  routines  such  as  economic  dispatch and optimal power flow. For this reason, there is a lot of interest  on  developing  accurate  models for  predicting  electric  load  over  recent  years.  Prior  art  in  this domain used time-series and linear regression as means of coming up  with  good  forecasting  models.  In this project, we use multiple regression with interaction effects to develop a new model that can accurate predict electric load from several features.  We  validate  different  models  and  quantify  their  performance  via both standard  goodness of fit criteria such as the adjusted $R^2$ as well as criteria that rely on the test set. 


## Description of files

There are **four** main files in this project repository:

- `dataPrep.py`
- `DataAnalysis.py`
- `holiday_list_conv.py`
- `Load_forecasting.py`

The `dataPrep.py` 


## Load-temperature characteristic

From Figures 2 and 3, we see that there is high correlation between the peaks and valleys of the temperature and the load. This  aligns  well  with  intuition  and  corroborates  the  causal relationship  between  temperature  and  load  that  is,  high  andvlow  temperature  are  the  main  drivers  behind  the  load  peaks. We  can  hence  forecast  the  load  through  its  relationship  with temperature. Using  our  data,  we  plot  the  load  versus  temperature  characteristics. From these  plots,  we  see  that  this  characteristic  has  predominantly  a  quadratic/cubic  U-shape.  We  note  that,  this curve  is  nonsymmetric  with  its right  part  exhibiting  steeper  slope  than  the  left  one.  The minimum  of  these  curves  is  around  62  F.  Given  their  shape, piecewise linear, piecewise quadratic, continuous quadratic or cubic functions seem to be the most appropriate functions for capturing the basic relationship between the load and temperature. In this project, we will explore both a continuous  quadratic  function and a cubic function to  model  the  load-temperature  relationship. 

![](load_temp.png)
*Load-temperature characteristic*
