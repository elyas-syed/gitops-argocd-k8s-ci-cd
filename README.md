## Securonix App demo

### Requirements of the App

Given the attached app.py, please do the following:
1. Write a Dockerfile to package this flask Application as a container.
2. Write the necessary Kubernetes manifests to deploy this container as a web application.
3. Incorporate a dummy URL this application would respond on.

### App Build Process

1. Created Dockerfile for the Python applicaiton
2. Tested to make sure app is working properly
3. Create Helm Chart for the Application
4. Modified the values.yaml file to customize the App Details
5. Added Ingress and tls capabilities in value.yaml file so app can recieve a tls certificate
6. Deployed on Kubernetes Cluster as Deployment with 3 Pods for high availability 
7. Created Separate dev, qa, stage, and prod version of the app with it's own domain name



### Tree structure of Directory
```
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