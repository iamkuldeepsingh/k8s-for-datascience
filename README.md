# K8s-for-datascience

# Requirements for this exercise to have working Docker and Kubernetes setup, For local setup refer below details

Docker https://www.docker.com/products/docker-desktop 

Minikube https://kubernetes.io/docs/tasks/tools/install-minikube/

# The entire exercise has been broken into 4 parts
## Docker
 - Once cloned the repo, cd k8s-for-datascience/docker
 - docker run -d -p 8080:8080 -v `pwd`:/home gcr.io/deeplearning-platform-release/tf2-cpu.2-0
 - Access the notebook on localhost:8080 and Run all the notebook steps
 - For extending image check Dockerfile and build the image with any other name
 - For verification purpose we will use already uploaded image kduhan/tf2-mxnet-custom as image is very large
## K8s
  - cd ../k8s/
  - Run kubectl create -f k8s.yml
  - Once pod is up run kubectl port-forward pods/dlc-tf 8080:8080
  - Access the notebook on localhost:8080 and you can use the earlier notebook to verify it
  - Clean it up using kubectl delete -f k8s.yml
  
## Scaling/Distribution
For Dask Distibution Test
  - cd ../distributed/dask/
  - Run kubectl create -f dask.yml
  - Once both Scheduler and workers are up, Test Scaling by 2 kubectl scale deployment daskd-worker --replicas=2
  - Clean it up using kubectl delete -f dask.yml
  
For Tensorflow Distibution Test
  - cd ../tf
  - Run kubectl create -f pv.yml; kubectl create -f master.yml; kubectl create -f worker0.yml; kubectl create -f worker1.yml
  - Once both master and workers are up, go to localhost:8888 and run the notebook it will run on two workers
  - Run kubectl create -f tensorboard.yml and access the localhost:6006 to check the graphs
  - Clean it up using kubectl delete -f tensorboard.yml; kubectl delete -f worker1.yml; kubectl delete -f worker0.yml; kubectl delete -f master.yml; kubectl delete -f pv.yml

## Kubeflow (Extra bonanza offer as it was not planned earlier)
  - Single Click Notebook server
  - Single View for entire ML/AI workload
  - Pipeline for Complex workflow
  - Versioning and Deployment on K8s
  - Hyperparameter Tuning
  
 This will be shown at preconfigured machine and information will be shared on how to setup
  
