# VUR Application Kubernetes Deployment

This repository contains the necessary Kubernetes manifests to deploy the VUR application on a k3s cluster. Below is a comprehensive guide to the cluster configuration, components, persistent volume claims, and database initialization.

## Cluster Overview

The VUR application is deployed on a lightweight k3s Kubernetes cluster optimized for edge, IoT, and CI/CD environments. The cluster consists of several nodes, each serving a specific role in the operation and management of the Kubernetes resources.

### Nodes in the Cluster

- **Master Node**: Hosts the Kubernetes control plane services, managing the cluster's state and configuration.
- **Worker Nodes**: Responsible for running the application workloads and other services as scheduled by the master node.

### Cluster Components

- **Pods**:
  - `vur-app`: The main backend service for the VUR application.
  - `vur-vue`: Frontend service that serves the VUR web interface.
  - `mysql-pod`: Database service running MySQL, used for storing encrypted texts.

- **Services**:
  - `vur-app-service`: Exposes the `vur-app` pod to be accessed on a specific node port.
  - `vur-vue-service`: Exposes the `vur-vue` pod for frontend access.
  - `mysql-service`: Internal cluster service that allows other services to communicate with the MySQL database.

### Persistent Volume Claims (PVCs)

- `mysql-pvc`: A persistent volume claim used by the MySQL database to ensure data persists across pod restarts and deployments.

### Database Initialization

The MySQL database is initialized with a single table `texts`, which is used to store encrypted text entries. This is accomplished through an init script mounted into the MySQL pod at startup.

## Demo

A live demo of the VUR application can be accessed at [http://49.13.50.133:30001/](http://49.13.50.133:30001/).

## Quickstart

To deploy the VUR application on your own k3s cluster, follow these steps:

1. Clone this repository to your local machine or directly on your Kubernetes master node.
2. Apply the manifests in the following order:
   ```shell
   kubectl apply -f mysql-pvc.yaml
   kubectl apply -f vur-mysql-pod.yaml
   kubectl apply -f vur-mysql-service.yaml
   kubectl apply -f vur-app.yaml
   kubectl apply -f vur-app-service.yaml
   kubectl apply -f vur-vue.yaml
   kubectl apply -f vur-vue-service.yaml


## Additional Information
This deployment is an example of a cloud-native application leveraging Kubernetes for orchestration. It demonstrates my ability to design and implement a full-stack application deployment on a modern container platform.