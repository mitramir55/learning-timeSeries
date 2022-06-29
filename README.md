# learning-timeSeries

Finished the first session of Kaggle series. 

Finished second session about trend. Basically, 
* Spline is a good library to use

the procedure is: 

- Creating a plot data = df.rolling(window=12, min_window=6).mean()

- Creating a  DeterministicProcess for trend and const:

     DeterministicProcess(index, order=1)

    For the current observations: dp.in_sample()
    For future predictions: dp.out_of_sample()

Seasonality:

* There are indicators (just like turning one field into categories.)
* and other ways like Fourier transform

to model seasonality.

We need to remove these seasonality components to predict the data itself.

Cycles:

* When the data is related to the past data not time. E.g., when we have <b> cyclical unemployment</b>:
the boom after resession that causes jobs to increase, then we have employment and then another round.

| <img src="https://i.imgur.com/CC3TkAf.png" alt="drawing" width="600" style="text-align:center;" /> | 
|:--:| 
| *Serial dependence* |




How to detect it?

* We create a correlation plot for data with different time lags. then see if they are related. 

* We can use the plot that shows how much each is predicting (the importance of each lagged value in predicting the last value).

* We can create a plot showing the rolling average. Then if the main plot was similar to the rolling average,
we can say it has predicting abilities. (the deseasoned averaged data will also show the same pattern.)


| <img src="https://i.imgur.com/6nTe94E.png" alt="drawing" width="600" /> | 
|:--:| 
| *Partial autocorrelations of US Unemployment through lag 12 with 95% confidence intervals of no correlation.* |


Things to consider in a time series dataset:

- Seasonality: 
     * weekly indicators
     * Annual with Fourier pairs. (you have to use fourier calandar and add the order double that of 
     the number of observed trends seen in the deterministic process.)

- National Holidays. (we can create indicators with those.)

- Cycles in the dataset. (time series self-dependency / serial dependence)

- Are there any other datasets that can help us predict? For example, can we use google searches
for flu cough to create lag features and see if they can predict future flu visits?