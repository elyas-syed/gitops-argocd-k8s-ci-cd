## Securonix App demo

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
6. Deployed on Kubernetes Cluster as Deployment with 3 Pods for high availability 
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
