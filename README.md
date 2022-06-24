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

Things to consider in a time series dataset:

- Seasonality: 
     * weekly indicators
     * Annual with Fourier pairs. (you have to use fourier calandar and add the order double that of 
     the number of observed trends seen in the deterministic process.)

- National Holidays. (we can create indicators with those.)
