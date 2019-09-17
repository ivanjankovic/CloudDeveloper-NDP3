

Setup:
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

start app:
```
docker-compose up
```

access app:  
[http://localhost:8100](http://localhost:8100)

stop app:
```
docker-compose down
```

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
[http://localhost:8100](http://localhost:8100)

resaurces:  
[Convert your secret data to a base-64 representation][1]

## CI/CD:


[Project Rubric]()  
[Starter Repository]()

[1]:https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#convert-your-secret-data-to-a-base-64-representation
