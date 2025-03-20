---
title: "Docker Volumes: What You Need to Know?"
datePublished: Thu Mar 20 2025 04:56:02 GMT+0000 (Coordinated Universal Time)
cuid: cm8gvp0dr001d08jvavhycjfk
slug: docker-volumes-what-you-need-to-know
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742442788367/f8afb3ee-8cc6-4bd0-9d13-9df5b8ae7cd7.png
tags: docker, devops, cloudnative, bind-mount, docker-volumes

---

Hi everyone,

Docker has truly transformed the world of containerization by making applications lightweight and portable. However, it initially faced a significant challenge: data persistence. As we saw, containers are ephemeral, meaning any data written inside them is lost when they stop or are deleted. This is where **Docker volumes** come into play, providing **persistent storage for containers**.

In this article, we'll dive into why Docker volumes were needed, the problems they solve, the different types of volumes, and how they compare with bind mounts. We'll also explore real-world examples to help you understand their importance, along with hands-on practices on how to create, destroy, and restart a volume while navigating through its lifecycle. So, let's get started!

Make sure to check out other blogs on Docker, as this blog is part of a continuation series on the #Docker topic.

---

### **The Big Problem: Why Does Docker Need Volumes?**

Imagine this: every time a **Docker container stops or gets removed, all the data inside it vanishes**. That's because containers are meant to be temporary. While this works **great for stateless applications**(it does not keep track of the application logs or any data), it's a real headache for apps that need to keep data around. Think about:

* **Databases** like PostgreSQL, MySQL, or MongoDB, which hold vital user and transaction data for financial apps.
    
* **Application logs** that are crucial for debugging and monitoring.
    
* **User uploads** such as images, documents, or videos that need to stay put even if the app restarts.
    

Without a way to keep data safe, using Docker for these tasks would be an absolute mess. That's why Docker introduced Volumes—a solution for storing data persistently, separate from the container's lifecycle.

**Let's look at a real-world example:**  
Imagine an **e-commerce platform like Amazon**, which uses a **microservice** architecture. Your database service needs to persist order history, customer details, and inventory data even if the database container is restarted. Using Docker volumes, you can store this data on the host machine or in a cloud storage backend while keeping your application stateless and scalable. When you place an order, data such as your cart items, order details, and transaction records need to be stored permanently.

* **Product Images & Static Files:** Stored in Docker volumes to persist across deployments.
    
* **Database Data:** Stored in a volume to ensure no information is lost when updating or restarting the database container.
    
* **User Sessions & Logs:** Shared between services using volumes for better tracking and debugging.
    

Without volumes, every restart would mean losing customers’ orders, product listings, and transaction history — it’s a disaster for any online store!

### **Problems:**

To conclude, below are the three major problems faced in terms of data storage in docker containers:

* ***A container couldn't write files, and the system failed to keep records of previous logs, and so compromising the details.***
    
* ***If the backend systems go down, the classic frontend and backend sharing information with each other causes the problem to persist.***
    
* ***Your app tries to read a file from the Host OS but doesn't know how to do it because containers run in isolated environments.***
    

To solve these, Docker came up with two concepts, **Volumes and Bind mounts**.

---

1. **Volumes**
    
    Think of volumes as a **reliable storage solution** that Docker manages for you. It does not depend on your host machine’s directory structure and OS, volumes are **independent and portable**. This makes them a great choice when you need to back up, **migrate, or share data** between multiple containers.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742439679592/4d1f6ae5-1f0e-4243-9773-22af1ba82ca4.png align="center")
    
    One of the biggest advantages? **Performance.** When you write data directly into a container’s filesystem, it relies on a storage driver, which adds overhead and slows things down. Volumes, on the other hand, **write straight to the host filesystem**, making them much faster and more efficient. Plus, they don’t bloat your container size.
    
    Now, you might wonder, *“****Should I always use volumes?****”*  
    Well, not necessarily. If you need direct access to files from both the host and the container, bind mounts might be a better choice. But if you’re **looking for a clean, managed, and high-performing storage option** that works across different environments, volumes are your best bet.
    
    **The Lifecycle of Volumes:**
    
    Think of a Docker volume like a separate storage unit—it exists independently of any container. Even if you delete a container, the volume (and its data) **stays intact**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742444039505/b720d130-16f5-4fe0-b095-debb4915af6c.png align="center")
    
    For example, if you have a **PostgreSQL container** storing data in a volume, you can remove and recreate the container without losing your database. Since volumes can be shared, multiple containers can access the same data simultaneously.
    
    And don’t worry—volumes **don’t disappear** **on their own**. If you ever need to clean up unused ones, just run:
    
    ```bash
    docker volume prune
    ```
    
