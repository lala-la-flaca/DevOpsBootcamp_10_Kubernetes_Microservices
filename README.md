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
   chmod 400 k8s-1-32-2-do-1-nyc1-1747874609416-kubeconfig.yaml
   ```
   
   <img src="" width=800 />
   
5. Set the KUBECONFIG environment variable to the path of the configuration file.
    
   ```bash
   export KUBECONFIG=k8s-1-32-2-do-1-nyc1-1747874609416-kubeconfig.yaml  
   ```
   
   <img src="" width=800 />
   
6. Verify that the nodes are active

    ```bash
    kubectl get node
    ```
    <img src="" width=800 />

### Creating Deployment & Service for Each Microservice

1. Create a namespace named microservices to group all microservices in the cluster.

   ```bash
   
   ```
   <img src="" width=800 />
   
3. Create the deployment and service YAML file for each microservice.
4. Apply the YAML file in the microservice namespace.

   ```bash
   kubectl apply -f config.yaml -n microservices
   ```
   <img src="" width=800 />
6. Verify that all pods are running.

   ```bash
   kubectl get pod -n microservices
   ```
   <img src="" width=800/>
   
8. Verify all the services were created.

   ```bash
   kubectl get services -n microservices
   ```
   <img src="" width=800 />
   
10. Obtain the external IP of your node to access the boutique.
    ```bash
    kubectl get nodes -o wide
    ```
    <img src="" width=800 />
    
12. Navigate to DigitalOcean and modify the firewall to allow incoming internet traffic.
    
   <img src="" width=800 />
   

### Apply K8 and Security Best Practices
1. Use a fixed image version to ensure consistency across environments.

   <img src="" width=800 />
   
3. Add a livenessProbe to each microservice to monitor container health.
   
   <img src="" width=800 />
   
5. Specify the protocol for the livenessProbe. Use gRPC (developed by Google) in this case.
6. Specify the port for the livenessProbe.
7. Set periodSeconds to specify how often to check container health.
   
   <img src="" width=800 />
   
9. Add a readinessProbe to each microservice to verify when the container is ready to receive traffic.
10. Define the protocol, port, and periodSeconds for the readinessProbe.
    
   <img src="" width=800 />
   
12. For Redis, change the probe protocol from gRPC to TCPSocket. Kubelet attempts to open a socket to the container using the application port.
    
   <img src="" width=800 />
   
14. For the frontend microservice, change the gRPC probe to httpGet and specify the HTTP path. Kubelet sends an HTTP request to the specified path and port. To check the HTTP endpoint.
    
   <img src="" width=800 />
   
16. Define resource requests and limits for each microservice to manage expected and maximum resource usage.
    
   <img src="" width=800 />
   
18. Change the frontend service type from NodePort to LoadBalancer. NodePort exposes all worker nodes, while LoadBalancer provides a single entry point from the Cloud Provider. Exposing all worker nodes increases the security risks.
    
   <img src="" width=800 />
   
20. Set the number of replicas for each deployment.
    
   <img src="" width=800 />
   
22. Use labels consistently to identify and manage deployments.
    
   <img src="" width=800 />
   
      
