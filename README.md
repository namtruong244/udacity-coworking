## Project Overview: Coworking Space Service

The Coworking Space Service is a set of APIs that enables users to request one-time tokens and administrators to authorize access to a coworking space. This service follows a microservice pattern and the APIs are split into distinct services that can be deployed and managed independently of one another. For this project, you are a DevOps engineer who will be collaborating with a team that is building an API for business analysts. The API provides business analysts with basic analytics data on user activity in the coworking space service. The application they provide you functions as expected, and you will help build a pipeline to deploy it to Kubernetes. You'll submit artefacts from the build and deployment of this service.

## Step 1: Set Up a Postgres Database
Pre-requisites:
- Have Kubernetes cluster ready.
- Have `kubectl` installed and configured to interact with your cluster.

Instructions:
1. Apply YAML configurations
    ```bash
    kubectl apply -f pvc.yaml
    kubectl apply -f pv.yaml
    kubectl apply -f postgresql-deployment.yaml
    ```
2. Connecting via Port Forwarding:
   ```bash
   kubectl apply -f postgresql-service.yaml
   ```
3. Set up port-forwarding to `postgresql-service`:
   ```bash
   kubectl port-forward service/postgresql-service 5433:5432 &
   ```
4. Checking the tables:
    ```bash
    PGPASSWORD="$DB_PASSWORD" psql --host 127.0.0.1 -U root -d mydatabase -p 5433
    ```

## Create a Dockerfile for the Python Application
Dockerfile
[Dockerfile](./analytics/Dockerfile)

## Write a Build Pipeline with AWS CodeBuild
buildspec File
[buildspec](./buildspec.yml)

BuildCode history
![BuildCode history](Project%20Screenshots/CodeBuild.png)

## Push a Docker image into AWS ECR
Elastic Container Registry history
![Elastic Container Registry history](Project%20Screenshots/ElasticContainerRegistry.png)

## Create Kubernetes Service and Deployment
1. List Services
   ```bash
   kubectl get svc
   kubectl describe svc
   ```
   List Services
   ![List Services](Project%20Screenshots/ListServices.png)
   List Describe Services Kubernetes
   ![List Describe Services Kubernetes](Project%20Screenshots/DescribeSvcKubernetes.png)
   List Describe Services Postgres DB
   ![List Describe Services Postgres DB](Project%20Screenshots/DescribeSvcPostgresqlService.png)
   List Describe Services Coworking API
   ![List Describe Services Project3 API](Project%20Screenshots/DescribeSvcCoworking.png)

3. List Pods
   ```bash
   kubectl get pods
   kubectl describe pods
   ```
   List Pods
   ![List Pods](Project%20Screenshots/ListPods.png)
   List Describe Pods DB
   ![List Describe Pods DB](Project%20Screenshots/DescribePodsPostgresql.png)
   List Describe Pods API
   ![List Describe Pods API](Project%20screenshots/DescribePodsCoworking.png)
   
4. List Deployments
   ```bash
   kubectl get deployments
   kubectl describe deployment project3-api
   ```
   List Deployments
   ![List Deployments](Project%20Screenshots/ListDeployments.png)
   List Describe DB
   ![List Describe Deployments](Project%20Screenshots/DescribeDeploymentsPostgresql.png)
   List Describe API
   ![List Describe Deployments](Project%20Screenshots/DescribeDeploymentsCoworking.png)

## AWS CloudWatch for Logs
   
   CloudWatch Cluster Logs
   ![CloudWatch Cluster Logs](Project%20Screenshots/CloudWatch-ClusterLogs.png)
   CloudWatch Logs
   ![CloudWatch Logs](Project%20Screenshots/CloudWatch-Logs.png)
