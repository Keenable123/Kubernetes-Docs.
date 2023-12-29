# Table of content

[Introduction](#Introduction)

[What does Kubernetes store in etcd?](#What-does-Kubernetes-store-in-etcd)


[Where is the etcd data stored?](#Where-is-the-etcd-data-stored)

[What is etcd full form?](#What-is-etcd-full-form)

[Can I use etcd as a database?](#Can-I-use-etcd-as-a-database)

[Set-up of Kubernetes](#Set-up-of-Kubernetes)







## Introduction
* Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform designed to automate the deployment, scaling, and management of containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

#### Here's a brief introduction to Kubernetes:

###### Containerization: 
Kubernetes is closely associated with containerization technologies like Docker. Containers are lightweight, isolated environments that package an application and its dependencies, making it easy to move and run applications consistently across different environments.

##### Orchestration:
 Kubernetes provides a powerful way to orchestrate containers. It allows you to define how your applications should run, how they should scale, and how they should self-heal in the event of failures.

##### Cluster Management: 

Kubernetes manages a cluster of machines, typically called nodes, that can be physical or virtual. These nodes are grouped into a cluster, and Kubernetes orchestrates containers on these nodes. The nodes can be distributed across various cloud providers, on-premises data centres, or even developer laptops.

##### Desired State:
 Kubernetes operates on the principle of declaring the desired state of your application. You describe how your application should look, and Kubernetes makes it happen. This approach is known as Infrastructure as Code (IaC).

##### Self-Healing: 
Kubernetes constantly monitors the state of your applications and automatically replaces or reschedules containers that have failed. It ensures that your applications remain available and resilient.

##### Scaling:
 You can easily scale your application up or down based on resource demand. Kubernetes can handle horizontal scaling by adding or removing instances of your containers.

##### Rolling Updates: 
Kubernetes supports rolling updates, which allow you to update your application with minimal downtime. New versions of your containers can be gradually rolled out while the old versions are replaced.

##### Service Discovery and Load Balancing: 
Kubernetes provides built-in service discovery and load balancing for your containers, making it easy to expose services to the outside world or route traffic internally.

##### Configuration Management: 
You can manage configuration data separately from the application code, and Kubernetes makes it easy to inject configurations into your containers.

##### Extensibility: 
Kubernetes is highly extensible and has a rich ecosystem of extensions and add-ons for various use cases.

Kubernetes has become the de facto standard for container orchestration in the cloud-native ecosystem. It simplifies the deployment and management of containerized applications, making it easier to build and run scalable, reliable, and resilient services. It's a complex system with a steep learning curve, but it offers significant benefits for organisations looking to adopt container-based infrastructure and microservices architecture.

## What does Kubernetes store in etcd
Kubernetes uses etcd as its distributed key-value store to maintain the state of the entire cluster. Etcd is a consistent and highly available distributed database that stores configuration data, metadata, and other critical information about the cluster. Here are some of the key things that Kubernetes stores in etcd:

##### Cluster Configuration: 
Information about the Kubernetes cluster's configuration, including the API server's configuration, cluster-level security settings, and other cluster-wide settings.

##### Node Information:
 Details about each node (or worker) in the cluster, such as its name, address, and available resources. This information is crucial for scheduling and orchestrating workloads on the nodes.

##### Pod and Container Information: 
etcd stores metadata about pods and containers, such as their names, labels, and status. This information is used for tracking the state of workloads running in the cluster.

##### Service Information: 
Data related to Kubernetes services, including service definitions, endpoints, and service account tokens.

##### Replication Controller and Deployment Data: 
Information about replication controllers and deployments, including desired replica counts, scaling information, and rollout strategies.

##### Namespace Data: 
Details about namespaces, which provide a way to logically group and isolate resources within the cluster. This includes namespace names and associated metadata.

##### Persistent Volume Claims and Storage Classes: 
Information about storage resources, such as persistent volume claims and storage classes, which are used to provision and manage storage for applications.

##### Secrets and ConfigMaps:
 Secure information like secrets and configuration data stored in ConfigMaps. This data can be mounted into pods as files or environment variables.

##### Resource Quotas and Limit Ranges: 
Definitions of resource quotas and limit ranges, which enforce resource constraints and limits for namespaces and pods.

 ## Where is the etcd data stored?

etcd is a distributed key-value store that is often used as a reliable data store for coordinating distributed systems and managing configuration data in environments like Kubernetes. Etcd stores its data on the file system of the machines where etcd is running.

The default data directory for etcd is typically /var/lib/etcd on Linux systems. However, you can configure the data directory when you start the etcd server by using the --data-dir command-line option. For example:

##### bash
etcd --data-dir=/path/to/custom/data/directory

The data directory contains all the data managed by etcd, including key-value pairs and other metadata required for its operation. It's important to ensure that this data directory is backed up regularly and that you have a plan for data recovery in case of failures, as data stored in etcd is critical for the proper functioning of the systems that rely on it.

Keep in mind that etcd is often deployed in a distributed fashion across multiple machines to ensure high availability and fault tolerance. Each etcd instance on different machines stores its own copy of the data, and they communicate with each other to maintain consistency across the cluster.





##  What is etcd full form?

The term "etcd" is not an acronym; it is just a short, simple name for the distributed key-value store system. It is not derived from a specific set of words or phrases. The name "etcd" is often pronounced as "et-cee-dee," and it was chosen for its simplicity and ease of use. Etcd is a popular component in the cloud-native ecosystem, often used for service discovery, configuration management, and coordination of distributed systems.


## Can I use etcd as a database?

Etcd is primarily designed as a distributed key-value store for configuration management, service discovery, and coordination of distributed systems. While it can be used to store data in a key-value format, it may not be the best choice for all database use cases.

Here are some considerations when thinking about using etcd as a database:

##### Data Model:
 Etcd is not a traditional relational or document database, and it lacks the complex querying and indexing capabilities found in dedicated databases. It's best suited for storing small amounts of metadata and configuration data.

##### Consistency:
 Etcd provides strong consistency guarantees, which can make it suitable for certain use cases that require strong consistency. However, this might come at a performance cost compared to databases optimised for specific workloads.

##### Data Volume: 
Etcd is designed to manage relatively small amounts of data. If your application requires a database for large-scale data storage, you should consider other database systems designed for that purpose.

##### Querying: 
Etcd's querying capabilities are limited. It primarily supports simple key-based reads and writes. If your application needs complex querying, aggregation, or analytics, dedicated databases like MySQL, PostgreSQL, or NoSQL databases might be more appropriate.

##### Transactions: 
While etcd supports transactions for atomic operations on multiple keys, it may not provide the same level of transactional support as traditional databases.

##### Performance: 
The performance characteristics of etcd might not be optimal for all database workloads. It is optimized for distributed coordination and high availability, which may lead to trade-offs in terms of raw data storage and retrieval speed.

In summary, etcd is not a replacement for traditional databases in most cases. It's a specialized tool designed for specific use cases related to distributed systems and configuration management. If you need a general-purpose database for data storage and retrieval, it's usually better to consider other database solutions that are more tailored to your specific requirements.











## Set-up of Kubernetes
Before installing minikube you have to install docker and curl command.
```
sudo apt-get update
sudo apt-get upgrade -y
```

```
Output

Hit:1 http://security.ubuntu.com/ubuntu jammy-security InRelease
Hit:2 http://in.archive.ubuntu.com/ubuntu jammy InRelease
Hit:3 http://in.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:4 http://in.archive.ubuntu.com/ubuntu jammy-backports InRelease
Reading package lists... Done
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  gjs libgjs0g python3-update-manager ubuntu-advantage-tools update-manager
  update-manager-core
0 upgraded, 0 newly installed, 0 to remove and 6 not upgraded.
```


## Then we have to install docker so follow the below link for installation of docker(We can also install hyper,podman,virtual box VM fusion but I have used docker)
## https://docs.docker.com/engine/install/ubuntu/

```
sudo apt install curl
```
```
Output

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
curl is already the newest version (7.81.0-1ubuntu1.15).
0 upgraded, 0 newly installed, 0 to remove and 6 not upgraded.
```
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

```
output
  
  % Total	% Received % Xferd  Average Speed   Time	Time 	Time  Current
                             	Dload  Upload   Total   Spent	Left  Speed
100 89.3M  100 89.3M	0 	0  2108k  	0  0:00:43  0:00:43 --:--:-- 2438k
```
```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
```
Output

  % Total	% Received % Xferd  Average Speed   Time	Time 	Time  Current
                             	Dload  Upload   Total   Spent	Left  Speed
100 89.3M  100 89.3M	0 	0  1918k  	0  0:00:47  ```
0:00:47 --:--:-- 1961k

```
```
sudo install minikube-linux-amd64 /usr/local/bin/minikube


```




```
minikube start
``` 
```
output

 😄  minikube v1.32.0 on Ubuntu 22.04 (kvm/amd64)
✨  Using the docker driver based on existing profile
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
🏃  Updating the running docker "minikube" container ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
🔎  Verifying Kubernetes components...
	▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
``````


```
 minikube status
```
``````
output

minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