2. **Bind Mounts**
    
    Bind mounts work differently from volumes—what it does is that **they link a specific folder on your host machine to a container**. This means changes inside the container **directly affect** the files on your host, and vice versa.
    
    For example, if you mount a local directory to a **Nginx container’s** folder, any updates you make to the config file on your host will instantly reflect in the running container. This makes bind mounts great for development when you need live updates without rebuilding the container.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742441517742/51ec0967-45a4-4bd8-b545-52db369a7ebe.png align="center")
    
    However, since bind mounts depend on the host’s filesystem, they **aren’t as portable or safe** as volumes. If you accidentally delete or move files on the host, the container loses them too.
    
    So, if you need fast, host-container file sharing, bind mounts are useful. But for better persistence and portability, **volumes** are the way to go!
    
    Here, the busybox image runs a container that mounts/binds the host data to container data.
    
    ```bash
    docker run -d -v /host/data:/container/data busybox
    ```
    

---

### **Types of Docker Volumes**

Docker offers several types of volumes, each designed to meet different needs and use cases. Understanding these types is important and can help you choose the best option for your specific scenario.

1. **Anonymous Volumes:**
    
    Docker offers different types of volumes to fit various needs, and one of these is **Anonymous Volumes**. These are **created automatically when a container starts** and are perfect for situations where a container needs **temporary storage**. They provide a seamless way to manage data that doesn't need to persist beyond the container's lifecycle, making them an ideal choice for short-term data handling.
    

```bash
docker run -d — rm -v /data busybox
```

Here, the busybox image runs a container instance in a detached mode and removes a volume attached to it named /data.

2. **Named Volumes:**
    
    The another one of the key types is the Named Volumes. These are **explicitly created and managed by Docker**, offering a reliable way to handle data that needs to stick around. The best part is that these named Volumes can be **shared between multiple containers**, making them perfect for scenarios where you want different containers to access the same data effortlessly. Whether you're running a multi-container app or just need a robust data storage solution, Named Volumes has got your back!
    

```bash
docker volume create named-volume
docker run -d -v named-volume:/app/data busybox
```

---

### **Volumes vs Bind Mounts**

**Volumes** are managed by Docker and are the preferred way to persist data in Docker.

**Bind Mounts** allow you to directly map host directories to containers, providing more control but requiring careful management.

| **Volumes** | **Bind mounts** |
| --- | --- |
| It is managed by the Docker platform itself | Not managed by Docker. |
| Platform independent. | Platform dependent. |
| More secure | Less secure |
| Storing persistent data | Accessing specific files on the host. |

---

### Some Hands-on practice for you!

Now it's time for us to experiment with volumes.This hands-on practice will help us grasp the practical applications of volumes and how they can enhance our Docker workflows.

The below example **creates a new volume named my-volume and lists all the available volumes** in the specific folder.

```bash
docker volume create my-volume
docker volume ls
```

**Inspect the volume** to know the details about the volume created such as its labels, the name of the volume scope (global or local) and its mount point etc..,

```bash
docker volume inspect my-volume
#output
docker volume inspect my-vol
[
    {
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/my-vol/_data",
        "Name": "my-vol",
        "Options": {},
        "Scope": "local"
    }
]

#now remove the volume 
docker volume rm my-volume
```

When you kick off a container with a volume that isn't there yet, Docker will make the volume for you. Check out the below example where the volume `myvol2` gets mounted into `/app/` the container.

Both the `-v` and `--mount` examples do the same thing. Just remember, **you can't run both unless you delete the** `my-vol` **container and the** `myvol2` **volume after doing the first one.**

```bash
docker run -d \
  --name my-vol \
  --mount source=myvol2,target=/app \
  nginx:latest
```

```bash
docker run -d \
  --name my-vol \
  -v myvol2:/app \
  nginx:latest
```

Now you can delete and remove the volumes as well if you want to. Be careful when you do this,cuz it can’t be undone!

```bash
#stops the running container
docker container stop devtest
#remove the stopped container
docker container rm devtest
#delete the volumes if you dont want the stored data anymore
docker volume rm myvol2
```

Good job! You have learned some of the essential commands to manage the lifecycle of volumes!

---

### **Conclusion**

Docker volumes solve one of the biggest challenges in containerized environments that is data persistence.They **allow applications to maintain state,share data,and ensure important files are not lost even if a container stops or crashes**.By using volumes wisely,you can make your Dockerized applications more scalable,resilient and production ready.Get some hands on practices so that you get a grasp of how volumes are handled in Dockers!

That’s it for this one.

**Thanks for reading! Will see you soon with the next blog!**

**Let’s connect**!  
[**LinkedIn**](https://www.linkedin.com/in/devisri-s-0987b6256/)  
[**Github**](https://github.com/Devisrisamidurai)