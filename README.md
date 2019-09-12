# Scalable Machine Learning Pipelines with MLflow
MLflow Workshop for Strange Loop 2019

https://thestrangeloop.com/2019/scalable-machine-learning-pipelines-with-mlflow.html


## Prereqs

```
pip install mlflow
```
* Conda from https://docs.conda.io/en/latest/miniconda.html
* Docker https://docs.docker.com/install/overview/

## Module 1

### Objective 
Get famailir with how an MLflow project is set up

We will be going through the wine-quailty example (mlflow/examples/sklearn_elasticnet_wine/) which attempts to create a model that can predict the quilty of wine given
input features.

For this module we will...
* Look through data for our experiment
* Update  our MLflow project with new metrics and parameters
* Use the MLflow tracking UI to track our experiments

#### Steps

0. Clone mlflow repo
https://github.com/mlflow/mlflow

https://www.mlflow.org/docs/latest/tutorial.html


1. Observe our Data

The data we will be working with is in the wine-quailty.csv file which contains 11 features, we will be trying to predict quailty based on the other 10 features.


2. Update Metrics and Parameters

We will be updating train.py as well as the MLflow project file, currently random_state is hard coded to 42, and is not being tracked. These kind aof decisons can be lost in expertimentation and we would like to track this variabile.

Guidelines

*  Update code to generate a random number for each test run
*  Add a new random_state hyperparamter to your ElasticNet
*  update MLproject with the random_state hyperparamter
*  Add a MLflow metric for random seed as well.


3. Make Models

Can you make script to do random runs?
Do 100 runs which variables gave you the least MAE and RMSE?

View all your experiments using the Tracking UI

```
mlflow ui
```

## Module 2

### Objective 
A key componet of MLflow is reproducibility, in order to verify that you will be running someone elses MLflow project.

#### Steps

1. Running experiment from github  

In order for someone else to run your experiment, we will need to push it to github, we will follow these steps..

* package your code like https://github.com/mlflow/mlflow-example
* push your code to github
* run someone elses project 

```
mlflow run git@github.com:mlflow/mlflow-example.git -P alpha=0.5
```

Can you run 5 other experiments? View the results in Tracking UI

2. Running experitment in a Docker image

Not only can we package experiments in github, we can containerize the entrie process for mass reproducibility 

* Can you update your MLflow project to match thier docker example?

https://github.com/mlflow/mlflow/tree/master/examples/docker

* Can someone else build and run your Docker image?


## Module 3

### Objective 
MLflow gives us an easy way to provide an endpoint for our model to give live predictions. In this module we will stand up a server to accept REStful post requests to provide an output.

#### Steps

1. Make REST endpoint to hit your service

```
mlflow models serve --model-uri runs:/RUN_ID/model --no-conda
```


2. Send request

Heres an example request

```
curl -X POST -H "Content-Type:application/json; format=pandas-split" --data '{"columns":["alcohol", "chlorides", "citric acid", "density", "fixed acidity", "free sulfur dioxide", "pH", "residual sugar", "sulphates", "total sulfur dioxide", "volatile acidity"],"data":[[12.8, 0.029, 0.48, 0.98, 6.2, 29, 3.33, 1.2, 0.39, 75, 0.66]]}' http://127.0.0.1:5000/invocations
```

3. Deploy in Docker container

To deploy to the cloud we can dockerize our model endpoint, follow guidance from their documentation 
https://www.mlflow.org/docs/latest/models.html#deploy-a-python-function-model-on-amazon-sagemaker


## Free time

Some other MLflow projects to play with

https://github.com/mlflow/mlflow/tree/master/examples/flower_classifier
https://github.com/mlflow/mlflow/tree/master/examples/multistep_workflow


Can you update exisiting projects to use MLflow? Try some of these

https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/tutorials/mnist
https://github.com/kristpapadopoulos/house-price-predictions/blob/master/3-Boston-RTL-Regularization.py
https://github.com/tensorflow/models/tree/master/tutorials/image/cifar10




