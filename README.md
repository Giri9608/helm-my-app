AWS RDS Scanner Helm Chart
A Helm chart for deploying the AWS RDS Scanner container on Minikube with manual execution.

Prerequisites

Helm 3.x
Minikube
Kubernetes cluster (Minikube)
Docker image: giri8608/rds-scanner (available on Docker Hub)

Installation

Start Minikube:
minikube start --driver=docker


Clone the Repository:
git clone https://github.com/Giri9608/helm-my-app.git
cd helm-my-app


Load the Docker Image into Minikube:
minikube image load giri8608/rds-scanner:latest


Install the Helm Chart:
helm install rds-scanner-release .



Testing

Verify the Pod:
kubectl get pods

Look for a pod named rds-scanner-release-<hash> with status Running.

Access the Pod for Manual Execution:
kubectl exec -it rds-scanner-release-<hash> -- /bin/sh


Run the RDS Scanner:Inside the pod, execute the rds_scanner.py script with AWS credentials:
export AWS_ACCESS_KEY_ID=<your-access-key>
export AWS_SECRET_ACCESS_KEY=<your-secret-key>
export AWS_DEFAULT_REGION=ap-south-1
python /app/rds_scanner.py --region ap-south-1

Replace <your-access-key> and <your-secret-key> with your AWS credentials.


Values



Key
Description
Default



image.repository
Container image repository
giri8608/rds-scanner


image.tag
Container image tag
latest


image.pullPolicy
Image pull policy
IfNotPresent


replicaCount
Number of replicas
1


service.type
Service type
ClusterIP


service.port
Service port
80


Notes

The pod runs sleep infinity to allow manual execution. Use kubectl exec to interact with the container.
The service is included but not required for manual execution, as rds_scanner.py is a CLI tool.

