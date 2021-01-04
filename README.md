# Operationalizing Machine Learning

This project is part of the Udacity Azure ML Nanodegree. In this project, we first learn to deploy the best model of an AutoML run, enable insights on, create documentation for and consume the resultant endpoint. Additionally, we also create, publish and consume a machine learning pipeline with an AutoML step using the Python SDK for Azure.

## Architectural Diagram
![Architectural Diagram](pictures/architecture.png)

## Key Steps

### Creating the Auto ML Model
First, we upload and register the Bank Marketing dataset on the Azure ML studio. 
![BankMarketing Dataset](pictures/dataset.png)
![Registered Dataset](pictures/registered-dataset.png)

Then, we proceed to initialize an AutoML run for building a classifier with the primary metric as Accuracy, exit criterion 1 hour and concurrency as 5. This takes about 29 minutes to run.
![AutoML 1](pictures/automl-1.png) 
![AutoML 2](pictures/automl-2.png)

As a result of this AutoML run, the best model we get VotingEnsemble with accuracy 0.91866 and some other metrics as shown by the screenshots below.
![Voting Ensemble](pictures/voting-ensemble-1.png)
![Voting Ensemble Graph](pictures/voting-ensemble-graph-1.png)
![Voting Ensemble Graph](pictures/voting-ensemble-graph-2.png)
![Voting Ensemble Graph](pictures/voting-ensemble-graph-3.png)

### Deploying the best model
We use the Azure Container Instance deployment service of Azure ML Studio to deploy the best observed model of the AutoML run.
![Deploying Voting Ensemble](pictures/deploy-1.png)

After a while, the model is deployed and the endpoint becomes active.
![Active deployment](pictures/deploy-2.png)
![Active deployment](pictures/deploy-3.png)

### Enable logging Application Insights for Azure WebService
In order to do this, we run the ```logs.py``` file, where we update the name of the webservice to 'demo-model-deploy'.
![Logging](pictures/logs-1.png)
![Logging](pictures/logs-2.png)
![Logging](pictures/logs-3.png)

As a result of doing this, we can observe that the application insights have been enabled for this deployment.
![Logging](pictures/logs-4.png)

### Swagger Documentation
To enable swagger documentation, we first access the swagger URI from the Details tab of the deployed endpoint.
![Swagger URI](pictures/swagger-1.png)

If we visit this URI, we can find the '''swagger.json''' file. Next, we download this '''swagger.json''' to the swagger directory of the project folder.
Next, we run '''serve.py''' to serve the '''swagger.json''' on a simple HTTP server at port 8000, and swagger.sh to download the latest Swagger container, and run it on port 9000.
Once that is done, we can browse to http://localhost:9000/ to find the swagger container. Here, we enter the URL for '''swagger.json''' being served (http://localhost:8000/swagger.json) to generate documentation for our endpoint.
![Swagger URI](pictures/swagger-2.png)
![Swagger URI](pictures/swagger-3.png)
![Swagger URI](pictures/swagger-4.png)

### Consume model endpoints
To consume model endpoint, we run the '''endpoint.py''' file by modifying the scoring URI and authentication key. We get results that look like the following - 
![Consuming endpoint](pictures/endpoint.png)

**Benchmarking the endpoint**
We benchmark the endpoint using Apache bench to load-test our model. In order to do so, we execute '''benchmark.sh''' after updating the URI and and key. The results are as follows-
![Benchmarking endpoint](pictures/benchmark-1.png)
![Benchmarking endpoint](pictures/benchmark-2.png)
![Benchmarking endpoint](pictures/benchmark-3.png)
![Benchmarking endpoint](pictures/benchmark-4.png)

### Create and publish a pipeline
We get the same Bank Marketing Dataset and define a pipeline with an automl step for training our data. Once that is done, we publish the pipeline.
![Pipeline with AutoML Step](pictures/pipeline-1.png)
![Pipeline with AutoML Step](pictures/pipeline-2.png)
![Published Pipeline](pictures/published-pipeline-1.png)
![Published Pipeline](pictures/published-pipeline-2.png)
![Published Pipeline](pictures/published-pipeline-3.png)
![Published Pipeline](pictures/published-pipeline-4.png)
![Published Pipeline](pictures/published-pipeline-5.png)
![Published Pipeline](pictures/all-pipelines.png)

## Screen Recording
A screen recording of the project in action:
https://youtu.be/0BTFvhw0jU8

## Standout Suggestions Attempted
The project attempted to load-test the deployed model by utilizing the capabilities of Apache Benchmark.

## Future Improvements
* We can work on data cleaning, preprocessing and some feature engineering for the Bank Marketing Dataset.
* We can perform outlier detection.
* The classification AutoML task can include deep learning techniques to achieve better results.
* We can add a parallel run step to our pipeline. This might help in reducing the processing time.
