---
title: "Kubernetes Architecture - A deep dive"
seoTitle: "Kubernetes Architecture Explained"
seoDescription: "Explore Kubernetes architecture, origins, and components to simplify cloud-native development and container orchestration in this guide"
datePublished: Mon Mar 03 2025 17:31:11 GMT+0000 (Coordinated Universal Time)
cuid: cm7tc6nsc000e09l2bjlmbpvw
slug: kubernetes-architecture-a-deep-dive
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1740936386668/2ee47a88-70cc-448a-81b0-d0bd5e08ef96.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1741023003422/0a630938-70d9-46bd-81eb-fc69dbb4dc11.png
tags: kubernetes, devops, beginners, opensource-inactive, cloud-native, kubernetes-architecture

---

Hello everyone,  
Today, we dive into the reasons behind Kubernetes, its history, architecture, and various components. If you are looking to explore cloud-native development, this is the best place to start.  
Deploying applications at scale can be overwhelming. Kubernetes makes it easier — but where to start?  
When I first heard about Kubernetes, it sounded complex and intimidating. But once I got my hands dirty, I realized how powerful it is in simplifying container orchestration.

---

## A Brief about Kubernetes

Before even moving on to the main architecture,let us quickly answer the question-What is Kubernetes?

At its core,Kubernetes is an **opensource project** for **managing multi-containerized applications** with a touch of **“automation”** to it.

Additionaly,its a **CNCF graduated project** which means its backed by a **HUGE community of contributors**,and **supporters** and is **stable** to be used in a **production environment**.

## Why is there a need for Kubernetes?

Before Kubernetes came into the picture, companies faced many challenges in managing applications at scale. Traditionally, they relied on:

* **Physical servers**: Inefficient resource usage.
    
* **Virtual machines (VMs)**: Improved flexibility but still required manual scaling and management.
    
* **Containerization**: Docker popularized lightweight, portable applications, but managing many containers was still hard.
    

Companies needed a way to automate the deployment, scaling, and management of containers and realized Docker was not capable of doing this alone.

---

## Why Docker is not the end solution?

Docker, as we all know, only helps in packaging the code and its dependencies in a container that runs in isolated environments. Containers are ephemeral in nature, which means they have a short life and can die and revive anytime.

* **Single host:** Runs on a single machine.
    
* **No auto-healing:** Containers do not restart automatically if stopped by a user or if they go down for any reason.
    
* **No auto-scaling:** Containers do not automatically increase during high traffic.
    
* **No enterprise-level support:** Docker Swarm offers some support but is platform-oriented and only works well with Docker containers. It does not support Kubernetes custom resource definitions (extensions) that offer many useful features.
    

Let’s start with an **Netflix example** to make things easier for you:

Imagine it's weekend time in New York, and everyone is watching Netflix. On weekdays, the traffic to Netflix is not too much. You need to stream high-quality video content to millions of user requests without crashing systems or servers to provide a great user experience. But how to handle this?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741020803142/38f625ff-9ec1-48a5-8e33-63a78f3ce3f2.png align="center")

* If your application runs on only one (or a few) server, then the server will definitely go down (risk).
    
* Or if you increase the number of servers (EC2, physical servers) to run all the time, even on weekdays when there is no traffic at all, you’re definitely going to lose a lot of costs and inefficient resource usage.
    
* You probably could not predict when the traffic is going to increase or decrease, and you also cannot manually increase the number of servers when traffic is high and vice-versa.— So what to do?
    
* If your server goes down, wouldn’t there be a way to heal the containers or spin up another container automatically?
    

Wouldn't it be great if there were a tool that automatically scales, heals, and manages containers?

And, That’s where Kubernetes comes in. Gotcha?

---

## How and where was Kubernetes born?

<mark>Google</mark> had been managing massive workloads for years using an internal system called <mark>Borg</mark>.  
Borg was used internally at Google to schedule and run workloads efficiently across clusters of machines.  
Learning from Borg’s strengths and limitations, Google developed a more flexible, open-source system now called Kubernetes.

