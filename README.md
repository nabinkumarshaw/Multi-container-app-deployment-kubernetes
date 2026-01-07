# Multi-Container App Deployment using Kubernetes

## 1)Deployed a Node.js frontend and database backend in separate Kubernetes pods using Docker images.

## 2)Configured Deployment, Service, and ConfigMap YAML manifests for load balancing, scalability, and 24/7 availability.

##  3)Implemented Kubernetes features like rollouts and rollbacks for zero-downtime updates.

## 4)Deployed locally with Minikube using kubectl.




Multi-Container App deployment  on Kubernetes

1. Project Overview

"This project demonstrates how to deploy a Node.js application connected to a MongoDB database using Kubernetes. It is a multi-container setup where both containers—one for the Node.js app and one for MongoDB—are deployed within the same Pod, and are exposed using a Kubernetes Service."

2. Tech Stack
Backend: Node.js

Database: MongoDB

Containerization: Docker

Orchestration: Kubernetes (YAML manifests)

Deployment Method: Multi-container Pod (sidecar pattern)

Cloud Readiness: Configured for LoadBalancer service



3. Architecture
One Pod contains two containers:

Node.js app container (image: philippaul/node-mongo-db:02)

MongoDB container (mongo:latest)

Replicated across 3 pods for high availability.

Kubernetes Service of type LoadBalancer to expose the application on port 8000, routing traffic to port 3000 inside the containers.


4. Key Components
✅ deployment_same.yml
Defines a deployment named deployment-nodedb-app

Contains:

3 replicas

Two containers in one Pod: Node.js and MongoDB

Container images:

philippaul/node-mongo-db:02 (Node.js app)

mongo:latest (MongoDB)

✅ service_same.yml
Defines a Kubernetes Service named service-nodedb-app

Type: LoadBalancer

Forwards external traffic from port 8000 to internal port 3000

Uses label selector app: deployment-nodedb-app to target the right Pods



5. How It Works
Kubernetes spins up 3 identical Pods (replicas), each containing:

The Node.js application

A MongoDB database instance

Each Pod runs independently but has both containers communicating via localhost inside the Pod.

The Kubernetes Service listens on port 8000 and forwards requests to the Node.js app on port 3000.

External users can access the app via the public IP assigned by the LoadBalancer.


6. Challenges Faced
Challenge	Solution
Communication between app and DB Solved by placing both in the same Pod to share localhost
Exposing app externally	Used LoadBalancer service in Kubernetes
Ensuring high availability	Set replica count to 3 for failover and scaling


 7. Real-World Use Case
"This kind of multi-container pattern is useful in real-world microservices where tightly coupled services (like app + DB or app + sidecar) need to be deployed together. It's also an efficient way to prototype or demo a full-stack service locally or in the cloud."


 8. Possible Improvements
Use Persistent Volumes for MongoDB data

Move MongoDB to a separate Pod for better scalability

Add readiness/liveness probes for container health checks

Implement CI/CD with tools like Jenkins or GitHub Actions



 Sample Explanation in Interview
 
"I built a Kubernetes-based multi-container app where a Node.js backend and MongoDB database run inside the same Pod. I used a Kubernetes Deployment to manage replicas and a LoadBalancer Service to expose the application. One key challenge was ensuring communication between the app and database, which I resolved by running them as containers in the same Pod so they can use localhost. I chose this pattern to simulate a real-world scenario where services are closely linked. In the future, I plan to decouple the DB and use Persistent Volumes for data persistence."
