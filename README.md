# ☸️ Kubernetes
## 📦 Demo 5: 
This project is part of the **Kubernetes Module** from the **TWN DevOps Bootcamp**. It demonstrates how to deploy a microservices-based application architecture into a Kubernetes cluster using **YAML files** for services, deployments, and configurations with production and security best practices. In this Demo we are going to use the Online Boutique example from Google.

## 🚀 Technologies Used
- **Kubernetes (minikube)**: Container orchestration.
- **REDIS**: In-memory database.
- **DigitalOcean**: Cloud-managed K8s.
- **Linux**: Environment for CLI.
- **YAML**: Resource definitions.
- **kubectl**: CLI
  
## 📋 Prerequisites
- Ensure minikube is running.
- Ensure you have a Digital Ocean account.
- Kubectl is installed and configured to connect to your cluster.
- Docker is installed for building container images.


## 🎯 Features

- Create a K8 manifest for Deployments and Services for all microservices of an online shop application.
- Deploy microservices to DigitalOcean managed Kubernetes cluster.
- Apply best practices.

## 🏗 Project Architecture

<img src=""/>

## ⚙️ Project Configuration
1. The Online Boutique is available 
   [Online Boutique](https://github.com/GoogleCloudPlatform/microservices-demo)
2. Download the YAML example

### Setting Up a Kubernetes Cluster Using DigitalOcean K8 Engine
1. Sign in to DigitalOcean and create a Kubernetes cluster.

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_DO_MongoDB/blob/main/Img/1%20creating%20k8%20digitalocean.png" width=800 />
   
2. Configure the cluster by specifying the node pool name, data center region, cluster capacity, and adding three nodes.
   
   <img src="" width=800 />
   
3. Download the cluster configuration file in the Overview section of the cluster configuration.
   
   <img src="" width=800 />
   
4. Update the file permissions to read-only.

   ```bash
   chmod 400 
   ```
   
   <img src="" width=800 />
   
5. Set the KUBECONFIG environment variable to the path of the configuration file.
    
   ```bash
   export KUBECONFIG=k8s-1-32-2-do-1-nyc1-1746734593185-kubeconfig.yaml   
   ```
   
   <img src="" width=800 />
   
6. Verify that the nodes are active

    ```bash
    kubectl get node
    ```
    <img src="" width=800 />

### Creating Deployment & Service for Each Microservice

1. Create a namespace named microservices to group all microservices in the cluster.
2. Apply the YAML file in the microservice namespace.
3. Verify that all pods are running.
4. Verify all the services created.
5. Obtain the external IP of your node to access the boutique.
6. Navigate to DigitalOcean and allow incoming internet traffic.

### Apply K8 and Security Best Practices
1. Use a fixed image version to ensure consistency across environments.
2. Add a livenessProbe to each microservice to monitor container health.
3. Specify the protocol for the livenessProbe. Use gRPC (developed by Google) in this case.
4. Specify the port for the livenessProbe.
5. Set periodSeconds to specify how often to check container health.
6. Add a readinessProbe to each microservice to verify when the container is ready to receive traffic.
7. Define the protocol, port, and periodSeconds for the readinessProbe.
8. For Redis, change the probe protocol from gRPC to TCPSocket.
9. For frontend microservice, change the gRPC probe to httpGet and specify the HTTP path.
10. Define resource requests and limits for each microservice to manage expected and maximum resource usage.
11. Change the frontend service type from NodePort to LoadBalancer. NodePort exposes all nodes, while LoadBalancer provides a single entry point.
12. Set the number of replicas for each deployment.
13. Use labels consistently to identify and manage deployments.
      
