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