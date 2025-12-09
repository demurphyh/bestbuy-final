# Lab Project: Cloud-Native App for Best Buy

## Architecture Diagram

![Architecture Diagram](image.png)

## Brief Overview

This application is a containerized microservices application consisting of 7 microservices.

- Store Front(Vue.js): Store front is a front-end application weher customers can browse and place orders for various tech products.
- Store Admin(Vue.js): Store admin the the employee facing web application that is used to view and confirm orders.
- Order Service(Node.js): Order service manages customer orders and interacts with RabbitMQ for order queuing.
- Product Service(Rust): Product service handle the hard-coded product listings and lists information about them.
- Makeline Service(GO): Makeline service processes the orders after they are accepted and transfers them to MongoDB.
- RabbitMQ: RabbitMQ is a message broker that is used to queue orders for processing.
- MongoDB: MongoDB is used to store accepted orders.

## Deployment Instructions

### Step 1 - AKS Cluster

Create an AKS Cluster on the Azure portal with at least one worker node.

Connect to the AKS Cluster

In the overview page, click on Connect.

Select Azure CLI tap. You will need Azure CLI. If you don't have it: Install Azure CLI

Login to your account using

`az login`

Set the cluster subscription using the command shown in the portal (it will look something like this):

`az account set --subscription 'subscribtion-id'`

Copy the command shown in the portal for configuring kubectl (it will look something like this):

`az aks get-credentials --resource-group AlgonquinPetStoreRG --name AlgonquinPetStoreCluster`

### Step 2 - ConfigMaps

Deploy the ConfigMap for RabbitMQ

`kubectl apply -f config-maps.yaml`

Verify the ConfigMap deployment

`kubectl get configmaps`

### Step 3 - Deploy the Application

`kubectl apply -f cloudnative-deployment.yaml`

Verify Deployment

`kubectl get pods`

`kubectl get services`

## Links Table

[Youtube Link](https://youtu.be/2qjZN3uunJQ)

|  Service | Docker Image   |
|---|---|
|  [Store-front](https://github.com/demurphyh/store-front-final) | [Store-front](https://hub.docker.com/repository/docker/desmurp/store-front-final/general)  |
| [Store-admin](https://github.com/demurphyh/store-admin-final)  |  [Store-admin](https://hub.docker.com/repository/docker/desmurp/store-admin-final/general) |
|  [Product-service](https://github.com/demurphyh/product-service-final) | [Product-service](https://hub.docker.com/repository/docker/desmurp/product-service-final/general)  |
| [Makeline-service](https://github.com/demurphyh/makeline-service-final)| [makeline-service](https://hub.docker.com/repository/docker/desmurp/makeline-service-final/general) |
| [Order-service](https://github.com/demurphyh/order-service-final)| [Order-service](https://hub.docker.com/repository/docker/desmurp/order-service-final/general) |
