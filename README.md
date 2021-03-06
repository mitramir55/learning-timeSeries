# learning-timeSeries


<b>Basic definition of Time Series Analysis:</b> I think this branch of ML is just fooling itself.</br>
You have one set of data that you use to predict the future. Y is basically X but in a lagged time.



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
| *correlogram: Partial autocorrelations of US Unemployment through lag 12 with 95% confidence intervals of no correlation.* |


Things to consider in a time series dataset:

- Seasonality: 
     * weekly indicators
     * Annual with Fourier pairs. (you have to use fourier calandar and add the order double that of 
     the number of observed trends seen in the deterministic process.)

- National Holidays. (we can create indicators with those.)

- Cycles in the dataset. (time series self-dependency / serial dependence)

- Are there any other datasets that can help us predict? For example, can we use google searches
for flu cough to create lag features and see if they can predict future flu visits?

Important Plots:

PACF:

*  For detecting autocorrelation


* what it does: Calculate the exact (Only the direct) effect that Xt-n has on Xt

| <img src="images/pacf.png" alt="drawing" width="600" /> | 
|:--:| 
| *PACF* |

Tutorial:
[link](https://www.youtube.com/watch?v=5-2C4eO4cPQ)

ACF:

* This includes indirect effects.

* pearson correlation

Definitions:

* Lead time: 
How much you bring Xs forward in time

| <img src="https://i.imgur.com/xwEgcOk.png" alt="drawing" width="600" /> | 
|:--:| 
| *time series prediction with ml algorithms* |

```
# we bring outputs forward
def make_multistep_target(ts, steps):
    return pd.concat(
        {f'y_step_{i + 1}': ts.shift(-i) for i in range(steps)}, axis=1)

```

* Lags:

```
# we bring features back in time
def make_lags(ts, lags, lead_time=1):
    return pd.concat(
        {
            f'y_lag_{i}': ts.shift(i) for i in range(1, lags + 1)
        },
        axis=1)
```

multi-output regression problem:

How do we approach it?

* Direct: Directly create a separate model for each output. (A thousand different models for a thousand future points)

* Recursive: Look at the last point for predicting one time in the future.

* DiRec: Look at several time steps before by pushing the target forward and pulling the features backwards, so we get
records with 1, 2, 3,..., n lagged features and also 1, 2, 3,..., steps in the future. Then the model uses these n lagged features to predict several points in the future. 
    - take this that not all the models are able to produce multiple outputs. So you have to wrap them in another function.


