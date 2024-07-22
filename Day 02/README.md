# How To Dockerize a Project : Day 2 of 40 days of kubernetes 🚀

In today’s fast-paced development environment, ensuring consistency across different stages of deployment can be challenging.

Docker offers a powerful solution to this problem by allowing developers to package their applications and all their dependencies into a single, portable container. This ensures that your application runs smoothly in any environment, from a developer’s laptop to a production server.

In this blog , we’ll guide you through the process of Dockerizing a project.<br>

## Docker workflow 
Dockerizing an application is a crucial step towards achieving a more efficient, scalable, and reliable deployment process.

The process of Dockerizing an application involves several steps shown as follow :

![Docker_workflow](https://github.com/user-attachments/assets/a3ee7a1e-3a3b-4bda-a1f3-04c78d7091af)

### Step 1 : Setting up the application

In our wokflow we used a Node.js app . The app is ready on a github repo, you can clone it from there .

    git clone https://github.com/docker/getting-started-app.git

### Step 2 : Creating the Dockerfile
A Dockerfile is a critical component in the process of containerizing an application. It serves as a script that contains a series of instructions on how to build a Docker image.

Each instruction in the Dockerfile creates a new layer in the container’s filesystem. These layers are stacked on top of each other to form the final Docker image.

The Dockerfile we created for our App is as follows :

<br>

    FROM node:18-alpine
    WORKDIR ./app
    COPY . .
    RUN yarn install --production
    CMD ["node","src/index.js"]
    Expose 3000


Let’s break down the components of the Dockerfile :


<b> From node:18-alpine :</b> we specified the base image we used for our dockerfile , this image is a lightweight, minimal Node.js runtime environment based on the Alpine Linux distribution.

<b> WORKDIR /app :</b> This intruction specifies our work directory inside the container .

<b> COPY . . :</b> This intruction copies all of our files from the current directory on our machine into our work directory inside the container .

<b>RUN yarn install — production :</b> This instruction allows us to install all the necessary dependencies for our App . In our case it’s going to install all the production dependencies for the

<b>CMD [“node”,”src/index.js”] :</b> This instruction specifies the command to run when the container starts. In our case , we’ll be running “node src/index.js” .

<b>EXPOSE 3000 :</b> In this instruction, we specify the port that the port that our application will use to communicate with the outside world.


### Step 3 : Building the Docker Image

After creating the Dockerfile , we used it to build our Docker Image.

A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the application code, runtime environment, libraries, and dependencies already sepecified within the Dockerfile .

To create the docker image for our App, we used the following Docker build command .

    docker build -t day02-todo .

### Step 4 : Push the Docker Image

After building the Docker image, we’ll push it to a Docker repository to make it available to other users, whether in a public or private repository, so they can use it.

First, we have to create a repository within Docker Hub .

<b> Docker Hub </b> is a cloud-based Docker registry service provided by Docker, Inc. It serves as the default and most popular repository for Docker images, allowing users to share and manage their container images.

First, we have to create a repository within Docker Hub . This repository can be Public where images are accessible to anyone or private where images are accessible to specific users only . In our case , our repository is public.

To push the docker image , we have to authenticate to DockerHub using the command :

    docker login

To push our image , we used the following command :

    docker push username/new-reponame:tagname

Now our image is available on the repository .<br><br>

![Dockerhub](https://github.com/user-attachments/assets/b3e73b92-85be-4c83-aef9-b260b793c28c)

<br>
### Step 5: Pull the Docker Image

Now that our image is available and public , anyone from any machine can pull it and use it .

To pull the Docker image, we use the following command :

    docker pull username/new-reponame:tagname

### Step 6: Run the Docker Image

In order to run our app, we need to create a container from the pulled image .

Docker container is a running instance of a Docker image. It encapsulates an application and its dependencies in an isolated environment, providing consistency across multiple environments. When a Docker image is instantiated, it becomes a container that can be started, stopped, moved, and deleted.

To run a Docker image we use the following command :

    docker run -dp 3000:3000 username/new-reponame:tagname

<br>
Let’s break down the different options used in the command :

<b> -d </b> : option used to make the container run into a detach mode so that you can keep using the terminal while the image is running .

<b> -p </b> : specifies the port that the container will expose , we can also specify the mapped port on the Docker Host that will be used to exchange with the container .

Now that we have our container running , our application has become up and accessible . We can check it out on the browser :

![App](https://github.com/user-attachments/assets/23b5676c-5f05-4b9a-8afa-0d6cd2374e97)

<br>

## Conclusion
By completing this lab, we have gained practical experience in containerizing applications with Docker, allowing for consistent, scalable, and portable deployments. This foundational knowledge sets the stage for further exploration of advanced Docker features and orchestration with Kubernetes.

## Ressources
For more informations check out this tutorial by Piyush sachdeva <br>

[![Day 2/40 - How To Dockerize a Project - CKA Full Course 2024](https://img.youtube.com/vi/nfRsPiRGx74/sddefault.jpg)](https://youtu.be/nfRsPiRGx74)

