# Scalable Machine Learning Pipelines with MLflow
MLflow Workshop for Strange Loop 2019

https://thestrangeloop.com/2019/scalable-machine-learning-pipelines-with-mlflow.html


## Prereqs

pip install mlflow
install conda
or can use our custom docker image

## Module 1

Look at wine-quailty.csv
Lets see code... train.py

currently random_state is hard coded to 42, and is not being tracked
lets update code to generate a random number

- comment out or change random seed
- pass in random_state to ElasticNet
- update MLproject with random_state
- mlflow log metric for random seed

Can you make script to do random runs?
Do 100 runs which variables gave you the least MAE and RMSE?

Run Tracking UI

```
mlflow ui
```

## Module 2

Encourage colab, run someone elses project

1  package your code like https://github.com/mlflow/mlflow-example
2. push to github
3. run someone elses project 

mlflow run git@github.com:mlflow/mlflow-example.git -P alpha=0.5


## Module 3

Make REST endpoint to hit your service

```
mlflow models serve --model-uri runs:/RUN_ID/model --no-conda
```

Send request

```
curl -X POST -H "Content-Type:application/json; format=pandas-split" --data '{"columns":["alcohol", "chlorides", "citric acid", "density", "fixed acidity", "free sulfur dioxide", "pH", "residual sugar", "sulphates", "total sulfur dioxide", "volatile acidity"],"data":[[12.8, 0.029, 0.48, 0.98, 6.2, 29, 3.33, 1.2, 0.39, 75, 0.66]]}' http://127.0.0.1:5000/invocations
```

## Free time

extra creds

https://github.com/mlflow/mlflow/tree/master/examples/multistep_workflow

