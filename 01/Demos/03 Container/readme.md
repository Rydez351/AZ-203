# Create containerized solutions

[Docker](https://www.docker.com/products/docker-desktop)

[Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)

[Kubernetes](https://kubernetes.io/de/)

#### Create Image & Deploy to Dockerhub / Azure

Create Image `FoodUI` or `FoodApi`

`docker build --rm -f "app.prod.dockerfile" -t foodui .`

Tag the Image

`docker tag foodui arambazamba/foodui:1.1.0`

Publish to Dockerhub

`docker push arambazamba/foodui`

Publish to ACR:

Execute `create-container-reg` and:

```
docker tag foodui acr.azurecr.io/foodui:1.1.0
docker push acr.azurecr.io/foodui:1.1.0
```

### Azure Container Instances

Execute `create-container-instance.azcli`

### Web App for Container

Go to Food UI:

Build Image

```
docker build --rm -f "app.prod.dockerfile" -t foodui .
```

Run Image

```
docker run -p 8080:80 foodui
```

### AKS

[az aks Commands Overview](https://docs.microsoft.com/en-us/cli/azure/aks?view=azure-cli-latest)

[DevSpaces Intro](https://docs.microsoft.com/en-us/azure/dev-spaces/quickstart-team-development)

#### Create AKS Cluster

Install kubectl command line client locally:

`az aks install-cli`

> Note: You might need to set a path to your system env variables

Create resource group:

`az group create --name az-203 --location westeurope`

Create AKS cluster:

`az aks create --resource-group az-203 --name foodcluster --node-count 1 --enable-addons monitoring --generate-ssh-keys`

Get credentials for the Kubernets cluster:

`az aks get-credentials --resource-group az-203 --name foodcluster`

Get a list of cluster nodes:

`kubectl get nodes`

Apply the yaml

`kubectl apply -f foodui.yaml`

Get the serive IP and use it on the assigned port

kubectl get service foodui --watch

### Helm

[Helm Documentation](https://helm.sh/)

#### Installation on Windows

[Get Chocolatey](https://chocolatey.org/install)

`choco install kubernetes-helm`

#### Installation on Linux or WSL

```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

#### Using Helm

[Using Helm](https://helm.sh/docs/intro/using_helm/)

[Helm CLI Reference](https://helm.sh/docs/helm/)

Sample: https://github.com/Azure-Samples/helm-charts/tree/master/chart-source/azure-vote

List Repos

```
helm repo list
```

Install a Repo

helm install voting azure-samples/azure-vote