<mark>Kubernetes is often called K8s </mark> (k, 8 replaced for in between 8 letters,s). Cool, right?

In 2014, Google open-sourced Kubernetes and donated it to the <mark>Cloud Native Computing Foundation (CNCF)</mark>, an organization that focuses on building things around Kubernetes.

After its launch, major tech companies (Microsoft, Red Hat, AWS) adopted Kubernetes. It became cloud-agnostic, meaning it could run on any cloud provider or even on-premises. Today, it is the foundation of modern cloud-native computing and powers applications at scale.

---

## Features:

Kubernetes is a <mark>container orchestration</mark> platform (simple, minimalistic). It is built on a master-worker node architecture. It is actually a <mark>cluster</mark> under the hood, which means it contains a group of nodes.

* **Orchestration tool**: Helps in deploying & managing containers dynamically.
    
* **Deployment**: Automates deployment.
    
* **Zero-downtime updates**: Even if new updates come in, they do not disturb the running applications.
    
* **Auto-scaling and auto-healing**.
    
* **Fault tolerance and load balancing**.
    

Applications that meet the above requirements are called <mark>cloud-native applications</mark> (that run on K8s).

---

## Architecture:

A Kubernetes cluster consists of a <mark>control plane</mark> (master node) plus a set of worker machines, called <mark>nodes</mark>, that run containerized applications. Every cluster needs at least one worker node in order to run Pods (more on that later).

In production environments, the control plane usually runs across multiple computers, and a cluster usually runs multiple nodes, providing fault tolerance and high availability.

![The control plane (kube-apiserver, etcd, kube-controller-manager, kube-scheduler) and several nodes. Each node is running a kubelet and kube-proxy.](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg align="left")

We are about to dive into an overview of each component in the Kubernetes architecture and discover what each one does. Are you ready? Roll up your sleeves, and let's get started! This is going to be exciting!

---

### Kubernetes API

K8s is powered by an incredible <mark>REST </mark> (Representational State Transfer) API! The API server is a key component. Every move you make in K8s, whether it's creating pods or keeping an eye on services, is an API interaction. It's the heart and soul of the platform, offering a seamless interface for managing and engaging with Kubernetes resources. The K8s API is enormous, with hundreds of endpoints and concepts to explore. It's way more than just a collection of HTTP endpoints!

The API server is a crucial part of the K8s control plane that reveals the K8s API, acting as the control plane's frontend. The main implementation of the Kubernetes API server is kube-apiserver.

---

### etcd

It is the powerhouse for <mark>storing all cluster data</mark>! If your cluster ever goes down, don't worry—every bit of data is safely stored and backed up in the etcd folder, ensuring there's absolutely no data loss!

The keyword here is **"**`key-value store`**"** which means that the data is stored in the form of **key-value pairs** rather than the traditional way of using tables.

---

### Kubelet

Think of it as the <mark>ultimate guardian </mark> or supervisor for containers on a worker node! Kubelet makes sure the containers inside the pod are running just as they should. It eagerly communicates with the control plane to get instructions (like "Run this pod here"). Kubelet keeps a close eye on the pod’s health and springs into action to restart it if anything goes wrong. Plus, it seamlessly interacts with container runtimes like Docker, containerd, or runc. How amazing is that?

**Restaurant example**:  
Imagine K8s as a restaurant and each table is a working node. Kubelet is a waiter who takes orders from the manager (API server) and ensures food (containers) is served correctly.  
If a dish (Pod) is missing, the waiter make sure it’s prepared again.

---

### Kube-proxy

Think of kube-proxy as the ultimate <mark>traffic controller </mark> inside the K8s cluster! It expertly manages networking within the cluster and ensures requests zoom to the right pods, even if they switch to another node. It brilliantly handles load balancing between multiple pods. Using iptables and IPVS (those awesome Linux networking tools), it crafts routing rules like a pro!

