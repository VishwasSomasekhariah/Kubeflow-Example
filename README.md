# Kubeflow Pipelines
Kubeflow Pipelines is a platform for building and deploying portable, scalable machine learning (ML) workflows based on Docker containers.

The Kubeflow Pipelines platform consists of:

- A user interface (UI) for managing and tracking experiments, jobs, and runs.
- An engine for scheduling multi-step ML workflows.
- An SDK for defining and manipulating pipelines and components.
- Notebooks for interacting with the system using the SDK.

A pipeline is a description of an ML workflow, including all of the components in the workflow and how they combine in the form of a graph.

A pipeline component is a self-contained set of code that performs one step/task in your ML workflow

In this example we create a simple digit_recognizer pipeline using MNIST dataset which consists following steps/tasks,
- getting_the_data
- reshaping_the_data
- building_the_model
- serving_the_model

These steps have been individually containerized to pipeline components and can be found within ```pipeline/components```

## Getting started
Setup a complete Kubeflow on your civo cluster, simple way is to use the application available in the civo marketplace(This handles all the versioning issues and network connection issues that you may get otherwise for you).

This is tested and run on ```Kubeflow v1.6```.

Port forward istio-ingressgateway using the following command to access Kubeflow UI locally at ```localhost:8080```
```
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
```
Port forward MinIO UI using the following command to access MinIO UI locally at ```localhost:9000```
```
 kubectl port-forward svc/minio-service -n kubeflow 9000:9000
```

Create a new Notebook server in the Kubeflow UI with the specifications that you need.  
Connect to view the web interface exposed by your notebook server.  
The Jupyter notebook gives to access to Terminal, Python 3 ipykernel etc.  
From the Terminal you can clone the above repository and you should have direct access to these files locally.

Either you can make use of the ```digit_recognizer_pipeline.ipynb``` to edit any function's logic and create new pipeline components or make use of the tasks available in ```pipeline/components```.  By default the notebook uses the preexisting components to create a new experiment and run.

Once the experiment is completed you can use the ```predict.ipynb``` to see if the model that is served using kserve works or not.
