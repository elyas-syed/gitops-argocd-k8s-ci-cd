# Securonix App demo

### Requirements of the App

Given the attached app.py, please do the following:
1. Write a Dockerfile to package this flask Application as a container.
2. Write the necessary Kubernetes manifests to deploy this container as a web application.
3. Incorporate a dummy URL this application would respond on.

### App Build Process

1. Created Dockerfile for the Python applicaiton
2. Tested to make sure app is working properly
3. Created Helm Charts for the Application - Helm Charts are Package Managers for Kubernetes
4. Modified the values.yaml file in Helm Chart to customize the Application parameters
5. Added Ingress and tls capabilities in values.yaml file so app can recieve a tls certificate for http/https
6. Deployed application on Google Cloud GKE Kubernetes Cluster as Deployment with 3 Pods for high availability 
```
replicaCount: 3
```
7. Also enabled Horizontal Pod Autoscaler which allows the Pods to scale from 1 to 100 if load reaches 80%
```
autoscaling:
  enabled: true
  minReplicas: 1
  maxReplicas: 100
  targetCPUUtilizationPercentage: 80
  # targetMemoryUtilizationPercentage: 80
```  

8. Created Separate dev, qa, stage, and prod version of the app with it's own domain name

* dev: https://securonix-dev.devopslearn.net/

* qa: https://securonix-qa.devopslearn.net/

* stage: https://securonix-stage.devopslearn.net/

* prod: https://securonix-prod.devopslearn.net/


# CI/CD Process Implemented

## Continous Integration Process
Application was build using Jenkins for CI
* A Jenkins job was run to build the image
* It went through Sonarqube for static analyis of code
* Once the unit test was successful the artifact was pushed to docker repository

<img width="647" alt="jenkins" src="https://user-images.githubusercontent.com/84156957/154834413-5841258e-6c4d-4dd9-a641-5e88e1cb46b0.png">


## Continous Delivery/Continous Deplopyment Process
### For CD Process ArgoCD was used to deploy the application on Kubernetes
* ArgoCD uses **GitOps** and uses the git repository as a source of truth and constantly syncs the current state wtih desired state of infrastructure
* To automate this process a multi-branch pipeline can be created that will ArgoCD to pull from git repository and deploy to multiple enviornments
* Application was deployed with multiple pods for high availability 
 
<img width="647" alt="Screen Shot 2022-02-20 at 12 19 05 AM" src="https://user-images.githubusercontent.com/84156957/154834470-38e4c967-9d74-4a1b-bd6d-1395ae651ed0.png">

## ArgoCD was used to automate the CD process and deploy directly on Kubernetes

<img width="1512" alt="Screen Shot 2022-02-20 at 12 17 26 AM" src="https://user-images.githubusercontent.com/84156957/154834447-98f76e82-fd51-483f-a06e-7eb7b04903db.png">

## Overview of ArgoCD Deployment on Kubernetes 

<img width="1025" alt="Screen Shot 2022-02-20 at 2 43 32 AM" src="https://user-images.githubusercontent.com/84156957/154835090-b59563c4-91ea-4ae2-8398-ff1327bd7535.png">


## Summary
* Google Cloud GKE Clusters were used to minimize the cost
* Helm Charts were used to simplify the deployment of application on Kubernetes Clusters
* Another automated way to deploy applicaiton was implemented with CI/CD
* Jenkins was used for CI to build the artifact and push it to docker hub
* ArgoCD and GitOps methodology was used for CD process and application was deployed in automated fashion directly on Kubernetes Clusters


### Tree structure of Directory
```
├
├── application.yaml
├── argocd
│   ├── deployment.yaml
│   └── service.yaml
├── docker
│   ├── app.py
│   ├── Dockerfile
│   ├── LICENSE
│   ├── README.md
│   └── requirements.txt
├── hello-world-dev
│   ├── Chart.yaml
│   ├── templates
│   │   ├── deployment.yaml
│   │   ├── _helpers.tpl
│   │   ├── hpa.yaml
│   │   ├── ingress.yaml
│   │   ├── NOTES.txt
│   │   ├── serviceaccount.yaml
│   │   ├── service.yaml
│   │   └── tests
│   │       └── test-connection.yaml
│   └── values.yaml
```

