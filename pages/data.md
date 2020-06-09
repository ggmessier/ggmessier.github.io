---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# Data Analytics

*It’s tough to make predictions, especially about the future.*

-Yogi Berra

The primary purpose of my data analytics program is to improve the services provided to individuals living with homelessness.  As I publish work in this area, I also release the source code used to generate the published results in my data analytics [github repository](https://github.com/ggmessier/data-analytics).

## Getting Started

- [Background Material](data-background)
- [New Student Orientation](data-orientation)


## Supervised Learning

Our objective is to use an algorithm to predict the value of a *target variable* based on the values of some *input variables*.  Supervised learning has the benefit of having access to a *training set* where we have $M$ samples of the input variables that are associated with $M$ target variable values.  This data set is used to train the parameters of the algorithm in order to minimize the error between the algorithm's prediction and the target variable values in the training data. 

We can represent the input variables in the training data by the $M \times P$ matrix  $\mathbb{X} = [\ \mathbb{X}_1 \ldots\ \mathbb{X}_P\ ]$, where $P$ is the number of data features.  The $i$th training sample corresponds to the $i$th row in $\mathbb{X}$ and can be represented by the $P$ element vector $\mathbb{x}_i = [\ x\_{i1} \ldots x\_{iP}\ ]$.  The target variable values are contained in the $M$ element column vector $\mathbb{Y} = [\ y_1 \ldots y_M\ ]^T$.


In some cases, the target variable takes on continuous values, in which case we are solving a *regression* problem.  If the target variable is drawn from a discrete set of values or involves making a choice, then we are solving a *classification* problem.

As an example, when creating a fantasy baseball team, we might be interested in determining how many games a major league baseball player will likely play in a season.  The more games played, the greater the impact of the player on our team.  Our training set could be derived from the 2018 season where $M$ is the number of players.  If the features in our data consist of the number of hits and number of outs for each player, then $P=2$.  Even though a player can only play an integer number of games, we would still consider this a regression problem.


## Over-fitting, Under-Fitting and Cross-Validation

During training, we adjust the parameters of our algorithm or system model to minimize the difference between the model predicted values and the target variable values in the training data.  This is known as training error.  *Generalization error* refers to the error between the model prediction and target variable for data outside of the training set.

*Over-fitting* refers to the risk of creating an overly specialized model that does a great job of minimizing training error by matching the dataset exactly at the cost of increasing generalization error.  This can be avoided by using *cross validation* where the model is trained only on a portion of the training set and evaluated using the data excluded from training.


A very simple model with few parameters (ie. a best fit line) will tend to underfit most data sets and will result in high training and generalization error.  An underfit estimator is said to suffer from *bias*.  As complexity is increased, $h(x)$ will do a better job of fitting the training data and training error will decrease.  However, $h(x)$ may reach a point where it starts to exhibit *variance* where it begins to fit to small or random fluctuations in the training data.  Over-fitting causes generalization error to increase for high levels of model complexity.


## Model Selection

Model selection refers to choosing the appropriate algorithm and the parameters of that algorithm to achieve the best possible performance and the right balance between over-fitting and under-fitting.  In Andrew Ng's lectures, he gives the pragmatic advice to start with simple algorithms first and to add complexity in a very gradual and controlled way.  These are the steps:

1. Choose your regression or classification algorithm.
2. Select data features and model complexity:
  - If you have a lot of features in your raw dataset, you may want to perform some simple correlation coefficient calculations to determine which subset are most tightly connected to the target variable.
  - Some models operate on mathematical variations of the raw data (features raised to an exponent, kernel functions, etc.) and increasing the complexity of these operations can sometimes improve the fit to the training data.
3. Evaluate training error and generalization error using cross-validation.
4. Repeat Steps 2-3 with more features and increasing complexity.  Terminate when we identify the model complexity/data feature combination that minimizes generalization error.

It should be noted that many machine learning algorithms have specialized algorithms for model selection.  Linear/logistic regression will naturally produce smaller coefficients for features that have less influence over the target variable.  Neural networks will also naturally focus on the data features that are most relevant.  In general, the feature selection and dimensionality reduction families of algorithms also attempt to find the most relevant data features for a particular problem.


## Algorithms

#### Linear Regression

The `Games Played Linear Regression` notebook in the `baseball\notebooks` folder demonstrates the use of linear regression to predict the number of games played in a season by a major league basball player.  Coefficients are calculated directly from the least squares solution and the z-score statistical significance test is applied to the coefficient values.  Randomized hold-out cross-validation is used to calculate training and generalization error.  The sci-kit learn library is also used as a baseline and to illustrate how regularization techniques can be used to simplify the linear regression model.

#### Logistic Regression

The `Games Played Logistic Regression` notebook in `baseball\notebooks` demonstrates how to use the scikit-learn libraries to perform binary classification on two different data sets.  Regularization is explored and the different metrics used to evaluate the performance of a binary classification algorithm are introduced.


















