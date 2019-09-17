

Setup:
- Required
- AWS CLI
- Docker
- Kubectl
- KubeOne

Required Accounts:
- Amazon Web Services
- DockerHub

### Run App Localy in Container:


Get Repository:
```

git clone
cd into repository folder

```

#### Create Images & Containers:

build images:

```
cd docker-images
docker-compose -f docker-compose-build.yaml build --parallel
docker images
```

start app locally:

```
docker-compose up
```

access app:

```
http://localhost:8100
```

stop app:

```
docker-compose down
```

push images to DockerHub:

```
docker-compose -f docker-compose-build.yaml push
```

Docker image can be build
The app can be containerized
Docker-compose file available for running containers locally
Screenshot of the terminal running containers
The applications runs in a container without errors
All services are connecting properly with S3 and DB
There are instruction on how to upload images
The project images are available on DockerHub
Screenshot of images in DockerHub

Provisioning & Nodes Cluster Setup:
terminal:
cd terraform-kubeone
terraform init
terraform plan
terraform apply
terraform output -json > tf.json
kubeone config print > config.yaml
kubeone install config.yaml --tfjson tf.json
export KUBECONFIG=$PWD/<cluster_name>-kubeconfig
kubectl get nodes
kubectl get -n kube-system machinedeployment
kubectl scale -n kube-system machinedeployment/<name> --replicas=2

Deployment:
info:
Convert your secret data to a base-64 representation
terminal:
kubectl apply -f deployment
kubectl port-forward service/reverseproxy 8080:8080
kubectl port-forward service/frontend 8100:8100
access app:
http://localhost:8100

The application runs on a cluster in the cloud
The project can be deployed to a kubernetes cluster
how to deploy to a kubernetes cluster

The app can be upgraded via rolling-update
The students can deploy a new version of the application without downtime
how do i test this, how do show this

A/B deployment of the application
Two versions of the same app can run at the same and service traffic
how do i test this, how do show this

Monitoring
The application is monitored by Amazon CloudWatch
how do i test this, how do show this

CI/DC, Github & Code Quality:
The project demonstrates an understanding and use of CI/CD and Github
All project code is stored in a GitHub repository
The README file includes an introduction how to setup project
It explains the main building blocks
The student uses a CI tool to build the application.
A CD tool is in place to deploy new version of the app automatically to production.
A link to the repository has been provided for reviewers.

make sure you remove secrets and env variables before submission

Project Rubric
Starter Repository
```
