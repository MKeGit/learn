To begin training our machine-learning model, we'll start by teaching the computer what parts of the data to look at to make predictions. We know that the column we want the model to predict is the "Launched" column. We'll extract this column and store it in a variable as a list of `Y` and `N`.

## Further data cleansing

Next, we'll remove some of the columns that aren't needed for making this prediction. Columns like "Name" give us more context about the data, but the name of a launch doesn't indicate if weather will cause the launch to be postponed. In this module, we'll focus on the columns for wind speed, conditions, and precipitation.

> [!NOTE]
> We don't typically recommend variable names like `x` and `y`, but they're norms used in data science to represent input and output data. This usage is based on the grounding in mathematical algorithms. For example, you might remember formulas like *y=mx+b*.

In the Jupyter Notebook (*.ipynb* file) you created in the previous module, run the following commands. If too much time has passed since you ran through the steps in that module, you might get errors. In that case, reimport the libraries and data from the previous module and then run the commands:

```python
# First, we save the output we are interested in. In this case, "launch" yes and no's go into the output variable.
y = launch_data['Launched?']

# Removing the columns we are not interested in
launch_data.drop(['Name','Date','Time (East Coast)','Location','Launched?','Hist Ave Sea Level Pressure','Sea Level Pressure','Day Length','Notes','Hist Ave Visibility', 'Hist Ave Max Wind Speed'],axis=1, inplace=True)

# Saving the rest of the data as input data
X = launch_data
```

You now have two variables. The output is in `y`, and the input is in `X`. You can see an overview of the input data by looking at the columns in the newly created `X` variable:

```python
# List of variables that our machine learning algorithm is going to look at:
X.columns
```

The `X` input data represents the weather for a particular day. In this case, we aren't worried about the date or time. We want the weather profile for that day to indicate whether a launch should happen, not the date or time.
