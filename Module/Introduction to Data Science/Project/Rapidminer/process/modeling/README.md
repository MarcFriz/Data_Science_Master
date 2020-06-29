# Data_Science_Master

## Data Modelling
### First step - Naive approach

Process: naivClassifier_diff_model

- Based on the given data I tested different types of model to determined which 
performs on a useable level.
- The basic assumption is that the Classification of the price (rise or fall) can 
be found in the day before. For this I do not have to consider the whole timeline 
for all attributes.

### Second step - Evaluate the Naive approach

Process: naivClassifier

- Here I used the Model with the highest accuracy to train it
for all the types of Fuel

### Third step - Time Series approach

Process: LagClassifier

- Make sure all data are preperated as needed (5 and 10 days in the past)
- Based on the Model found by the naive approach I did a hyperparameter Tuning 
with a Grid-Search:
    - Training cycles
    - learningrate
- The Grid-Searche applys to both Time Series with one type of Fuel
- After the Grid-Search the parameters are copied for the other types of Fuel


### Addition - One Station

Process: LagClassifier_one_Station

- Is the same as LagClassifier but only with the date for on Station
- Used in the Evaluation
