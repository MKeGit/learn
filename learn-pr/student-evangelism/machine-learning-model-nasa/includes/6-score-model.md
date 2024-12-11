Doing a simple comparison of percentage of data that resulted in a `Y` launch is useful for checking if the model is close to correct, but it's even more useful to actually score the model. 

## Score the model

As with an exam, you can measure learning with a score. There's a one-line function you can call to see how correct the model was at predicting whether a launch would happen.

```python
# Calculate accuracy
tree_model.score(X_test,y_test)
```

Using the `score()` function, you pass in the `X_test` input data and the `y_test` output data to "grade" the model. The higher the score, the better our model is at predicting the outcome of a rocket launch based on weather data.

## Understand the score

The model in this example is 98.3% correct, which is good. In fact, with the small amount of data cleansing and manipulation we did and with the known issues of the data, it seems a little *too* good.

Perhaps we have the best data and correctly trained our model to be so precise. But maybe this accuracy rate means we're good at guessing this partially manufactured data, so this score wouldn't be reliable in the real world. For context, 70% accuracy with a decision tree classifier (when it's run the first time) is common.

How might you ensure that the score itself is an accurate representation of how correct the model is?

One way would be to ask an expert to fill in the `Y` and `N` data for the non-launch dates instead of just guessing `N`. For example, the likelihood of the day right before or right after a launch *also* being a good day to launch is probably higher than we represented in this data.
