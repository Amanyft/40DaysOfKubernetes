# Beginner's Guide to Docker: Day 1 of 40 days of kubernetes 🚀 

## What is Docker ?
Docker is an open-source platform that enables developers to automate the deployment, scaling, and management of applications within lightweight, portable containers. These containers package an application and its dependencies together, ensuring that the application runs consistently across different environments.

## Why Docker is essential for kubernetes ?
Docker is essential for Kubernetes because it provides the foundational container technology that Kubernetes orchestrates.
Docker's containerization, image management, lightweight nature, integration capabilities, and support for development workflows make it a crucial component in the Kubernetes ecosystem. Together, Docker and Kubernetes enable efficient, consistent, and scalable deployment and management of containerized applications.

## Containers VS virtual Machines
The following diagram illustrates the architecture using VMs Vs containers:
![Container_VM](https://github.com/user-attachments/assets/9a6eaab9-2c99-444f-9749-4cbe7d008d98)

Containers and virtual machines (VMs) are both technologies used to isolate applications and their dependencies, but they operate in fundamentally different ways and have distinct characteristics.
Here's some of the key differences :

### Architecture :
Containers are lightweight , they share the Host OS kernel and use isolated user space. They include the app as well as all of its dependencies.
Virtual Machines on the other hand, includes a complete OS, including the kernel, which makes them heavier, they run a separate OS instance on top of this virtualized hardware. They include the application, all its dependencies, and an entire OS.

### Ressource utilization :
Containers share resources and have minimal overhead, allowing more containers to run on the same hardware compared to VMs. They start in seconds because they don't boot a full OS.
VMs require more resources (CPU, memory, storage) because each VM includes a full OS. They take minutes to boot because they need to start an entire OS.

### Portability :
Containers can run on any system that supports Docker, ensuring consistency across different environments (development, testing, production). Docker images can be easily shared and distributed via container registries like Docker Hub.
VMs can be moved between compatible hypervisors, but the process is more complex and resource-intensive.

## Docker Architecture
![Docker_Architecture](https://github.com/user-attachments/assets/9dae100e-6bbf-4cc3-be60-0ca2a822e830)

Docker architecture is designed to provide a robust, efficient, and scalable way to manage and deploy containerized applications.
Here's an overview of the key components and how they interact:
Docker Client : a command-line tool that communicates with the Docker daemon. Users use commands like docker build, docker run, and docker pull to interact with Docker.
###### Docker Host : 
consist of the machine that runs the Docker Daemon and containers. The Docker Host can be a physical machine, a virtual machine, or a cloud instance.
###### Docker Demon (dockerd): 
runs on the host machine. It listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes.
It creates, runs, and monitors containers. The daemon can be on the same host as the client, or they can communicate over a network.
###### Docker Images & containers :
Docker images are read-only templates used to create containers. They contain the application and its dependencies, along with the necessary configuration.
Containers are runnable instances of Docker images. They encapsulate the application and its environment, ensuring consistency across different environments.
###### Docker registry : 
a centralized repository where Docker images are stored, managed, and distributed. It plays a crucial role in the Docker ecosystem, enabling users to share and deploy containerized applications seamlessly.

## Docker workflow example 
![worklow](https://github.com/user-attachments/assets/891af528-be19-45c0-88ec-653a9190e8e2)

The docker workflow starts with writing the Dockerfile that contains all the commands a user could call on the command line to assemble an image.

Example of a Dockerfile :

    # Use an official Node.js runtime as the base image
    FROM node:14
    # Set the working directory
    WORKDIR /app
    # Copy package.json and package-lock.json to the working directory
    COPY package*.json ./
    # Install dependencies
    RUN npm install
    # Copy the entire project directory into the container
    COPY . .
    # Expose port 3000 to the outside world
    EXPOSE 3000
    # Command to run the application
    CMD ["npm", "start"]

Following that we run the build command to build the docker image for the app , we use the following command :

    docker build -t myapp .

After building the image we push it to the docker registry . The most common docker registry is DockerHub . We use the following command :

    docker push myrepository/myimage:tag

Now the image is available on DockerHub and accessible to anyone (public). To use that it on any machine, we need to pull it first. For that pupose we use the following command :

    docker pull myrepository/myimage:tag

After pulling the docker image, we run it so we get our container ready ,up and running . We use this command :

    docker run -dp 3000:3000  myrepository/myimage:tag

## Conclusion
Containerizing applications using Docker simplifies deployment processes, improves scalability, and streamlines dependency management.
By packaging applications into containers, Docker guarantees uniform performance across diverse environments, establishing itself as an essential asset in contemporary software development and deployment workflows.

For more information go through this video by Piyush Sachdeva.

[![Day1/40 - Docker Tutorial For Beginners](https://img.youtube.com/vi/ul96dslvVwY/sddefault.jpg)](https://youtu.be/ul96dslvVwY)


    
