# ff-battery-soh-prediction-training
This project showcases the steps for the data pre-processing and model training based on the synthetic data simulating the State of Health (SOH) degradation of electric vehicle batteries over time under certain conditions.

# Step 1: Process raw data

These dataset were imported from a project that generated synthtic battery data. 

For more details about the battery simultor service and customization, check out the link below: 

 https://github.com/FIWARE-EdgeAI-Project/ff-battery-synthetic-data-generator/tree/main


### Context about raw data: EVs Battery simulation scenarios

The data is generated for six different scenarios:

- Normal usage, optimal charging
- Normal usage, full charging
- Normal usage, frequent top-ups
- Normal usage, deep discharge
- High usage, optimal charging
- Low usage, optimal charging

Files are named according to the pattern: 

`{usage}_usage_{charging}_charging_battery_data.csv`

### Implmentation: 

All the steps for the raw data processing can be found in this [Notebook](notebooks/0_concat_datasets.ipynb)


# Step 2: Feature engineering & base model training. 

The next steps considers the results from the previous notebook "0_contact_datasets.ipynb" which purpose was to combine the datasets which were in raw format and the resulting dataframe has additional columns about the battery usage and charging modes that were categorically encoded. 

### Explanation of the new features:
- **Temperature_Optimal**: Binary indicator for optimal temperature range (15-35°C).

- **Temperature_Extreme**: Binary indicator for extreme temperatures.

- **Temp_Deviation_Low and Temp_Deviation_High**: Measure how far the temperature is from the optimal range.

- **Season**: Categorical feature indicating the season based on the month.

- **Usage_Intensity**: Categorizes daily cycles into low, normal, and high usage.

- **Deep_Discharge**: Indicates if the battery experienced deep discharge or full charge.

- **Optimal_Charging**: Indicates if the charging was within the optimal range (20-80%).

- **Cycle_Age**: Normalized total cycles to represent the battery's age.

- **SOH_Change_Rate**: Rate of change in SOH, which can capture degradation trends.

=> These new features relate to the factors influencing SOH degradation.  
=> It captures temperature effects, usage patterns, charging behaviors, which should provide a richer set of features for the linear regression model to work with.

### Implmentation: 

All the steps for the feature engineering and Linear regression model (baseline model) training can be found in this [Notebook](notebooks/1_feature_engineering_training.ipynb)



