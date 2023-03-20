# Project 1 overview: Estimator of weekly return on share price
* Created a tool that estimates the return per calendar week of a share to help private investors get a broad timing for orders over the year.
* Implemented an exponential decay to optimize Exponential Moving Average (EMA).
* Built various models to reach best forecast through (equal) weighted average for weekly return.

## Code and resources used
* Python 3.9.15.
* Packages: pandas, numpy, math, plotly.express, plotly.graph_objects, requests, json.
* dataset: dynamic data per company on about exemplary ING Bank~[5877 rows x 9 columns] covering 20+ years of historical data from API [](https://www.alphavantage.co/).

## Data cleaning
* Implemented a search engine to access identification of shares on the market from API 
* Cleared data from irrelevant metrics and time periods.
* Preprocessed data from daily open and close prices to daily return.
* Preprocessed daily return (equal) weighted weekly return.

## EDA exemplary on estimated return of ING Bank share price
* Built Model 1 for weekly return estimation through a flexible time period selection and equally weighted return per year.

![](/Images/INGreturnanalysis20082010.jpg)

* Built Model 2 for weekly return estimation through a retrospective time period selection and weighted return per yearly exponential decay.
* Built Model 3 to control model 2 through the same time period and weighted return per yearly decay through implemented Exponential Moving Average (EMA).

![](/Images/INGretrospectivereturnanalysis12years.jpg)

* Built Cross-model of Model 1 and Model 2 to reach best forecast model.

![](/Images/INGreturncrossanalysis2008201012years.jpg)

## Model Building
I started the model building by interpreting the goal of predicting return development of a share price. <br>
So, first I built Model 1 since a relevant argument usually is, that there likely could be a repetition of past events in the current ones and with these events a similar development in the share price. In Model 1 is to set a time period with bounding years. Exemplary 2008-2010: This will show yearly overlapping and equal weighted weekly return through the post the financial crisis 2008, if it is wished to compare it with the current developement post Covid-19 and Ukrainian war.<br>
Secondly, with Model 2 I applied a common forecast technic for trend continuing past development, thus weighting yearly return from current return back to the return of past years with exponential decay. Model 3 was necessary to control Model 2 with an often used metric, here the Exponential Moving Average (EMA) over the years, to confirm return estimation.

* At this point there were three main problems to solve: price difference over time, the inaccuracy of the exact week for a certain return, the irregular calendar week 53 and setting a visual to show return over +/- developments of more that one week.
* Solutions respectively: usage of percentage, taking into account a moving three week average, making a case distinction and bounding an accumulated return to the sign of the three week average.

At last, I built a cross-model, that combines Model 1 with Model 2 in order to combine estimation, based on both arguments for return estimation: compare the current period with a past period and continuing a current trend.
* Problem: Due to more scattering by considering more years, the extreme values in Model 1 or 2 decrease, while the period length increases. 
* Solution: Weighting the values of the Model with minor absolute values, so that values of Model 1 and Model 2 have in total the same length. The minor values have to be changed, since the mayor values are supposed to come from a shorter period, so there is a more realistic return estimation due to less scattering.
## Instructions of use
* Model 1: Input is a time period with similar events as the current ones. 
* Model 2: Input is the number of years to set the length of the time period. The time period will start with weight 10% on return of the oldest year. The decay factor is being calculated through the total of years of the period. Young years are considered heavy into account.
