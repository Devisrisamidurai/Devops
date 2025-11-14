---
title: "Getting started with Kubernetes"
datePublished: Fri Nov 14 2025 16:11:41 GMT+0000 (Coordinated Universal Time)
cuid: cmhz22hso000202jv9fkmgjts
slug: getting-started-with-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1762605305250/48de6d15-ddb0-47b7-8a39-e8592fef38d1.jpeg
tags: kubernetes, devops, cloud-native, minikube

---

Hello everyone, hope you’re doing great!  
In this article, we will dive into how to work with Kubernetes from scratch, covering the installation, setting up the base environment, deploying a simple application to K8S, and we’ll get to play around with it for a while with some interesting commands.

If you’re someone new and this is the first time you’re hearing the word “Kubernetes”, then I would strongly recommend giving this blog a read before you dive in here!  
[All about k8s architecture](https://devisri-blogs.hashnode.dev/kubernetes-architecture-a-deep-dive) - where I’ve talked about its history and broken down its architecture and components.

This is going to be a full hands-on (trust me, it’ll be so fun!), so have your laptop ready and let’s goo!

## Prerequisite & Installation

Kubernetes is too **complex and heavy** to have on your system, and so we’ll be choosing a much lighter version out there so that your system won’t crash. Throughout this blog series, we’ll stick to minikube (small K8S) since it’s very easy to get started with. Before installing it, ensure you have the following requirements on your system.

* **2 CPU cores or more**
    
* **2GB of free memory**
    
* **20GB of free disk space**
    
* **Internet connection**
    
* Container managers like **Docker** or Podman for driver managers.
    
    Minikube lets you run a single-node Kubernetes cluster locally. To install it,
    
    1. ### Windows/WSL
        
    
    ```bash
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    ```
    
    2. ### Mac OS
        

```bash
brew install minikube
```

To verify the installation type,

```bash
minikube version
```

If installed, it shows something like the example below in your terminal!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762762882370/10c20105-786d-4c3c-baba-48e5da285975.png align="left")

## Other options

There are so many ways to work with Kubernetes. If you are using it for learning purposes, and if your system does not support the installation, better go for online playgrounds.  
Playgrounds are the best choice that runs on the cloud and lasts about 1 hour, and it’s free. Some of the Playgrounds I’ve used that best suited working with k8s are,

* **Killercoda Kubernetes playground**
    
* **Kodekloud K8s playground(paid)**
    
* **Play with Kubernetes**
    
* **Katacoda (legacy)**  
    All you need to do is just open, type commands as it is and experiment freely.
    

## K8s flavors

K8s has got so many flavors to work with, and one of the other lightweight options is Kind(yeah, need to be kind enough to use it😄!)  
Kind(Kubernetes in Docker) is great if you want lightweight clusters inside Docker.  
To install it, just type:

```plaintext
go install sigs.k8s.io/kind
```

Have Golang preinstalled in your system. And then, to create a K8s cluster, type

```plaintext
kind create cluster --name demo-cluster
```

## Minikube and why?

Kubernetes itself is an opensource project maintained by the CNCF(Cloud Native Computing Foundation), developed by Google. Many organizations build their own distributions(“flavors”) on top of it, all based on the same Kubernetes core, but with extra tools, installers, UIs, or integrations. Think of it, milk is the base for the ice cream, and you can modify it by adding toppings,flavors, and different use cases.

Likewise, companies just modify the base Core K8S according to their taste and use cases. Kubernetes is classified based on these different use cases as below, and how and where, which version of it serves the best.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762833312646/c8d98346-429c-4f01-91a6-745d5d67aec2.png align="center")

But.. wait! You may ask, when there are so many flavors out here, why use minikube? K8s is designed for managing clusters across multiple machines or cloud servers. But when you’re just learning, developing locally, or testing deployments, you don’t need all that complexity, and that’s where it shines(Cuz, obv you’ll work with small projects)! Some specific reasons,

* It's a **single-node cluster** on your laptop.
    
* Provides a fully **functional Kubernetes** environment.
    
* Great for **learning and experimenting**— more than enough to understand how deployments, pods, and services work.
    

## A simple project

Okie, it’s build time!

To work around, I’m gonna build a simple **Golang web server** that simply says **“Hello world!”**👀.Open up the terminal and type,

```plaintext
mkdir K8s-Demo
cd K8s-Demo
code .
```

It opens up your **VS Code** with the setup env. Copy & Paste the code below,

