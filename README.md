

Setup:
- Required
- AWS CLI
- Docker
- Kubectl
- KubeOne

Required Accounts:
- Amazon Web Services
- DockerHub

Get Repository:

```
git clone
cd into repository folder
```

## Run App Localy in a Container:

#### Create Images & Containers:

#### build images:
```
cd docker-images
docker-compose -f docker-compose-build.yaml build --parallel
docker images
```

start app locally:
```docker-compose up```

access app:
```http://localhost:8100```

stop app: `docker-compose down`

#### push images to DockerHub:
```
docker-compose -f docker-compose-build.yaml push
```  

## Run App on Cloud - App Container Kuernetes Cluster AWS:

#### Provisioning:
```
cd terraform-kubeone
terraform init
terraform plan
terraform apply
terraform output -json > tf.json
```

#### Cluster Setup:
```
kubeone config print > config.yaml
kubeone install config.yaml --tfjson tf.json
export KUBECONFIG=$PWD/<cluster_name>-kubeconfig
kubectl get nodes
kubectl get -n kube-system machinedeployment
kubectl scale -n kube-system machinedeployment/<name> --replicas=2
```

#### Deployment:

```
kubectl apply -f deployment
```

port forward:
```
kubectl port-forward service/reverseproxy 8080:8080
kubectl port-forward service/frontend 8100:8100
```

access app:
```
http://localhost:8100
```

resaurces:  
[Convert your secret data to a base-64 representation][1]

## CI/CD:

CI/DC, Github & Code Quality:
The project demonstrates an understanding and use of CI/CD and Github
All project code is stored in a GitHub repository
The README file includes an introduction how to setup project
It explains the main building blocks
The student uses a CI tool to build the application.
A CD tool is in place to deploy new version of the app automatically to production.
A link to the repository has been provided for reviewers.

make sure you remove secrets and env variables before submission

[Project Rubric]()  
[Starter Repository]()

[1]:https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#convert-your-secret-data-to-a-base-64-representation
