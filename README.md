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

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_DO_MongoDB/blob/main/Img/1%20creating%20k8%20digitalocean.png" width=500 />
   
2. Configure the cluster by specifying the node pool name, data center region, cluster capacity, and adding three nodes.
   
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/4%20create%20k8%20in%20DO.png" width=500 />
   
3. Download the cluster configuration file in the Overview section of the cluster configuration.
   
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/5%20download%20k8%20config%20file.PNG" width=500 />
   
4. Update the file permissions to read-only.

   ```bash
   chmod 400 k8s-1-32-2-do-1-nyc1-1747874609416-kubeconfig.yaml
   ```
   
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/6%20setting%20permisson%20config%20file.png" width=500 />
   
5. Set the KUBECONFIG environment variable to the path of the configuration file.
    
   ```bash
   export KUBECONFIG=k8s-1-32-2-do-1-nyc1-1747874609416-kubeconfig.yaml  
   ```
   
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/9%20configuring%20the%20micronservice%20config%20file.PNG" width=500 />
   
6. Verify that the nodes are active

    ```bash
    kubectl get node
    ```
    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/10%20get%20node.PNG" width=500 />

### Creating Deployment & Service for Each Microservice

1. Create a namespace named microservices to group all microservices in the cluster.

   ```bash
   kubectl create namespace microservices
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/12%20creatng%20microservices%20namespace.png" width=500 />
   
2. Create the deployment and service YAML file for each microservice.
3. Apply the YAML file in the microservice namespace.

   ```bash
   kubectl apply -f config.yaml -n microservices
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/13%20apply%20the%20config%20file%20with%20deployent%20and%20services%20in%20the%20namespace.png" width=500 />
4. Verify that all pods are running.

   ```bash
   kubectl get pod -n microservices
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/14%20pods%20running%20in%20the%20microservice%20ns.png" width=500/>
   
5. Verify all the services were created.

   ```bash
   kubectl get services -n microservices
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/15%20checking%20services.png" width=500 />
   
6. Obtain the external IP of your node to access the boutique.
    
    ```bash
    kubectl get nodes -o wide
    ```
    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/16%20getting%20external%20ip%20address.PNG" width=500 />
    
7. Navigate to DigitalOcean and modify the firewall to allow incoming internet traffic.

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/18%20add%20an%20inbound%20rule%20allowing%20traffic%20from%20internet.png" width=500 />
    
8. Check the public IP address using port 30007
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/17%20online%20boutique%20up.PNG" width=500 />
   

### Apply K8 and Security Best Practices
1. Use a fixed image version to ensure consistency across environments.

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/100%20pinned%20image.png" width=500 />
   
2. Add a livenessProbe to each microservice to monitor container health.
   
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/101%20livenessProbe.png" width=500 />
   
3. Specify the protocol for the livenessProbe. Use gRPC (developed by Google) in this case.
   
4. Specify the port for the livenessProbe.
   
5. Set periodSeconds to specify how often to check container health.
   
6. Add a readinessProbe to each microservice to verify when the container is ready to receive traffic.
    
7. Define the protocol, port, and periodSeconds for the readinessProbe.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/102%20readinessProbe.png" width=500 />
   
8. For Redis, change the probe protocol from gRPC to TCPSocket. Kubelet attempts to open a socket to the container using the application port.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/103%20tcpsocket.png" width=500 />
   
9. For the frontend microservice, change the gRPC probe to httpGet and specify the HTTP path. Kubelet sends an HTTP request to the specified path and port. To check the HTTP endpoint.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/104%20httpget%20bcs%20endpoint%20checking%20the%20http%20endpoint.png" width=500 />
   
10. Define resource requests and limits for each microservice to manage expected and maximum resource usage.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/105%20adding%20expteced%20resources%20needed.png" width=500 />
   
11. Change the frontend service type from NodePort to LoadBalancer. NodePort exposes all worker nodes, while LoadBalancer provides a single entry point from the Cloud Provider. Exposing all worker nodes increases the security risks.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/108%20using%20loadbalancer%20as%20a%20netry%20point%20and%20no%20nodeport.png" width=500 />
   
12. Set the number of replicas for each deployment.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/109%20setting%20replicas%20high%20availability.png" width=500 />
   
13. Use labels consistently to identify and manage deployments.
    
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_10_Kubernetes_Microservices/blob/main/Img/110%20labels.png" width=500 />
   
      