```go
package main
import (
  "fmt"
   "net/http"
)
 func handler(w http.ResponseWriter,r *http.Request){
   fmt.Fprintln(w,"Hello World from Kubernetes!! This is a Go web server running in localhost.")
}
func main(){
    http.HandleFunc("/",handler)
    fmt.Println("Server is running on port 8080...")
    http.ListenAndServe(":9090",nil)
}
```

To run the app, do

```powershell
go mod init
go mod tidy
go run main.go
```

Access the app at http://localhost:9090 and tadaa😄, the app runs smoothly and prints hello world!! nothing fancy here🫠

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762923705078/420b8d6f-6270-4dba-a315-d0d85508e323.png align="center")

Now, containerize the hello-world app by writing a dockerfile.

```dockerfile
FROM golang:1.22 as builder
WORKDIR /app
COPY . .
RUN go mod init hello-k8s && go build -o app .

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/app .
EXPOSE 9090
CMD ["./app"]
```

To build a docker image out of this,

```powershell
docker build -t hello-k8s:latest .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762872338365/87d438da-aa39-484a-b997-c049065c5481.png align="left")

To run Docker instances,

```powershell
docker run -p 9090:9090 hello-k8s:latest
```

This should work fine, and the app can still be accessed via **port 9090**.

**Github Repo** for this project: [https://github.com/Devisrisamidurai/K8s-blog-Demo](https://github.com/Devisrisamidurai/K8s-blog-Demo)

**PS: If you’re new to containerization, then read this blog so that you better understand stuff.  
**[**Docker for absolute beginners**](https://hashnode.com/post/cm81xzs3q000009l4914405yi)

## Write a YAML file and its definition

Here comes the important part, where we will be writing YAML files for deploying on Kubernetes. And again, if you’re new to YAML, then give this blog a read because things get difficult hereafter.

[Introduction To YAML](https://hashnode.com/post/cmbnufk1r000402ibhr6i1vpx)

We know that Kubernetes is essentially a **REST API** under the hood, and every action you take within a Kubernetes cluster, be it the creation of pods or the monitoring the services, boils down to interactions with its API. It’s a way more than just a collection of HTTP endpoints! And there are three ways to interact with the API:  
1\. **via kubectl** - Kubernetes terminal way  
2\. **curl requests**  
3\. **client-go,client-java** library code

Here’s the YAML manifest for Kubernetes deployment. We’ll go through what each line means and how it works. But before that, we should know the difference between what a deployment is, a service vs a replicaset in Kubernetes manifests.

* **Container**: Created by running commands using Docker.
    
* **Pod**: Defined in a YAML file instead of using commands.
    
* **Deployment**: Provides a higher-level abstraction that manages rolling updates, rollbacks, and scaling of pods. It creates a new Replicaset for updates, shifts traffic to new pods, and removes old ones without downtime.
    
* **Replicaset**: Ensures the desired number of pods are running in your cluster by monitoring and replacing any that fail or disappear.
    
* **Service**: Exposes a group of pods to the network, providing stable IP and DNS for communication, even though pods are temporary.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741012607268/eb41134b-58f8-41e2-9d1d-9cb8b0addac4.png?auto=compress,format&format=webp align="center")

```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: hello-k8s
spec: 
  replicas: 2
  selector:
    matchLabels:
      app: hello-k8s
  template:
    metadata:
      labels:
        app: hello-k8s
    spec:
      containers:
        - name: hello-k8s
          image: hello-k8s:latest
          ports:
            - containerPort: 8080
```

Here’s the YAML manifest for creating a service in K8s using NodePort.

```yaml
apiVersion: v1
kind: Service
metadata:
 name: hello-service
spec: 
   type: NodePort
   selector: 
     app: hello-k8s
   ports:
   - port: 8080
     targetPort: 8080
     nodePort: 30008
