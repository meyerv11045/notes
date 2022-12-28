# Decision Trees

## Pros

- Easily explainable
- Highly interpretable

## cons

- low accuracy compared to other methods
- Cannot deal with additive structure (e,g. diagonal line separating classes)

# Ensemble Methods

- Used to improve the accuracy of predictions, especially with decision trees

1. Training different types of algorithms and then averaging their results
2. Training on multiple train sets from the population and then averaging their results
3. Bagging (random forrests)
4. Boosting (Adaboost, Xgboost)

- Bagging and boosting are most popular ensemble methods since the other two either require collecting more data (oftentimes infeasible) or using more algorithms

## Bagging

## Boosting

- Decreasing bias
- Additive

## Resources

- [CS 229 Lecture](https://www.youtube.com/watch?v=wr9gUr-eWdA&list=PLoROMvodv4rMiGQp3WXShtMGgzqpfVfbU&index=10)
- [Decision Tree Classifier from Scratch](https://www.youtube.com/watch?v=LDRbO9a6XPU)
    - [Code](https://github.com/random-forests/tutorials/blob/master/decision_tree.ipynb)
- [AdaBoost Ensemble in Python](https://machinelearningmastery.com/adaboost-ensemble-in-python/)
