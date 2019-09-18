

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
git clone git@github.com:ivanjankovic/cloud-developer-p3.git
cd cloud-developer-p3
```

## Run App Localy in a Container:

#### Create Images & Containers:

#### build images:
```
cd docker
docker-compose -f docker-compose-build.yaml build
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
cd kubernetes
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

## Clean Up:

```
kubectl delete -f deployment
cd kubernetes
kubeone reset config.yaml --tfjson tf.json
terraform destroy
docker system prune -a
```

[Project Rubric]()  
[Starter Repository]()
[Cost & Uasge][2]




[1]:https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#convert-your-secret-data-to-a-base-64-representation
[2]:https://console.aws.amazon.com/cost-reports/home?#/custom?groupBy=Service&hasBlended=false&hasAmortized=false&excludeDiscounts=true&excludeTaggedResources=false&timeRangeOption=Custom&granularity=Daily&reportName=&reportType=CostUsage&isTemplate=true&startDate=2019-08-01&endDate=2019-09-17&filter=%5B%7B"dimension":"RecordType","values":%5B"Refund","Credit"%5D,"include":false,"children":null%7D%5D&forecastTimeRangeOption=None&usageAs=usageQuantity&chartStyle=Stack