```

Here’s the complete breakdown of what each line meant in the YAML file we defined above.

| **apiVersion - apps/v1** | Every K8s object(pods, deployments, services) belongs to an API group and version and tells which version of API to use to interpret this file. |
| --- | --- |
| **kind** | This defines what type of K8s object we’re creating whether it’s a pod/service/Configmap/Ingress/deployment |
| **metadata** | Provides info about object with its name, namespace, labels and annotations. |
| **spec(specification)** | This is the heart of your resource,describes the desired state and it constantly compares the current state with its desired state. |
| **replicas** | Here, you’re asking K8s to maintain 2 running pods for this deployment and if one crashes, K8s will spin up new one automatically. |
| **selector** | This defines how the deployment finds which pod it controls. |
| **template** | Blueprint for the pods that the deployment will create, that describes what each pod should look like. |
| **template.spec** | This defines what actually runs inside each pod. |
| **containers** | A pod contain one or more containers. Each item under containers: defines a single container to run. |
| **ports** | List of container ports that the app listens on containerPort - Port inside the Pod’s container. nodePort - Exposed on each cluster node for external access. targetPort - Pod that sends traffic to |

Make sure the project structure is defined as follows,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763054439970/b79151c7-0d19-4a85-b95b-c3530ad52399.png align="center")

Place all your YAML files inside the k8s/manifests folder, that’s the default path that kubectl will look for when undergoing deployment.

## Deploying to K8s

The whole view of Deployment in K8s is as follows:

> ***Minikube (kubectl) reads the YAML file and identifies it as a Deployment(kind: Deployment) and creates a Deployment object named hello-K8s. Spawns 2 pods based on the template. Each pod runs a container from hello-k8s:latest listening on port 9090 and keeps monitoring; if a pod dies, it restarts one to maintain 2 running pods.***

Okie, let’s start deploying to K8s.. Open your **WSL terminal** and **create a user without sudo privileges** because its safer to run the minikube outside root account. To start the cluster, simply type

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763051193877/579f73fc-e19b-4896-9d76-457775d9a4df.png align="center")

As you can see, a cluster with a worker node using the Docker driver as a base, and it’s pulling the image with K8s version v1.31.0 on Docker driver as default of version 27.2. It also adds ingress for networking between the pods, allocating CPU RAM. It runs in the default namespace(let’s see)

**Namespaces**: It’s like a **separate folder that groups related resources**(Pods, Services,etc..) inside a cluster,helps to organize and isolate environments (dev, prod, test) each can have their own namespace.

If you wanna check current status of the minikube cluster, type and you can see a couple of things here👀

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763052425824/a0736cf4-993f-40e2-a7d1-bc2af460bb13.png align="center")

* **Control plane** - the minikube cluster acts as the master node/control plane.
    
* **Host**: The virtual machine or container is up and running.
    
* **kubelet**: Manages the Pod, indicating that this node is active.
    
* **api server**: The kubeapi server core is running.
    
* **Kubeconfig**: Local kubectl is correctly connected to this minikube cluster.
    
* **Kubectl**: Kubectl is a way of interacting with the Kube-server-api through the terminal.
    

Now let’s see if any pod is running in my Cluster,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763053519857/98335b74-47ca-471e-a45d-061069022ca2.png align="center")

Here, an old go-web app is running (312 days back!) with the desired state 1 container always up and running, but now it does not run due to CrashLoopBackOff. Let’s clean up the pod,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763054075540/72d61bf0-df9d-4d05-9d1d-b03878224685.png align="center")

Now it’s deleted, and let’s deploy guyss!

```bash
$ kubectl apply -f k8s/manifests/deployment.yaml
deployment.apps/hello-k8s created
```

Now check if any pod is running👀

```bash
$ kubectl get pods
NAME                          READY   STATUS              RESTARTS   AGE
hello-k8s-74f56ddfc7-xf9mv    0/1    ContainerCreating    0          10s
hello-k8s-74f56ddfc7-nq8hf    0/1    ContainerCreating    0          10s
```

Ohh well, the container is getting ready here, let’s see after some time what happens!

```bash
$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
hello-k8s-74f56ddfc7-lps9m    1/1     Running   0          20s
hello-k8s-74f56ddfc7-nq8hf    1/1     Running   0          20s
```

As you can see now, the container is up and running with the desired state being 2 mentioned in the deployment.yaml file.

To check the deployments in minikube cluster,

```bash
$ kubectl get deployments
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
hello-k8s    2/2     2            2           1m
```

Now let’s deploy the service as well. For that,

```bash
$ kubectl apply -f k8s/manifests/service.yaml
service/hello-service created
```

Let’s see if the service we created is configured correctly

```bash
$ kubectl get svc
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-service    NodePort    10.96.122.167    <none>        8080:30008/TCP   1m
kubernetes       ClusterIP   10.96.0.1        <none>        443/TCP          2d
```

Well, that too works fine! That’s how you deploy in Kubernetes🙌

Congrats, dude🎉!

---

## kubectl - The K8s terminal!

Kubectl (cube control) is the command-line tool that lets you talk to your K8s cluster. It connects to the API server(K8s heart) using your kubeconfig file and lets you

* Check cluster health
    
* Create, view, or delete resources (Pods, deployments, services, etc.)
    
* Deploy YAML manifests
    
* Debug running applications
    
    For example, when you run
    

```powershell
$ kubectl get pods
```

kubectl sends an HTTPS request to the Kubernetes API server, which replies with info about the pods in your cluster. The connection details like cluster endpoint, tokens and context all come from **~/.kube/config**.

## Playing around with commands

Now it’s playtime around Kubernetes. Roll up your sleeves, this is gonna be really fun and exciting😀.

So far, we saw how to get deployments, services separately. Now, we can get altogether with just a single command. As you can see below,

it gives the pods→ services→ deployements→replicaset in the hierarchy.

```bash
$ kubectl get all
NAME                              READY   STATUS    RESTARTS   AGE
pod/hello-k8s-6d8d4f7d9b-4jrzd    1/1     Running   0          20s
pod/hello-k8s-6d8d4f7d9b-bm8qg    1/1     Running   0          20s

