---
layout: post
title: Getting Started with Kats - One-Stop Shop for Time Series Analysis in Python
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Python, Data Science, Time Series, Tools and Libraries]
---

Kits to Analyze Time Series (Kats) is a light-weight, easy-to-use, and generalizable framework to perform time series analysis in Python. Time series analysis is an important part of data science and engineering work. Kats aims to provide a one-stop shop for techniques for univariate and multivariate time series including: 

1. Forecasting - Kats gives a full set of tools for forecasting that consists of ten+ individual forecasting models, ensembling, a self-supervised learning (meta-learning) model, backtesting, hyperparameter tuning, and empirical prediction intervals.

2. Anomaly and Change Point Detection - Kats upholds functionalities to identify different examples on time series data, including seasonalities, anomalies, change points, and slow trend changes.

3. Feature Extraction - TSFeature extraction module can create sixty-five features with clear statistical definitions, which can be incorporated in most machine learning models such as classification and regression.

4. Utilities - Kats also provides a set of useful utilities, such as time series simulators.

Installation:

To install Kats, use the below commands - 

```
pip install --upgrade pip
pip install kats
```

Basics:

Kats uses a `TimeSeriesData` object to represent univariate and multivariate time series. The methods below are used to initiate it:

```
from kats.consts import TimeSeriesData
import pandas as pd

df = pd.read_csv("data.csv")
kats_ts = TimeSeriesData(df)

# We can also pass specific columns
kats_ts = TimeSeriesData(time=df.time, value=df.value)
```

Operations on TimeSeriesData:

We can do many operations on Kats TimeSeriesData objects like slicing, math operations, extend, plotting, and utility functions (to_dataframe, to_array, is_empty, is_univariate).

```
# Slicing
kats_ts[1:5]

# Math Operations
kats_ts[1:5] + kats_ts[1:5]

# Extend
ts_1 = kats_ts[0:3]
ts_2 = kats_ts[3:7]

ts_1.extend(ts_2)

# Plotting
%matplotlib inline

# Must pass the name of the value columns to plot
kats_ts.plot(cols=['value'])
plt.show()
```

Forecasting:

Currently Kats supports the below TimeSeries base models for forecasting:

- Linear
- Quadratic
- ARIMA
- SARIMA
- Holt-Winters
- Prophet
- AR-Net
- LSTM
- Theta
- VAR

We can combine these to create more complex ensemble models. Let's see some examples - 

```
import pandas as pd

from kats.consts import TimeSeriesData
from kats.models.prophet import ProphetModel, ProphetParams
from kats.tsfeatures.tsfeatures import TsFeatures


df = pd.read_csv(
    "data.csv",
    header=0,
    names=["time", "value"],
)

# convert to TimeSeriesData object
kats_ts = TimeSeriesData(df)

# create a model param instance
params = ProphetParams(seasonality_mode='multiplicative')

# create a prophet model instance, NOTE - We need to install fbprophet in order to use it.
m = ProphetModel(kats_ts, params)

# fit model simply by calling m.fit()
m.fit()

# make prediction for next 30 month
fcst = m.predict(steps=30, freq="MS")

# calculate the TsFeatures
features = TsFeatures().transform(kats_ts)
```

Using the TsFeatures function, we can extract meaningful features from the given time series data.
We can also build an ensemble model using these base learners. When creating an ensemble, we have to specify the list of models (with parameters) that we wish to include in the ensemble, and then we can choose whether to aggregate these forecasts using the median or the weighted average. Prior to building any forecasts, the model checks for seasonality and if seasonality is detected, it performs an STL decomposition (using either additive or multiplicative decomposition, as specified by the user). Each of the forecasting models specified to the ensemble model are only applied to the deseasonalized components, and after these forecasts are aggregated the result is reseasonalized.
Let's see an example - 

```
from kats.models.ensemble.ensemble import EnsembleParams, BaseModelParams
from kats.models.ensemble.kats_ensemble import KatsEnsemble
from kats.models import (
    arima,
    holtwinters,
    linear_model,
    prophet,  # requires fbprophet be installed
    quadratic_model,
    sarima,
    theta,
)

# we need to define params for each individual forecasting model in `EnsembleParams` class
# here we include 6 different models
model_params = EnsembleParams(
            [
                BaseModelParams("arima", arima.ARIMAParams(p=1, d=1, q=1)),
                BaseModelParams("prophet", prophet.ProphetParams()),
                BaseModelParams("linear", linear_model.LinearModelParams()),
                BaseModelParams("quadratic", quadratic_model.QuadraticModelParams()),
                BaseModelParams("theta", theta.ThetaParams(m=12)),
            ]
        )

# create `KatsEnsembleParam` with detailed configurations 
KatsEnsembleParam = {
    "models": model_params,
    "aggregation": "median",
    "seasonality_length": 12,
    "decomposition_method": "multiplicative",
}

# create `KatsEnsemble` model
m = KatsEnsemble(
    data=kats_ts, 
    params=KatsEnsembleParam
    )

# fit and predict
m.fit()

# predict for the next 30 steps
fcst = m.predict(steps=30)

# aggregate individual model results
m.aggregate()

# plot to visualize
m.plot()

```

Changepoint detection:

Kats allows you to detect changepoints with the three major algorithms used to detect such patterns:
1. CUSUM Detection
2. Bayesian Online Change Point Detection (BOCPD)
3. Stat Sig Detection

CUSUM algorithm is used to detect an up/down shift of means in a time series.
Let's see an example - 

```
# import packages
import numpy as np
import pandas as pd

from kats.consts import TimeSeriesData
from kats.detectors.cusum_detection import CUSUMDetector

# simulate time series with increase
np.random.seed(10)
df_increase = pd.DataFrame(
    {
        'time': pd.date_range('2019-01-01', '2019-03-01'),
        'increase':np.concatenate([np.random.normal(1,0.2,30), np.random.normal(2,0.2,30)]),
    }
)

# convert to TimeSeriesData object
timeseries = TimeSeriesData(df_increase)

# run detector and find change points
change_points = CUSUMDetector(timeseries).detector()
```

That's all for now. In this tutorial, we learned about the basic operations of Kats in time series applications, including basic introductions to forecasting, changepoints detection, and feature extraction in Kats. Now you can try this library in your next time series project. We'll meet in another blog with something new. Until then, happy coding :)
