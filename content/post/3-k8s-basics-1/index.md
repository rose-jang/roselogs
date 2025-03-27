---
title: Kubernetes Basics
date: 2025-03-27
draft: false
image: k8s-banner.png
tags:
  - Kubernetes
  - Containerization
  - Virtualization
categories: 
  - Containerization
---


# What is Kubernetes?

**Kubernetes** is an open-source platform designed to manage containerized applications at scale. It automates the deployment, scaling, and management of application containers across clusters of machines.

Kubernetes is capable of running thousands of replicas of an application simultaneously, ensuring high availability and reliability. Each replica (an instance of an application) can be accompanied by additional containers, such as **sidecars**, which serve as "managers" performing essential tasks such as logging, proxying, or monitoring.

A key concept in Kubernetes is the shared lifecycle of containers within a pod, ensuring that all components of the application work together seamlessly. This design simplifies the deployment and management of applications, especially in large-scale environments where consistency and reliability are paramount.

---

## Fundamental Components

### Containers
*Packaging all dependencies, code, and runtime of exact versions*
- Containers ensures smooth operation across both development and production environments.
- Since modern applications require frequent updates and changes, containers make it easier for developers to implement and distribute updates without disrupting services.
- **Dev teams** can efficiently share and update applications, while **Ops teams** can maintain scalable and reliable deployments.

### Pod
*The smallest deployable unit in Kubernetes*
- A pod encapsulates one or more tightly coupled containers.
- Typically a pot hosts a single main application container, but it can include additional containers (sidecars) that assist the main application.
- Containers in a same pod share:
	- Storage volumes
	- Lifecycle management
		-  All containers in a pod start/stop/restart altogether, ensuring they function as a cohesive unit.
	- Network resources (same IP address / port space)
		- They communicate internally via localhost hostname with their designated ports.

### ReplicaSet
*Ensures desired pod availability and redundancy*
- A ReplicaSet is responsible for maintaining a stable set of identical pods, using a template.
- Maintains the desired number of pods running at all time, automatically replacing failed pods.
- **Purpose**: High Availability, redundancy, and scalability.

### Deployment
*Manages ReplicaSets and facilitates rolling updates*
- Deployment is a higher-level abstraction that manages ReplicaSets
- Helps automate the scaling and rollout process while minimizing manual intervention.

### Services
*Configuration for network and load balancing*
- Kubernetes pods are ephemeral, they can be created / destroyed dynamically. This means their IP addresses are not assigned statically. Services provide a stable endpoint to resolve this issue for accessing pods.

**Types of Services:**
1. Cluster IP (default type)
	- Exposes the service internally within the cluster.
	- Allows communication between pods in the same cluster.
	- Assigns an internal IP address and DNS name, unreachable from the external.
	- Service detects the correct pod based on the given **selector name**
		Service: `spec.selector.app` = Pod: `metadata.labels.app`
2. NodePort
	- Exposes the service on a static port on each node's IP.
	- Enabling the service accessible from outside the cluster using <NodeIP>:<NodePort>.
3. LoadBalancer
	- Exposes the service externally via a cloud-based load balancer.
	- Suitable for production environments requiring public access and traffic distribution.


### Summary
This post covered Kubernetes' core building units: Containers, Pods, ReplicaSets, Deployments, and Services. These components work together to provide a scalable, resilient system for managing containerized applications.