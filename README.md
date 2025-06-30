# Auto-Features-vs-Pricing
My customers are used car dealers. The question they are asking is what characteristics of used cars increase the prices of cars? The assumption is that the sale of a higher priced car nets more money for a used car dealer. There is the risk that this may not be true. 
The data used are based on a Kaggle dataset of used cars (www.kaggle.com)
# Dataset
The dataset is too large to upload to git. Any data should be placed in data/vehicles.csv to be read by the code or the code can be modified.
# Data cleaning
The VIN (vehicle identification number) contains a lot of information about a car not included in the dataset. VIN numbers varied depending on the manufacturer before 1981.
I dropped rows before 1981 to allow use of the VIN. Used car dealers are not likely to see many cars that old unless they specialize in classic cars. That is an entirely different market. I split the VIN into its components and created features from these. 
When text was converted to numbers to allow correlation calculations, I dropped the text columns, region, model, and state. State and region would be relevant to specific used car dealers and could be selected on an individual basis. There are too many models to use one-hot encoding. They could certainly be useful if the categories were narrowed. 
Assigning numeric values to the values in some of the features may have introduced bias but prevented the need for exploding the number of features using one-hot encoding. This could be explored further to test for bias.
I also made the assumption that all cars have some value, even if it is as scrap. This may be incorrect. Note that the y-intercept (price axis) is below $0. For instance, there may be a cost to getting rid of a scrap vehicle. 
# Correlations of features with price
All the features have some correlation with price. The features with the highest correlation with price in order from highest to lowest are year, diesel fuel, gas fuel, front wheel drive, 8 cylinders, 4-wheel drive. Year is also correlated with the odometer reading (0.5), which is not surprising. The other features are also of value. The full list, in order follows. This is the order in which to evaluate a car for purchase to resell, keeping in mind that the order may be different if the state and region are taken into account. For instance, Californians may prefer electric cars (cylinders#_0.0) while 4-wheel drive may be preferable in the frozen north. 
year
fuel_diesel
fuel_gas
drive_fwd
cylinders#_8.0
drive_4wd
cylinders#_4.0
odometer
transmission_other
transmission_automatic
drive_rwd
condition#
cylinders#_5.0
transmission_manual
fuel_hybrid
cylinders#_6.0
title_status#
fuel_electric
cylinders#_3.0
fuel_other
cylinders#_10.0
cylinders#_0.0
# Modeling
Year appears curved relative to price. Degree 3 produces better statistics than degree 2. However, if fit_intercept=True, linear produces the best statistics. It would be good to try some different year cutoffs because the data are starting to show the effects of the pricing of classic cars. 
The RMSE is over $9000 with just the most relevant features. This is a large error. The error is reduced to a little over $8000 if all the data are used. Running data by a state and region should help improve the statistics. Using the models of cars should also help but this feature may need further cleaning.
# Evaluation and next steps
The information a used car dealer needs to know is mainly what features are most relevant to pricing. As noted above, these are year, diesel fuel, gas fuel, front wheel drive, 8 cylinders, 4-wheel drive. Better recommendations could be given if the state and region were known. A current dataset would be needed to predict pricing for a given car.