NAME                              TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/hello-service             NodePort   10.99.87.220    <none>        8080:30008/TCP   10s
service/kubernetes                ClusterIP  10.96.0.1       <none>        443/TCP          5m

NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-k8s         2/2     2            2           20s

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-k8s-6d8d4f7d9b     2         2         2       20s
```

To get the running nodes in the k8s cluster, do

```bash
$ kubectl get nodes
NAME       STATUS   ROLES           AGE     VERSION
minikube   Ready    control-plane    3m34s   v1.29.0
```

To get the full details of a particular pod or deployment, type the following command. It lists below the name, namespaces and all other details, including the image name and the current status of the pod.

```bash
$ kubectl describe pod hello-k8s-6d8d4f7d9b-4jrzd
Name:         hello-k8s-6d8d4f7d9b-4jrzd
Namespace:    default
Labels:       app=hello-k8s
Containers:
  hello-k8s:
    Image:        hello-k8s:latest
    Port:         8080/TCP
    State:        Running
    Ready:        True
Events:
  Normal  Pulled     Successfully pulled image "hello-k8s:latest"
  Normal  Started    Started container hello-k8s
```

To get inside the cluster like a private network inside a Kubernetes cluster, use SSH (Secure Shell), which helps in letting you inside securely and within a virtual private network(VPN).

```bash
$ minikube ssh
docker@minikube:~$
```

Access the application using the service command,

```bash
$ minikube service hello-service
```

It should print something like this below.

```bash
🎉  Opening service default/hello-service in default browser...
👉  http://127.0.0.1:30008
```

In browser, you can see the output!! taddaaa💃🏻😉

```bash
Hello world from Kubernetes!! This is Go web server running in localhost.
```

Now, let’s stop the minikube cluster and then gracefully delete it

```bash
$ minikube stop
✋  Stopping node "minikube" ...
🛑  1 node stopped.
$ minikube delete
🔥  Deleting "minikube" cluster ...
💀  Removed all traces of the "minikube" cluster.
```

And, that’s it for this lecture! I hope you enjoyed as much as I did😉  
Practice it by developing a simple project and do this step by step as above, and with time, all these become so natural for you!!

##   
Important info

1. When you work with K8s, always ensure that you run all the commands not as the root user. Create a user and switch to it (e.g., `su devis`) to experiment.
    
2. Do not install minikube if your system has limited memory or frequently hangs. It can slow down your laptop. Instead, consider using online playgrounds for more flexibility, and it's really cool!
    
3. If you've read this far, it's been a long and enjoyable journey with you. Like ❤️ the blog and share it with your friends who might find it useful.
    

## Conclusion

Working with Kubernetes might seem complex at first, but tools like minikube make it simple to learn, experiment, and deploy your own applications locally. By setting up a cluster, writing a few YAML manifests, and deploying a simple app, you’ve come through how containers are managed, scaled and exposed in a real Kubernetes environment.

And **the best way to learn anything is by doing**👩‍💻! So why just scamming through?  
Get your hands dirty, try breaking things, explore different installation options and experiment with pods, services and deployments and with each command you run brings you closer to understanding the complexity behind it and how powerful Kubernetes really is.

**Thank you for reading😄**! I hope you enjoyed learning about Kubernetes!

See you soon with the next one, Until thenn, Byeee🙋‍♀️

![Bye Dog GIFs | Tenor](https://media.tenor.com/X2FM1MIFqy4AAAAM/hi-bye.gif align="left")

💡 **Let’s connect!** Feel free to reach out:  
[**LinkedIn**](https://www.linkedin.com/in/devisri-s-0987b6256/)  
[**GitHub**](https://github.com/Devisrisamidurai)