# Can you explain the price of electricity? by QRT

## Challenge context
Every day, a multitude of factors impact on the price of electricity. Local weather variations will affect both electricity generation and demand for instance. Long term phenomena, such as global warming, will also have a significant influence. Geopolitical events, such as the war in Ukraine, may affect in parallel the price of commodities, which are key inputs in electricity generation, knowing that each country relies on a particular energy mix (nuclear, solar, hydro, gas, coal, etc). Moreover, each country may import/export electricity with its neighbors through dynamical markets, like in Europe. These various elements make quite complex the modelisation of electricy price in a given country.

## Challenge goals
The aim is to model the electricity price from weather, energy (commodities) and commercial data for two European countries - France and Germany. Let us stress that the problem here is to explain the electricity price with simultaneous variables and thus this is not a prediction problem.

More precisely, the goal of this challenge is to learn a model that outputs from these explanatory variables a good estimation for the daily price variation of electricity futures) contracts, in France and Germany. These contracts allow you to receive (or to deliver) a given amount of electricity at a specified price by the contract delivered at a specified time in the future (at the contract's maturity). Thus, futures contracts are financial instruments that give you some expected value on the future price of electricity under actual market conditions - here, we focus on short-term maturity contracts (24h). Let us stress that electricity future exchange is a dynamic market in Europe.

Regarding the explanatory variables, the participants are provided with daily data for each country which involve weather quantitative measurements (temperature, rain, wind), energetic production (commodity price changes), and electricity use (consumption, exchanges between the two countries, import-export with the rest of Europe).

The score function (metric) used is the [__Spearman's correlation__](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient) between the participant's output and the actual daily price changes over the testing data set sample.

Feel free to visit our [dedicated forum](https://challengedata.qube-rt.com/) and our LinkedIn page for more information about the challenge and QRT.


## Data description
We provide three csv file data sets: training inputs X_train, training outputs Y_train, and test inputs X_test.

NB: The input data X_train and X_test represent the same explanatory variables but over two different time periods.

The columns ID in X_train et Y_train are identical, and the same holds true for the testing data. 1494 rows are available for the training data sets while 654 observations are used for the test data sets.

Input data sets comprise 35 columns:

- ID: Unique row identifier, associated with a day (DAY_ID) and a country (COUNTRY),
- DAY_ID: Day identifier - dates have been anonymized, but all data corresponding to a specific day is consistent,
- COUNTRY: Country identifier - DE = Germany, FR = France,

and then contains daily commodity price variations,

- GAS_RET: European gas,
- COAL_RET: European coal,
- CARBON_RET: Carbon emissions futures,

weather measures (daily, in the country x),

- x_TEMP: Temperature,
- x_RAIN: Rainfall,
- x_WIND: Wind,

energy production measures (daily, in the country x),

- x_GAS: Natural gas,
- x_COAL: Hard coal,
- x_HYDRO: Hydro reservoir,
- x_NUCLEAR: Daily nuclear production,
- x_SOLAR: Photovoltaic,
- x_WINDPOW: Wind power,
- x_LIGNITE: Lignite,

and electricity use metrics (daily, in the country x),

- x_CONSUMPTON: Total electricity consumption,
- x_RESIDUAL_LOAD: Electricity consumption after using all renewable energies,
- x_NET_IMPORT: Imported electricity from Europe,
- x_NET_EXPORT: Exported electricity to Europe,
- DE_FR_EXCHANGE: Total daily electricity exchange between Germany and France,
- FR_DE_EXCHANGE: Total daily electricity exchange between France and Germany.

Output data sets are composed of two columns:

- ID: Unique row identifier - corresponding to the input identifiers,
- TARGET: Daily price variation for futures of 24H electricity baseload.

__The solution files submitted by participants shall follow this output data set format__, namely to contain two columns ID and TARGET, where the ID values correspond to those of the ID column of X_test. An example of submission file containing random predictions is provided - see also the notebook in the supplementary material section for the benchmark output.

## Benchmark description
The benchark for this challenge consists in a simple linear regression, after a light cleaning of the data: The missing (NaN) values are simply filled with 0's and the COUNTRY column is dropped - namely we use the same model for France and Germany.

The public score obtained with this benchmark is 15.86%. A notebook explaining the generation of the benchmark is available in the "supplementary files" section of the challenge website.