**Hotel example**:  
Imagine K8s as a hotel, and each guest room is a pod. The front desk (kube-proxy) routes call correctly to the right room (Pod). If a guest (Pod) moves to another room (another node), the front desk redirects the call to the new room.

---

### Kube-scheduler

Kube-Scheduler is like a <mark>matchmaker</mark> for your pods, finding them the perfect worker node to run on. It figures out where each pod should go in the cluster by checking out the available nodes, their resources like CPU and memory, and any other requirements. It makes sure everything is spread out nicely across the cluster.

### Kube-controller

The controller manager is like the cluster's babysitter, always keeping an eye on things to make sure <mark>everything's running smoothly.</mark> It handles a bunch of controllers that take care of different parts of the cluster. If something goes off track, it jumps in to fix it, like restarting failed pods or auto-scaling.

* **NodeController**
    
* **JobController**
    
* **ServiceAccount controller**
    

### Cloud Controller Manager

The cloud controller manager (CCM) is a cool part of Kubernetes that lets it play nice with different cloud providers like AWS, Google Cloud, and Azure. It's like a bridge between K8s and the cloud, helping to manage stuff like load balancers, storage, and networking. It makes sure Kubernetes knows how to <mark>deal with cloud infrastructure</mark> the right way.

---

### Container vs. Pod

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741012607268/eb41134b-58f8-41e2-9d1d-9cb8b0addac4.png align="center")

---

* **Container**: You create it by <mark>running commands</mark> imperatively.
    
* **Pod**: Instead of writing commands, you declare it in a <mark>YAML </mark> (YAML Ain’t Markup Language) in a configuration file.
    
* **ReplicaSet**: A ReplicaSet ensures that a specified number of **<mark>identical pods</mark>** are always running in your Kubernetes cluster. If a pod crashes or is deleted, the ReplicaSet automatically <mark>creates a new one</mark> to maintain the desired count.
    
* **Deployment**: A <mark>Deployment </mark> is a higher-level abstraction that manages ReplicaSets and <mark>handles rolling updates, rollbacks, and scaling</mark> in a controlled way. When you update your application, the Deployment **<mark>creates a new ReplicaSet</mark>**, gradually shifts traffic to the new pods, and removes the old ones without downtime.
    

---

Some amazing real-life examples with the restaurant example!

| **Component** | **Description** |
| --- | --- |
| **Pod** | The smallest deployable unit in Kubernetes, like a single café where a few chefs (containers) work together, sharing resources to serve meals. |
| **ReplicaSet** | Acts as a franchise manager, ensuring a specific number of cafés (Pods) are always open. If one closes, another opens to maintain service. |
| **Deployment** | Functions as the city planner, managing when new cafés should open or existing ones need updates, ensuring smooth transitions without disruptions. |

Here's an exciting YAML file example to set up an nginx pod:

---

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      ports:
        - containerPort: 80
```

### **Conclusion**

Kubernetes might seem complex at first, but once you break it down, it’s like having an **automation superpower** for managing containers at scale. It takes care of **scaling, self-healing, load balancing, and deployments**, so you don’t have to manually manage everything.

From its roots in Google’s **Borg** to becoming the backbone of modern **cloud-native applications**, Kubernetes has revolutionized how applications run efficiently across **on-premises, cloud, and hybrid environments**.

If you’re just starting out, don’t worry if it feels overwhelming—**everyone starts somewhere!** The key is to **experiment, break things, and learn from them**. Before you know it, deploying applications with Kubernetes will feel natural!

Thank you for reading! I hope you enjoyed learning about Kubernetes!

💡 **Let’s connect!** Feel free to reach out:  
[**LinkedIn**](https://www.linkedin.com/in/devisri-s-0987b6256/)  
[**GitHub**](https://github.com/Devisrisamidurai)