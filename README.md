# Kubernetes Project: n8n + PostgreSQL + Ingress

This project deploys a full workflow automation stack on Kubernetes including:

- n8n (workflow automation platform)
- PostgreSQL (stateful database)
- ConfigMap (non-sensitive configuration)
- Secret (sensitive credentials)
- Ingress (external access)

---

## Architecture Overview

The system consists of:

- A **StatefulSet** for PostgreSQL with persistent storage
- A **Deployment** for n8n
- A **ConfigMap** for database configuration
- A **Secret** for database credentials
- A **Service** for internal communication
- An **Ingress** for external access

---

## Project Structure


configmap.yaml
ingress.yaml
n8n_deployment.yaml
n8n_secret.yaml
postgres_deployment.yaml
README.md


---

## Prerequisites

- Kubernetes cluster (Minikube, Kind, or Cloud cluster)
- kubectl configured
- Ingress controller installed (e.g., NGINX Ingress)

---

## Deployment Order

Apply resources in the following order:

```bash
kubectl apply -f n8n_secret.yaml
kubectl apply -f configmap.yaml
kubectl apply -f postgres_deployment.yaml
kubectl apply -f n8n_deployment.yaml
kubectl apply -f ingress.yaml
Accessing n8n

If using Ingress:

Configure your domain in ingress.yaml

Add it to your /etc/hosts if testing locally

Example:

http://n8n.local

If using NodePort:

http://<node-ip>:30000
Database Configuration

n8n connects to PostgreSQL using environment variables:

DB_TYPE=postgresdb

DB_POSTGRESDB_HOST=postgres-service

DB_POSTGRESDB_DATABASE=n8n

DB_POSTGRESDB_USER (from Secret)

DB_POSTGRESDB_PASSWORD (from Secret)

Persistent Storage

PostgreSQL uses a StatefulSet with:

PersistentVolumeClaim

volumeClaimTemplates

This ensures data is not lost when pods restart.

n8n also uses persistent storage for workflows.

Security

Sensitive data is stored in Kubernetes Secrets:

Database username

Database password

Non-sensitive configuration is stored in ConfigMaps.

Scaling

You can scale n8n using:

kubectl scale deployment n8nio-deployment --replicas=2
Useful Commands

Check pods:

kubectl get pods

Check services:

kubectl get svc

Check ingress:

kubectl get ingress

View logs:

kubectl logs <pod-name>
Notes

Ensure storageClass exists in your cluster.

Ensure Ingress controller is installed.

Adjust hostnames in ingress.yaml as needed.

Author

Kubernetes Project Lab


---

If you want, I can also:

- 🔥 Make it more professional (with diagrams section)
- 📦 Add troubleshooting section
- 🚀 Add CI/CD section
- 🏗 Turn it into a portfolio-grade README
- 📊 Add architecture diagram (I can generate one)

Tell me the level you want 😄
full md file no bs
# n8n + PostgreSQL Kubernetes Project

This project deploys a full workflow automation stack on Kubernetes including:

- n8n (workflow automation application)
- PostgreSQL (stateful database)
- ConfigMap (configuration data)
- Secret (sensitive credentials)
- StatefulSet (database workload)
- Deployment (application workload)
- Service (internal networking)
- Ingress (external access)

---

## Project Structure


configmap.yaml
ingress.yaml
n8n_deployment.yaml
n8n_secret.yaml
postgres_deployment.yaml
README.md


---

## Architecture

- PostgreSQL runs as a StatefulSet with persistent storage.
- n8n runs as a Deployment.
- n8n connects to PostgreSQL using environment variables.
- Secrets are used for database credentials.
- ConfigMap is used for non-sensitive configuration.
- Ingress is used to expose n8n externally.

---

## Requirements

- Kubernetes cluster (Minikube, Kind, or cloud)
- kubectl configured
- Ingress controller installed (e.g., NGINX)
- StorageClass available in the cluster

---

## Deployment Order

Apply resources in this order:

```bash
kubectl apply -f n8n_secret.yaml
kubectl apply -f configmap.yaml
kubectl apply -f postgres_deployment.yaml
kubectl apply -f n8n_deployment.yaml
kubectl apply -f ingress.yaml
Verify Deployment

Check pods:

kubectl get pods

Check services:

kubectl get svc

Check ingress:

kubectl get ingress
Accessing n8n
If Using Ingress

Configure the host in ingress.yaml.

For local testing, add the host to /etc/hosts.

Example:

http://n8n.local
If Using NodePort

Access using:

http://<node-ip>:30000
Database Configuration

n8n connects to PostgreSQL using these environment variables:

DB_TYPE=postgresdb

DB_POSTGRESDB_HOST=postgres-service

DB_POSTGRESDB_PORT=5432

DB_POSTGRESDB_DATABASE=n8n

DB_POSTGRESDB_USER (from Secret)

DB_POSTGRESDB_PASSWORD (from Secret)

Persistent Storage

PostgreSQL uses:

StatefulSet

volumeClaimTemplates

PersistentVolumeClaim

This ensures data persistence across pod restarts.

n8n also uses persistent storage for workflow data.

Secrets

Sensitive values stored in Kubernetes Secret:

Database username

Database password

Scaling

Scale n8n:

kubectl scale deployment n8nio-deployment --replicas=2
Logs

View n8n logs:

kubectl logs <n8n-pod-name>

View PostgreSQL logs:

kubectl logs <postgres-pod-name>
Cleanup

Remove all resources:

kubectl delete -f .
Notes

Ensure storageClassName exists in your cluster.

Ensure Ingress controller is installed before using ingress.

Verify all ConfigMap keys match exactly in case and spelling.

Ensure service names match between StatefulSet and configuration.

Purpose of This Project

This project demonstrates:

Kubernetes workloads (Deployment & StatefulSet)

Configuration management (ConfigMap & Secret)

Persistent storage

Internal service networking

External exposure via Ingress

Real-world application deployment patterns