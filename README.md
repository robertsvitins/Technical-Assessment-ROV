# Technical-Assessment-ROV
Answers for a technical assessment

## Setup
To make sure everything runs as intended, install the required libraries.
Run pip install -r requirements.txt

The python version for this is 3.13 (python3.13)

Further description of the answers to coding questions follows.

## Question 1: Cholesky Decomposition
The essence of this question is to create a Cholesky decomposition of a covariance matrix S, so that we can generate a random vector X from a vector of standard normal random variables U. 

To create an illustrating example, I downloaded price data for AI stocks and S&P 500 from Yahoo Finance, calculated their returns and their covariance matrix S. Then I implemented the Cholesky decomposition as required. Finally, I show that the covariance matrix of the generated random vectors X matches the desired covariance matrix S.

## Question 2: Implied Credit Spread
This problem consists of two parts: (1) interpolating the zero rate curve; (2) solving for the implied credit spread. 
We need to interpolate the zero rate curve because the given rates do not match all payment dates of the given bond.
The assumption of a flat structure of credit spreads simplifies the fitting problem, as we only need to add a constant spread in the pricing function to each of the interpolated zero rates.

I have created two solutions for this problem. In the "Simple Solution" by defining lower level functions to complete the task. In the "Implementing QuantLib" I attempt to achieve the same result with the QuantLib library.

Since it was not specified what convention the zero rates follow, I created answers for different conventions.
### Simple solution results: 
The implied credit spread assuming...
1) continuous rates = 1.45%
2) simple rates = 1.71%
3) annually compounded rates = 1.49%

### QuantLib solution results:
For the QuantLib solution I only implemented the simple solution with continuous rates: the implied credit spread assuming...
1) continuous rates = 1.45%

Which matched the simple solution.

## Question 3: Pricing an American Option
The purpose of this problem is to calculate the implied volatility of an American option with given parameters. An additional twist is that we have to fit the given term structure of zero rates. I assume that these are continuous rates.

The implied volatility of an option is the volatility that, together with other parameters that can be directly observed in the market, yields the current price of the option. To calculate the implied volatility, we first need a pricing formula. For this task, I implemented a binomial tree, as that allows us to select appropriate stopping times. Then, to fit the term structure I first interpolate the zero rate curve and then calculate the forward rate for the relevant interval in the binomial tree. This allowed me to calculated fitted binomial tree.

Then using an optimization algorithm, I calculated the implied volatility for a call and a put option. These are:
1) Implied vol Call = 19.68%
2) Implied vol Put = 63.01%
