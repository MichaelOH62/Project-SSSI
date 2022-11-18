# Project-SSSI
Project for CS301 F22
Project Members: Michael O'Hanlon & Adira Samaroo

For this project we will be using the repository under Adira S.'s GitHub account. We are using Google Colab for the environment of the project.

<h1>Hyperparameter Optimization:</h1>

A hyperparameter is a component of a model that can be thought of as a knob on a radio. It needs to be turned and adjusted with a certain level of precision in order to achieve the optimal results. To find the optimal values of these hyperparameters, hyperparameter optimization is used. Simply put, it is a process used to improve the performance of a machine learning model by finding the optimal values of the model’s hyperparameters.

There are many different algorithms that can be used to achieve hyperparameter optimization, in our case we used the GP Tuner or Gaussian Process, a sequential model-based optimization (SMBO) approach with Gaussian Process as the surrogate, which requires two steps, loss function estimation and an acquisition function used to guide the search for the optimizer. 

![Milestone3BayesianOptimization](https://github.com/adiraCode/Project-SSSI/blob/milestone-3/pictures/Milestone3BayesianOptimization.png?raw=true)

The optimization model constructs a posterior distribution of functions akin to the Gaussian Process. The functions are constructed with the intention of being the best representation of the function that is being optimized. The posterior distribution improves as the number of observations increases, and the tuner is able to choose which regions in the parameter space are worth searching with more accuracy.

![Milestone3PosteriorAcquisition](https://github.com/adiraCode/Project-SSSI/blob/milestone-3/pictures/Milestone3PosteriorAcquisition.jpeg?raw=true)

Gaussian Processes are non-linear models that allow data to be models with a family of functions. The GP Tuner minimizes or maximizes the amount of steps required to find a combination of parameters that are close to the optimal combination of hyperparameters. It is assumed that every data point is a normally distributed random variable and every data point is related to every other. Which means an entire dataset can be described by a multivariate normal distribution with a non-trivial covariance. Gaussian Processes are described by mean (the mean of the predictor variable for the data point) and kernell (the relationship between the data points that takes input from two data points and returns the covariance between them) functions.

However, in certain problems, it can be difficult to choose a covariance function and the hyperparameters associated with it. The method finds the maximum of the acquisition function, or proxy optimization problem, that is difficult to solve but cheaper in computation. Here we find the value of the hyperparameter that will improve either the maximum or minimum of the loss function fitted to the model. The function takes the mean and variance at each point and returns the hyperparameter value for the next run to find the potential value of each point.  This makes Bayesian Optimization is suggested for situations where sampling the function is expensive as the function evaluation is time-consuming during optimization.

To implement the tuner, we defined our search space as follows:

![search_space](https://github.com/adiraCode/Project-SSSI/blob/milestone-3/pictures/search_space.png?raw=true)

This code segment tells NNI that the hyperparameters to optimize are batch_size, epochs, and learning_rate. The possible values for the parameters are also given for NNI to choose from to determine which combination of 3 values yields the highest accuracy.
We then configured the experiment to run as follows:

![experiment_config](https://github.com/adiraCode/Project-SSSI/blob/milestone-3/pictures/experiment_config.png?raw=true)

This segment tells NNI exactly how the experiment should be run to fit our needs, including the specification of using GPTuner, as well as the number of trials to run.

<h2>Sources:</h2>
https://github.com/fmfn/BayesianOptimization

https://nni.readthedocs.io/en/latest/reference/hpo.html#nni.algorithms.hpo.gp_tuner.GPTuner

https://proceedings.neurips.cc/paper/2012/file/05311655a15b75fab86956663e1819cd-Paper.pdf

https://towardsdatascience.com/bayesian-optimization-or-how-i-carved-boats-from-wood-examples-and-code-78b9c79b31e5

https://nni.readthedocs.io/en/latest/hpo/tuners.html

https://towardsdatascience.com/shallow-understanding-on-bayesian-optimization-324b6c1f7083

<h1>Results Obtained:</h1>

<h2>Hyperparameter Optimization Results:</h2>

*picture*

Thus, the combination that yields the highest validation accuracy is a __ for the batch_size, __ for the epochs, and __ for the learning rate.

These values were then applied to the model to see how the baseline performance has improved after running the hyperparameter optimization.

<h2>Segmented Images:</h2>

*picture*

<h2>Training and validation loss vs. epochs:</h2>

*picture*

<h2>Precision and Recall Values:</h2>

*picture*
