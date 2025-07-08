## Docker Definition : 

Docker is an open-source platform that allows developers to automate the deployment of applications inside lightweight, portable containers. 

These containers include the application, libraries, and all necessary system dependencies, so they can run consistently across different environments — from development to production. 


## Container Definition: 

A container is a standard unit of software that packages application code along with its dependencies (like libraries, frameworks, configuration files) so it can run reliably on any system — whether it's a developer’s laptop, a test server, or a production cloud environment. 

 Containers are lightweight, isolated, and share the host system's OS kernel, unlike virtual machines 


 ##  Quick Comparison: Container vs Virtual Machine

| **Feature**     | **Container**                  | **Virtual Machine (VM)**      |
|------------------|-------------------------------|-------------------------------|
| **OS Overhead**  | Shares host OS kernel          | Full OS per VM                |
| **Size**         | Lightweight (MBs)              | Heavyweight (GBs)             |
| **Boot Time**    | Seconds                        | Minutes                       |
| **Portability**  | High (runs anywhere with Docker) | Lower                         |

<img width="603" alt="image" src="https://github.com/user-attachments/assets/0eaf27c6-e7cb-4153-b475-b5c5a8bbe790" />



##### Containers and virtual machines are both technologies used to isolate applications and their dependencies, but they have some key differences:
 ### Resource Utilization:
 Containers share the host operating system kernel, making them lighter and faster than VMs.
 VMs have a full-fledged OS and hypervisor, making them more resource-intensive.

 ### Portability: 
 Containers are designed to be portable and can run on any system with a compatible host operating system.
 VMs are less portable as they need a compatible hypervisor to run.

### Security:
VMs provide a higher level of security as each VM has its own operating system and can be isolated from the host and other VMs.
Containers provide less isolation, as they share the host operating system.

---

## Why are containers light weight ?
Containers are lightweight because they use a technology called containerization, which allows them to share the 
host operating system's kernel and libraries, while still providing isolation for the application and its dependencies
 
For example, creating a snapshot of a virtual machine (VM) typically requires at least 1 GB of storage,
whereas a container image might only take around 100 MB. This significant reduction in size makes containers lightweight
and much easier to ship and deploy across environments — whether to Docker, Kubernetes, or other platforms. 

Containers are lightweight by design because they do not include a full operating system. Instead, they share the 
host OS kernel and only package the application along with its required libraries and dependencies.
This makes containers faster to start, smaller in size, and easier to move between development, testing, and production environments. 


A Docker image is a read-only template used to create containers. It contains everything needed to run an application, including: 

- A base image (such as Ubuntu, Alpine, or Debian), 

- The application code, 

- The application’s dependencies (libraries, runtime, binaries), and 

- Any system-level dependencies required for the app to function. 

Docker uses minimalistic base images like Alpine (just ~5MB) to keep images lightweight. These base images provide only the essential components of an OS, reducing size, improving speed, and enhancing security. 

## So in short: 

>Docker Image = Base Image (minimal OS + system dependencies) + App Code + App Libraries 

When you run a Docker image, it becomes a container — an isolated, executable environment that behaves the same no matter where it runs. 

---
# Life cycle of Docker
<img width="531" alt="image" src="https://github.com/user-attachments/assets/3620e333-9da5-4073-9928-94ccd0944c8d" />

 ## 1. Dockerfile 
A Dockerfile is a text file with a set of instructions written by the developer. 
It defines how to build a Docker image — including base image, app code, dependencies, and runtime instructions. 

### Example : sample Docker File  

```bash
FROM node:18 

COPY . /app 

WORKDIR /app 

RUN npm install 

CMD ["node", "server.js"]
```

 ## 2. Build Step (Command: docker build) 
The Docker Engine reads the Dockerfile and builds an image using the instructions. 
This image is a snapshot that contains the app, dependencies, and base environment. 

## 3. Docker Image 
A Docker Image is a read-only template created from the Dockerfile. 
You can think of it like a "recipe" to create containers. 

Images can be stored, shared, and reused. 

 ## 4. Run Step (Command: docker run) 
When you run the image using the Docker Engine, it creates a container. 
This container is a live, isolated environment running the application. 

## 5. Container 
A container is the running instance of an image. 
It’s lightweight, fast, and consistent across environments. 
You can run multiple containers from a single image. 

## 6. Docker Engine 
The core engine that handles: 
Building images from Dockerfiles 
Running containers 

Executing Docker commands (like build, run, stop, remove, etc.) 

## Summary (Real-world analogy): 
Dockerfile = Cooking instructions 

Image = Ready-to-bake frozen pizza 

Container = Hot pizza ready to eat 

Docker Engine = Oven that does all the cooking 

Commands = Instructions you give the oven (like "bake this at 180°C") 

 


 
